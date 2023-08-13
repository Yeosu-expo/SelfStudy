# Strategy pattern
>> 자주 사용하는 패턴으로 OCP원칙을 따른다. 이 패턴은 어떤 함수가 동작할 때, 정해진 대로 동작하는 것이 아닌, 런타임 즉, 실행 시점에서 어떤 행동을 할 것인지 정해져서 동작하도록 하는 패턴이다.

자세히 말하면, 상위클래스(혹은 추상클래스)를 필드로 정의된 함수가 있고, 업캐스팅된 객체에 따라 다른 오버라이딩된 함수가 호출되게 하는 시스템이다.

## 예시 코드
```cpp
class Strategy{
        public:
                virtual void printSelf() = 0;
};

class ConcreteStrategyA:public Strategy{
        public:
                void printSelf() { cout << "Here is A" << endl; }
};

class ConcreteStrategyB:public Strategy{
        public:
                void printSelf() { cout << "Here is B" << endl; }
};

class ConcreteStrategyC:public Strategy{
        public:
                void printSelf() { cout << "Here is C" << endl; }
};

void printFunc(Strategy *strategy){
        strategy->printSelf();
}

void Client(){
        printFunc(new ConcreteStrategyA()); // Here is A
        printFunc(new ConcreteStrategyB()); // Here is B
        printFunc(new ConcreteStrategyC()); // Here is C
}

int main(){
        Client();

        return 0;
}
```