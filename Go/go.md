# Go
매우 빠른 데이터전달이 가능한 언어

go는 package에서 기능들을 가져와 쓸 수 있다. 일종의 라이브러리인 샘이다. 조금 다른점은 함수(함수 말고도 다른 것도 포함)가 대문자로 시작하는 경우만 가져다 쓸 수 있다. 즉, 소문자로 시작하는 함수는 일종의 private상태인 것이다. 같은 패키지에서만 사용한다면 소문자로 선언해도 된다는 뜻

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

### for
```go
numbers := []int{1,2,3}
for index,number := range numbers{
    fmt.Println(index, number)
}
// 0 1
// 1 2
// 2 3

for i := 0; i< len(numbers); i++ {
    fmt.Print(numbers[i])
}
// 0 1
// 1 2
// 2 3
```
go의 반복문은 for문 하나이다.
두 for문은 같은 코드이다. 보다싶이 range는 두가지 리턴값이 있고, 첫 번째는 index값 두번째는 value이다.
### if
```go
num = 19
if realnum:=num+1; num < 20{
    isTrue := true
}
isTrue := false

// isTrue = false
```
다른 언어의 if문과 다르게 if문 조건 앞에서 if문 안에서 사용될 변수를 선언할 수 있다.
### switch
```go
switch realAge := age + 2; realAge {
    case 20:
        return true
    case 50:
        return false
}

switch {
    case age < 20:
        return false
    case age >= 20:
        return true
}
```
위와 같이 switch문에서 변수를 만들 수 있고, switch변수를 지정하지 않아도 case문에서 조건으로 구분할 수도 있다.
### array
```go
names := [3]string{"kim", "park", "lee"}
names := []string{"kim", "park", "lee"} // 위의 코드와 같은 코드

names = append(names, "choi") // ["kim", "park", "lee", "choi"]
```
배열의 크기를 지정해줘도 되지만, 지정하지 않아도 알아서 원소 수만큼 크기가 정해진다. 이것을 slice라고 한다.
원소를 추가하고 싶으면 slice와, 배열에 추가할 값을 인자로 받는 append함수를 사용하고, append함수는 새로운 원소가 추가된 배열의 주소를 반환한다.
### map
```go
info := map[string]int{"kim":10, "lee":12}
```
key와 value의 자료형을 위와 같이 선언할 수 있다. 또한, for문에서 range로 탐색시 반환 값은 key,value 값이다.

한 가지 주의할 점은 빈 map을 선언할 경우 뒤에 {}을 붙여주거나 make함수로 선언해주어야 한다. 그러지 않으면 null값이 변수에 들어간다.

### struct
```go
type Info struct{
    Name string
    Age int
}

myInfo := Info{"kim", 20}
myInfo := Info{name:"kim", age:20} // 같은 코드임
```
여기서 type은 struct라는 자료형으로 Info라는 이름으로 새로운 자료형으로 선언하겠다는 뜻이다.
```go
type Dictionary map[string]string
```
처럼 선언할 수도 있다. 그러면 Dictionary map으로써 사용되는 새로운 자료형이다.

참고로 위의 구조체에서는 Info의 변수들을 대문자로 선언했기에 info(name, age)로 객체를 선언할 수 있다.
하지만 소문자로 변수를 선언하면 다른 패키지에서 name, age를 직접 접근할 수 없다.
즉, 접근할 수 있는 함수를 따로 public으로 만들어줘야한다.

Go에는 class도 없고, 그렇기 때문에 생성자도 없다. 그래서 Go에서는 struct를 잘 활용해야 한다.
하지만 class의 생성자를 흉내낼 수는 있다

#### Constructor
```go
type Info struct{
    name string
    age int
}

func NewInfo(name string) *Info{ // Constructor
    return Info(name:name, age:20)
}

func (i *Info) GetAge() int{
    return i.age
}

info := NewInfo("kim")
fmt.Println(info.GetAge()) // 20
```
GetAge함수는 private인 age변수를 가져온다. 여기서 (i *Info)는 해당 자료형으로 함수를 접근할 수 있게한다.
참고로, Go에도 포인터의 개념이 있기 때문에 i를 *Info가 아닌 Info로 선언하면, 객체를 복사하기 때문에 메모리 낭비가 생긴다.
또한, 함수가 객체의 정보를 수정한다면, 복사된 객체에서 수행하기 때문에 수정된 사항이 본래 객체에 적용되지 않을 수도 있기 때문에, 때에 따라 맞게 사용해야한다.

#### Method String
Go에는 struct를 위한 기본 함수 String이 있다. 이 함수는 struct를 출력하면 표시할 문자열을 반환값으로 정의할 수 있다.
```go
type Info struct{
    name string
    age int
}

func (i Info) String() string{
    return "I'm String Method in struct"
}

info:=NewInfo("kim")
fmt.Println(info) // I'm String Method in struct
```

***
### Error
만약 함수를 실행시켰는데 특정 조건에 부합하지 않아 에러가 있다는 것을 알리기 위한 자료형이다.
자료형이기 때문에 두 가지 정보가 담길 수 있다. 첫 번째는 에러메세지, 두 번째는 nil. nil은 문자열에서 null과 같은 의미이다.
```go
func isTrue(value bool) error{
    if(value){
        return nil
    }
    return error.New("value is not True")
}

err := isTrue(false)
if err != nil{
    fmt.Println(err) // value is not True
}
```