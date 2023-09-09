# Handler
> 간단하게 http요청을 다루는 것

## 예제 코드
```go
package main

import (
	"fmt"
	"net/http"
)

type concreteHandler struct{}

func (f *concreteHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	fmt.Fprint(w, "Hello, here concreteHanlder")
}

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprint(w, "Hello, world")
	})

	http.HandleFunc("/name", func(w http.ResponseWriter, r *http.Request) {
		name := r.URL.Query().Get("value")
		if name == "" {
			name = "noname"
		}
		fmt.Fprintf(w, "My name is %s", name)
	})

	http.Handle("/funcA", &concreteHandler{}) // 구조체 선언 및 call by reference

	http.ListenAndServe(":3000", nil)
}

```

### 해석
* http.HandleFunc
  * 첫 번째 인자로 루트주소로 부터의 주소를 받고, 두 번째 인자로 해당 주소로 이동시 실행할 함수를 받는다
  * 두 번째 인자의 함수는 첫 번째 인자로 http.ResponseWriter라는 응답을 줄 수 있는 변수이고, 두 번째 인자로 *http.Request라는 요청을 다루는 변수이다.
* http.Handle
  * http.HandleFunc과 기능적으로 같으며, 다른점은 두 번째 인자로 handler라는 인터페이스에 정의된 ServeHTTP라는 함수를 오버라이딩해서 받는다.
* r.URL.Query().Get(string)
  * *http.Request에서 오는 URL에 쿼리문에서 string에 해당하는 부분을 get할 수 있다.
  * ex) localhost:3000/name?value=kim
  * 이면, r.URL.Query().Get(value)이니까, value의 값인 kim을 받아와 반환한다.