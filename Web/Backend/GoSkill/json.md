# JSON I/O
> Json을 구조체 형태로 받고 다시 json으로 변환해서 응답 함

## 예제 코드
```go
package main

import (
	"encoding/json"
	"fmt"
	"net/http"
	"time"
)

type Info struct {
	FirstName string    `json:"first_name"`
	LastName  string    `json:"last_name"`
	Email     string    `json:"email"`
	CreatedAt time.Time `json:"created_at"`
}

type concreteHandler struct{}

func (f *concreteHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	userInfo := new(Info)
	err := json.NewDecoder(r.Body).Decode(userInfo) // info형태로 json을 받음
	if err != nil {
		w.WriteHeader(http.StatusBadRequest)
		fmt.Fprint(w, "Decoder error: ", err)
		return
	}
	userInfo.CreatedAt = time.Now()

	data, _ := json.Marshal(userInfo) // info형태의 정보를 json형태로 변환해서 data에 저장
	w.Header().Add("content-type", "application/json")
	w.WriteHeader(http.StatusOK)
	fmt.Fprint(w, "json: ", string(data)) // 본래 json은 일종의 string이기 때문에 byte array타입인 data를 다시 string으로 변환해줌
}

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprint(w, "Hello, world")
	})

	mux.HandleFunc("/name", func(w http.ResponseWriter, r *http.Request) {
		name := r.URL.Query().Get("value")
		if name == "" {
			name = "noname"
		}
		fmt.Fprintf(w, "My name is %s", name)
	})

	mux.Handle("/funcA", &concreteHandler{}) // 구조체 선언 및 call by reference

	http.ListenAndServe(":3000", mux)
}
```

#### 시행착오
* 구조체를 소문자로 정의해서 json패키지에서 해당 구조체를 인식하지 못했음
* 구조체의 필드를 소문자로 정의해서 외부 패키지에서 참조할 수 없었음