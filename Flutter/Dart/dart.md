# Dart Lang
## 특징
1. JIT & AOT
2. null safety

### JIT & AOT
쉽게 말해서 Just-In-Time(JIT)는 개발 도중, 코딩하는 즉시 결과를 확인할 수 있는 것을 의미한다. 예를 들어 웹페이지를 설계한다고 했을 때, 버튼의 디자인을 수정함과 동시에 옆에서 수정된 디자인을 확인할 수 있게 한다는 것이다. 이게 가능한 이유는 Dart VM이라는 것이 개발 중 계속 돌아가기 때문에 금방 피드백을 받을 수 있는 것이다.

그리고, 코드를 배포할 때는 AOT라는 것을 활용한다. AOT는 c, c++에서 배포할 때 코드를 한꺼번에 컴파일해서 배포하게 되는데 이것을 AOT라고 한다. 개발 도중 AOT 대신 JIT를 사용하는 이유는 AOT는 기계어로 배포하기 때문에 속도가 매우 빠르지만, 개발 도중 코드를 수정할 때마다 피드백을 얻기 위해 컴파일을 한다는 것은 매우 비효율적이다.(컴파일된 파일은 빠르지만, 컴파일하는 과정이 무겁기 때문)

결국 개발 도중에는 느리지만 피드백을 계속 받을 수 있는 JIT를 사용하고, 개발완료 시점에서는 배포를 위해 AOT를 사용한다고 할 수 있다.

### null Safety
개발에서 null은 참조시 오류를 일으키는 값이지만, null가지는 특수함 때문에 개발에서 null값은 필요하다. 메모리에 값의 부재를 의미하는 null은 다른 것으로 대체하여 표현할 수 없고, null값은 개발자의 실수나 의도에 따라 들어가는 것이 옳은 경우도 있기 때문이다.

그렇지만 앞에서 말했듯이 null은 개발자의 의도대로 사용된 것이 아니라면, 오류를 일으킨다. 이 오류의 가장 큰 문제점은 null값은 컴파일시에는 오류를 일으키지 않지만, 프로그램 실행단계에서 오류를 일으키기 때문에 문제가 된다. 즉, 사용자에게 배포된 시점에서 오류를 일으킬 수 있다는 것이다.

이를 해결하기 위해 Dart가 null을 대하는 매커니즘이 null safety이다. null safety는 일반적인 변수에는 null값이 안들어간다는 전재하에 동작하도록 한다. 그렇기 때문에 null없다는 전제하에 실행되기 때문에 null로 인한 오류도 없다. 하지만, 앞에 말했듯이 null은 개발에 있어 필요한 값이다. 이를 위해 Dart에서는 변수 선언시 해당 변수에 널이 들어갈 수 있음을 변수 선언 단계에서 알려줌으로써, 그 변수에서는 null값을 사용할 수 있게 해준다. 그리고 그 변수를 사용할 때는 null인지 아닌지 구분해서 코딩하도록 되어있다. 구체적으로 if문으로 null일때와 아닐때를 구분하는 것도 있지만, 변수명?.함수 이런식으로 변수명 뒤에 ?를 붙여서 null이면 함수가 실행되지 않고, null이 아니면 함수가 실행되지 않도록 동작한다.

```dart
String? name = "name"; // null값이 들어갈 수 있는 변수
name?.length; // null이 아닐때 함수가 실행됨
```

## 기능
##### 변수 선언
기본적으로 타입을 명시하고 선언해도 되지만, var로 선언해도 된다. dart에서 알아서 변수에 들어가는 값을 받고 유추해서 타입을 정한다. 하지만 한번 정해진 타입이 있는 변수에는 다른 타입 값이 들어갈 수 없다.

##### dynamic
dynamic이라는 타입이 있는데 이것은 변수의 타입이 다이나믹하게 변경 가능하다는 뜻이다. 즉, 문자열 값이 들어갔다. 정수형이 들어갈 수도 있다는 것이다.

##### final & const
dart에는 다른 언어의 const랑 비슷한 final과 const가 있다.
final은 우리가 알고 있는 const랑 비슷하게 한 번 값이 세팅되면 바뀌지 않는다. 하지만 dart에서 const는 final과 다르다. 한 번 값이 세팅되면 바뀌지 않는 것은 같지만, const는 컴파일 시점에서 이미 변수가 값을 구체적인 값을 알고 있어야한다. 다시 말해서 final변수는 프로그램이 실행되고 사용자에게 값을 받아오거나, API요청을 통해서 값을 받아오는 것이 가능하다. 반면 const는 컴파일 과정에서 이미 값을 알고 있어야 하기 때문에 프로그램 배포 이전, 즉, 컴파일 시점에 이미 변수에 값이 들어가야한다는 차이점이 있다.

