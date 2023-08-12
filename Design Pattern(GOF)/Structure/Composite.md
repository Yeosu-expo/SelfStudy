# Composite pattern
>> 단일 객체와 복합 객체를 하나의 단일 객체로 취급하여, 전체에서 부분으로 모두 접근할 수 있는 패턴이다.

풀어서 설명하면, 상위클래스 Component가 있고 하위클래스로 일반적인 단일객체 Leaf가 있고, 또 다른 하위클래스로 Composite가 있는데 이것은 Component의 리스트 형태 혹은 그룹형태의 객체이다. 즉, 단일객체Leaf와 다수의 객체가 저장될 수 있는 복합객체 Composite가 Component라는 상위클래스에 묶여있다고 할 수 있다. 

그래서 Composite의 원소로 Leaf(Component로 업캐스팅 된 것), Composite모두가 들어갈 수 있고, 그렇기 때문에 트리형태를 구현할 수 있다.

## 예시 코드
```cpp
class Component{
    public:
        virtual void fn() = 0;
};

class Leaf:public Component{
    public:
        void fn() { cout << "Leaf" << endl; }
};

class Composite:public Component{
    vector<Component*> vectorComponent;
    public:
        void fn(){
            cout << "Composite" << endl;
            for(vector<Component*::iterator iter=vectorComponent.begin();iter!=vectorComponent.end();iter++>)
                (*iter)->fn();
        }
        void add(Component *component) {
            vectorComponent.push_back(component);
        }
};

void Client(){
    Composite *Node1 = new Composite();
    Node1->add(new Leaf());
    Node1->add(new Leaf());

    Composite *Node2 = new Composite();
    Node2->add(new Leaf());
    Node2->add(new Leaf());
    Node2->add(new Leaf());

    Composite *Head = new Composite();
    Head->add(Node1);
    Head->add(Node2);

    Head->fn();
}

int main(){
    Client();

    return 0;
}
```
출력결과
Composite //Head
Composite //Node1
Leaf //Node1 Leaf
Leaf //Node1 Leaf
Composite //Node2
Leaf //Node2 Leaf
Leaf //Node2 Leaf
Leaf //Node2 Leaf