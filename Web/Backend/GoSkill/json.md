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

type info struct {
	firstName string    `json:"first_name"` // json은 키값으로 언더바표기법을 가지기 때문에 백틱으로 json에서는 이런 이름으로 사용할 것을 명시
	lastName  string    `json:"last_name"`
	email     string    `json:"email"`
	createdAt time.Time `json:"created_at"`
}

type concreteHandler struct{}

func (f *concreteHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	userInfo := new(info)
	err := json.NewDecoder(r.Body).Decode(userInfo) // info형태로 json을 받음
	if err != nil {
		w.WriteHeader(http.StatusBadRequest)
		fmt.Fprint(w, "Decoder error: ", err)
		return
	}
	userInfo.createdAt = time.Now()

	data, _ := json.Marshal(userInfo) // info형태의 정보를 json형태로 변환해서 data에 저장
	w.Header().Add("content-type", "application/json")
	w.WriteHeader(http.StatusOK)
	fmt.Fprint(w, "json: ", data) // 본래 json은 일종의 string이기 때문에 byte array타입인 data를 다시 string으로 변환해줌
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