##### late
final은 변수 선언당시 들어갈 값이나 리턴 값이 있는 함수를 변수에 넣어주면 되지만, 필요에 따라 나중에 값을 넣어주고 싶을 때가 있을 것이다. 이때 late키워드를 사용하면된다. 그러면 변수를 먼저 선언만 하고 나중에 값을 넣어줘도 된다.
```dart
late final name;
name="somthing";
```
또한 final과 함께 쓰지 않아도 명시적으로 나중에 값을 넣어준다는 뜻이기도 하다.

##### String with var
문자열안에 변수를 넣어서 문자열을 완성시킬 수 있다. 추가적인 작업이 필요하다면 중괄호 안에서 해주면 된다.
```dart
String name = "kim"
int age = 20;
String greeting = 'My name is $name and i\'m ${age + 3}.'
```
문자열을 작은따옴표나 큰따옴표 어떤 것으로든 감싸도 되지만, 감싼 따옴표가 문자열 안에 있을 때는 역슬래시와 함께 써주어야한다.

***
#### 자료구조
##### List
```dart
List<int> numbers1 = [1,2,3,4,];
var numbers2 = [1,2,3,4,]; // 위의 코드와 같음

bool isTrue = true;
var numbers3 = [
    1,
    2,
    3,
    4,
    if(isTrue) 5,
];
print(numbers3); // [1,2,3,4,5]

var oldFriends = ["kim", "lee"];
var newFriends = [
    "park",
    "choi",
    for(var friend in oldFriends) "*$friend*",
];
print(newFriends); // [park, choi, *kim*, *lee*]
```
if, for 문을 통해 원소를 추가할 수 있음
##### Map
```dart
var map = [ // Map<String, Object> map와 같음
    "first": "kim",
    "second": 12,
    "third": true,
];
Map<int, bool> map2 = [
    1: true,
    2: false,
    3: false,
];
```
다른 자료형에서도 그랬듯이 dart는 var로 선언하면 자료형을 추측해서 정한다. map을 보면 var로 선언했고, 그 안의 원소들이 key값에는 문자열이 value값에는 여러가지 자료형이 있다. 그렇기 때문에 key의 자료형으로 String, value의 자료형으로 어떤 자료형이든 포함하는 개념인 Object로 정해진다.

##### Set
```dart
Set<int> setInt = {1,2,3,4};
setInt.add(1);
setInt.add(1);
setInt.add(1);
print(setInt); //{1,2,3,,4}
```
set은 다른 자료형과 다르게 유니크한 값을 갖는다. 선언은 다른 자료형과 다르게 중괄호로 선언한다.

***

#### Fuction
```dart
String func({String pa1="defalut", int pa2=0, num pa3=0}) => "pa1=$pa1, pa2=$pa2, pa3=$pa3";
String func2({required String pa1, required num pa2}){
    return "pa1=$pa1, pa2=$pa2";
}

func(); // pa1=default, pa2=0, pa3=0
func2(); // error!
func2(
    pa2: 10,
    pa1: "parameter1",
); // pa1=parameter1, pa2=10
```

일반적인 함수정의는 다른 언어와 같다. 만약 함수가 반환만 하는 함수라면 위의 예시와 같이 =>로 바로 반환값을 넘겨줘도 된다.
##### position parameter & named parameter
일반적으로 매개변수를 함수에서 정의하고 함수를 호출할 때, 인자를 넘기는 방법은 정의된 매개변수의 순서대로 함수에 기입하는 것이다. 이때 그 함수의 매개변수를 position parameter라고 한다.

named parameter는 함수의 매개변수를 순서대로 받는 것이 아니라, 매개변수의 이름에 맞게 받는다.
하지만 여기에는 문제가 있다. Dart에는 null safety라는 개념이 있기 때문에 named parameter로 매개변수를 받을 시에 사용자가 매개변수의 값을 안주는 경우를 우려한다. 이를 위한 해결 방법은 2가지가 있다.
첫번째, 매개변수의 default값을 정의해준다.
두번째, 매개변수 정의 앞에 requried 키워드를 붙여 사용자가 해당 매개변수의 정보를 넘겨주지 않으면 안되도록 하는 것.

만약 named parameter를 사용하지 않고, 매개변수를 required하고 싶다면, 아래와 같이하면 된다.
```dart
String func(String pa1, int pa2, [num? pa3 = 10]) => "pa1=$pa1, pa2=$pa2, pa3=$pa3";
```
해당 매개변수를 대괄호로 감싸고 null일 수도 있다는 것을 표기하고 디폴트 값을 넣어준다

***

