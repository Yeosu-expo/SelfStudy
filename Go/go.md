# Go
매우 빠른 데이터전달이 가능한 언어

go는 package에서 기능들을 가져와 쓸 수 있다. 일종의 라이브러리인 샘이다. 조금 다른점은 함수가 대문자로 시작하는 경우만 가져다 쓸 수 있다. 즉, 소문자로 시작하는 함수는 일종의 private상태인 것이다. 같은 패키지에서만 사용한다면 소문자로 선언해도 된다는 뜻

## 기본 문법
### 변수
선언
```go
var name string = "kim"
name := "kim" // 같은 문장임
```
***
### 함수
```go
func getValue(name string) (int, string){
    return len(name), strings.ToUpper(name)
}

func printWords(words ...string){ // ...자료형 식으로 명시하면 array형태로 받아올 수 있음
    fmt.Println(words)
}

func main(){
    name := "kim"
    first, second := getValue(name)
    fmt.Println(first, second) // 3 KIM
    firstt, _ := getValue(name) // _는 리턴값을 무시한다는 뜻.
    fmt.Println(first) // 3

    printWords("kim", "park", "lee") // [kim, park, lee]
}
```

리턴 값이 하나가 아닌 함수는 그 리턴값을 다 받아줄 변수가 필요함. 그러지 않으면 오류가 뜸. 이때 언더바로 값을 받으면 그 리턴값은 무시한다는 뜻임.

getValue함수를 아래와 같이 써도 똑같이 돌아간다. 다른점은 리턴 값을 저장할 변수를 미리 지정하고 함수가 반환되면 자동으로 지정된 리턴 값이 담긴 변수를 리턴한다.
```go
func getValue(name string) (length int, upperName string){
    length = len(name)
    uppercase = strings.ToUpper(name)
    return
}
```
#### defer
```go
func getValue(name string) (length int, upperName string){
    defer fmt.Println("function done")
    length = len(name)
    uppercase = strings.ToUpper(name)
    return
}

func main(){
    name := "kim"
    first, second := getValue(name)
    fmt.Println(first, second)
    // function done
    // 3 KIM
}
```
defer는 함수가 종료된 시점에서 미리 입력된 명령을 수행한다.

***