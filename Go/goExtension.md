# Go 심화
## Goroutines
Go의 핵심기능이다. 일반적인 프로그램이 실행되는 순서는 코드의 흐름이다. 즉, A함수 다음 B함수가 코딩되어있으면, A함수가 끝나고 B함수가 진행된다. 하지만, 고루틴은 A함수와 B함수를 동시에 실행시킨다. 즉, 병렬성 연산이다.

고루틴에는 채널이라는 개념이 있다. 채널은 동시에 실행되는 함수끼리의 또는 함수와 메인함수의 소통방법이다.

1. main 함수에서 A,B함수가 고루틴으로 동시에 실행하고 있음
2. A함수가 채널을 통해 main함수에 정보를 전달함
3. 거의 동시에 B함수가 main함수에 채널을 통해 정보를 전달함 (A,B 어느 누가 먼저 main에 도착할지는 모름)
4. main함수 종료

이것을 코드로 나타내면 아래와 같다.
```go
func main() {
	c := make(chan string)
	Names := [4]string{"kim", "park", "lee", "choi"}
	for _, name := range Names {
		go sayName(name, c)
	}
	for i := 0; i < 4; i++ {
		fmt.Println(<-c) // read channel (if you don't read channel, goroutines will be ignored.)
        // beacaues, that means main function won't receive channel
	}
}

func sayName(name string, c chan string) {
    time.Sleep(time.Second * 3) // you can omit this code
	c <- "My name is " + name // send to main
}
```
My name is kim</br>
My name is lee</br>
My name is choi</br>
My name is park</br>

실행결과의 순서는 달라질 수 있다. 중요한 건 동시에 결과물이 나온다는 것이다.
함수를 보면 3초간 함수가 멈춰있다. 이 말은 이 함수를 수행하는 쓰레드가 멈춰있다는 뜻이다.
만약 고루틴을 사용하지 않으면, 3초 쉬고 첫 문장 출력, 3초 쉬고 두 번째 문장 출력 .... 되었을 것이다.
고루틴을 사용했기 때문에 동시에 3초를 기다리고 한꺼번에 출력한다.
다시 말해 고루틴 입장에서는 sayName함수를 실행하고 출력하는 과정이 한 루틴이고, 동시에 4번 일어난다는 것이다. 즉, 하나의 고루틴 입장에서는 channel을 read하는 for문이 하나의 출력만 실행되는 것처럼 보인다.

여기서 주의할 점은 채널이다. 고루틴을 사용할 때, 채널로 main함수와 연결하지 않으면, main함수는 go루틴함수를 무시하고 진행한다.

```go
func main() {
	Names := [4]string{"kim", "park", "lee", "choi"}
	for _, name := range Names {
		go sayName(name)
	}
	fmt.Println("1")
}

func sayName(name string) {
	time.Sleep(time.Second * 10)
	fmt.Println(name)
}
```
실행결과는 1만 출력된다. 10초도 기다리지 않는다. 왜냐하면 고루틴 함수가 무시되었기 때문이다.