##### QQ & QQ equal
```dart
// QQ
String func(String? str) => str?.toUpperCase() ?? 'NULL';
print(func(null)) // NULL

//////////////////////////////////
// QQ equal
String? str;
str ??= "New String";
print(str); // New String
```
QQ는 "좌항 ?? 우항"으로 구성되어 있고, 좌항이 null이면 우항을 반환하고, null이 아니면 좌항을 반환한다. 위의 예시를 구체적으로 설명하자면, 먼저 매개변수에 null이 올 수 있기 때문에 자료형에 ?를 붙여준 것이고, 좌항에 ?를 붙여야 str이 null일때 좌항을 실행할 수도 있기 때문이다. 따라서 func(null)은 좌항의 반환 값이 null이기 때문에 우항을 최종적으로 반환한다.

QQ equal은 "좌항 ??= 우항"으로 구성되고, 좌항이 null이면 우항을 좌항에 대입한다. 예시에서는 str에 아직 초기화가 안되서 null이 있고 그래서 "New String"이 str에 들어가게 된다.

***

#### Class
##### Constructor
```dart
class Player{
    String name; // 자료형을 적어줘야 함 class에서는
    int age;
    String team;

    Player(this.name, this.age); // constructor
    
    Player.createBlueTeam(String name, int age) :
        this.name = name,
        this.age = age,
        this.team = 'blue';
    
    Player.creatRedTeam({required String name, required int age}) :
        this.name = name,
        this.age = age,
        this.team = 'red';
}

void main(){
    Player player = Player("kim", 20);
    Player player2 = Player.createRedTeam(
        name: "lee",
        age: 21,
    )
}
```
객체 생성은 new를 붙여줘도 되지만, 안붙여줘도 괜찮다.
this를 통해 생성자에서 매개변수 정의 없이 position parameter로 바로 멤버 변수에 값을 넣을 수 있다.
다른 언어의 생성자와 다르게 생성자를 여러가지 가질 수 있다. 또한 매개변수는 named parameter를 적용할 수도 있다. 뒤에 콜론으로 나눠서 매개변수를 멤버변수에 바로 값을 넣는 것도 가능하다.

##### Cascade operate
```dart
var player = Player("default name". 12);
var player2 = player
    ..name = "new Name"
    ..age = 12
    ..team = 'red';
```
이런식으로 ..을 통해 해당 객체의 멤버에 접근할 수 있다. 멤벼 변수뿐만 아니라 함수까지도 가능하다.

##### abstract class
```dart
abstract class Animal{
    void say();
}

class Cat extends Animal{
    void say(){
        print("Meow");
    }
}

class Dog extends Animal{
    void say(){
        print("Bark");
    }
}
```

##### 상속 inheritance
```dart
class Animal{
    String name;
    Animal({required this.name});

    void say(){
        print("Hi, my name is $name");
    }
}

enum Color {Black, White}; // Enum

class Cat extends Animal{
    Color color;
    Cat({
        required this.color,
        required String name,
    }) : super(name: name); // 상위클래스 생성자로 매개변수 전달

    @override // 오버라이드 명시해주기
    void say(){
        super.say(); // 상위클래스 함수 이어쓰기
        print(" and my color is $color");
    }
}
```

상속과 추상화의 차이는 추상화클래스는 구체적인 정의 없이 해당 클래스를 extends하면 가지고 있어야할 멤버의 존재만 정의한다. 반면 상속은 상위클래스에서 멤버의 정의뿐만 아니라, 구체적인 구현까지도 한다.

##### 접근 지정자
Dart에는 접근 지정자가 public, private 두 가지만, 존재한다.
하지만, 구체적인 것은 다른 언어와 다르다.
먼저 public의 범위는 다른 언어와 마찬가지로 어디서든 접근할 수 있고, 선언은 따로 다른 접근지정자를 선언하지 않으면 public이다. 즉, default이다.
private의 범위는 다른 언어에서는 보통 동일 class에 한정되어 있지만, dart에서는 동일 라이브러리로 한정한다. 또한 선언은 함수명이나, 변수명 앞에 _(언더바)를 붙여주면 된다.

##### Mixins
```dart
class Powerful{
    int powerLevel = 100;
}

class Fast{
    void run(){ 
        print("fast run");
    }
}

class Cat with Powerful, Fast{}
```

Mixin은 생성자가 없는 클래스를 다른 클래스에 포함시켜주는 개념이다. 그렇기 때문에 어떤 클래스에 새로운 속성이나 기능을 추가시키고 싶을 때, 또 그 기능이 다른 클래스들에서도 사용될 수 있을 때 유용하다. 사용은 class 정의 뒤에 with를 붙여주고 Mixin class를 붙여주면 된다.