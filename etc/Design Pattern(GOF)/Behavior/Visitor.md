# Vistor pattern
>> 클래스가 정의되어 있고 새로운 기능을 추가하고 싶을 때, 기존의 클래스를 수정하지 않고, 새로운 클래스를 만들어 추가 기능을 구현해 기존 클래스에서 호출하는 형식으로 기능을 확장하는 방법이다.

이를 활용하면, 컴포지트 패턴이나, 트리 같은 계층 구조에서 계층에 따라 어떤 vistor를 호출할 것인지를 정해서 기능을 조건별로 호출할 수 있다.

## 예시 코드
```cpp
class Vistor{
        public:
                virtual void visit(class ConcreteElementA* concreteElementA) = 0;
                virtual void visit(class ConcreteElementB* concreteElementB) = 0;
};

class Element{
        public:
                virtual void accept(Vistor* visitor) = 0;
};

class ConcreteElementA:public Element{
        public:
                string value;
                ConcreteElementA(string value){
                        this->value = value;
                }
                void accept(Vistor* visitor){
                        visitor->visit(this);
                }
};

class ConcreteElementB:public Element{
        public:
                string value;
                ConcreteElementB(string value){
                        this->value = value;
                }
                void accept(Vistor* visitor){
                        visitor->visit(this);
                }
};

class ConcreteVistor1:public Vistor{
        public:
                void visit(ConcreteElementA* concreteElementA){
                        cout << "ElementA visit ConcreteVistor1: " << concreteElementA->value << endl;
                }
                void visit(ConcreteElementB* concreteElementB){
                        cout << "ElementB visit ConcreteVistor1: " << concreteElementB->value << endl;
                }
};

class ConcreteVistor2:public Vistor{
        public:
                void visit(ConcreteElementA* concreteElementA){
                        cout << "ElementA visit ConcreteVistor2: " << concreteElementA->value << endl;
                }
                void visit(ConcreteElementB* concreteElementB){
                        cout << "ElementB visit ConcreteVistor2: " << concreteElementB->value << endl;
                }
};

void Client(){
        ConcreteElementA* elementA = new ConcreteElementA("elementA");
        ConcreteElementB* elementB = new ConcreteElementB("elementB");
        ConcreteVistor1* visitor1 = new ConcreteVistor1();
        ConcreteVistor2* visitor2 = new ConcreteVistor2();

        elementA->accept(visitor1);
        elementA->accept(visitor2);

        elementB->accept(visitor1);
        elementB->accept(visitor2);

        delete(elementA);
        delete(elementB);
        delete(visitor1);
        delete(visitor2);
}

int main(){
        Client();

        return 0;
}
```

tips
```cpp
class Vistor{
        public:
                virtual void visit(class ConcreteElementA* concreteElementA) = 0;
                virtual void visit(class ConcreteElementB* concreteElementB) = 0;
};
```
이 부분에서 Vistor클래스는 ConcreteElementA, B보다 먼저 선언되어 있다. 그래서 매개변수로 그냥 ConcreteElementA, B를 사용하면 정의되지 않아서 사용할 수 없다고 오류가 뜬다. 이때 매개변수 안에서 미리 선언하면 해결할 수 있다. 
virtual void visit(class ConcreteElementA* concreteElementA) = 0;
처럼 하면 된다.


### 실행 결과
ElementA visit ConcreteVistor1: elementA</br>
ElementA visit ConcreteVistor2: elementA</br>
ElementB visit ConcreteVistor1: elementB</br>
ElementB visit ConcreteVistor2: elementB</br>