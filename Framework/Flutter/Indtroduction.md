# Flutter
>>주로 IOS, Android의 모바일 플랫폼에서 운영체제의 종류와 상관없이 동작하는 프로그램을 만드는 프레임워크이다. 뿐만 아니라, 웹에서도 사용할 수 있다.

## 동작원리
##### 1. Framework
개발자가 Dart언어로 프레임워크에서 코딩을 하면, 프레임워크는 그 코드를 이해한다.
##### 2. Engine
프레임워크가 해석한 내용으로 C/C++로 작성된 라이브러리로 다시 코드를 해석한다.
##### 3. Platform
Engine에서 재해석된 코드를 OS에 내장된 runner라는 것으로 동작시킨다.

***
FLutter는 다른 프레임워크하고는 다른 동작방식을 가지고 있다. 일반적인 프레임워크는 코드를 통해 OS와 소통하면서, OS에 기본적으로 구현되어 있는 위젯으로 어플을 구체화한다. 하지만, Flutter는 Engine단계에서 C/C++로 작성된 코드로 다시 해석해서 그저 동작시키기만 하기 때문에, OS의 기능을 사용하지않는다. 그렇기 때문에 OS의 기본적인 위젯을 사용하지 못한다는 단점이 있지만, OS에 종류에 제한이 없기 때문에 화면의 모든 픽셀을 마음대로 사용할 수 있다.

[Flutter architectural-overview](https://docs.flutter.dev/resources/architectural-overview)

## 특징
1. OS의 UI에 국한되지 않기 때문에 자신 앱만의 고유한 UI를 구현할 수 있다.
2. OS에 의존하지 않기 때문에 모든 OS에서 동작할 수 있다.

### vs React Native
React는 js를 통해 OS와 소통해서 앱을 만든다.
따라서, OS에 맞는 UI를 디자인하고 싶다면 >> React
자신의 앱만의 고유한 UI를 구현하고 싶다면 >> Flutter