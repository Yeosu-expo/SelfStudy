# Template Method pattern (class)
>> 어떤 동작을 하는 알고리즘이 있고 그것을 수행하는 함수가 상위클래스에 있을 때, 그 함수의 핵심 로직은 그대로 두고 핵심 로직의 구체적인 구현은 하위클래스에서 하게 한다. 그럼으로써, 알고리즘의 핵심로직은 변하지 않고, 구체적인 동작만 하위클래스마다 다르게 수행하게 되는 패턴이다. 

결국 상위클래스의 수정없이 하위클래스의 확장이나 수정만으로 알고리즘을 때에 맞게 변화하여 쓸 수 있는 것이다. 즉, OCP원칙에 알맞다.

## 예시 코드
```cpp
class AbstractClass{
        public:
                virtual void concreteMethod1() = 0;
                virtual void concreteMethod2() = 0;
                void method(){
                        concreteMethod1();
                        concreteMethod2();
                }
};

class SubClassA:public AbstractClass{
        public:
                void concreteMethod1(){
                        cout << "ConcreteMethod1 in SubA" << endl;
                }
                void concreteMethod2(){
                        cout << "ConcreteMethod2 in SubA" << endl;
                }
};

class SubClassB:public AbstractClass{
        public:
                void concreteMethod1(){
                        cout << "ConcreteMethod1 in SubB" << endl;
                }
                void concreteMethod2(){
                        cout << "ConcreteMethod2 in SubB" << endl;
                }
};

void Client(){
        SubClassA subA;
        subA.method();

        cout << endl;

        SubClassB subB;
        subB.method();
}

int main(){
        Client();

        return 0;
}
```

## 실행 결과
ConcreteMethod1 in SubA</br>
ConcreteMethod2 in SubA</br>
</br>
ConcreteMethod1 in SubB</br>
ConcreteMethod2 in SubB</br>