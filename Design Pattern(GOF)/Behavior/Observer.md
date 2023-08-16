# Observer pattern
>> 어떤 객체에서 이벤트가 발생했을 때, 그것을 감지하는 옵저버 객체가 그 반응을 감지하게하는 패턴이다.

이렇게 되면, 그 어떤 객체에서 일어나는 이벤트를 감지하기 위해 1초,1분,1시간 단위로 체크할 필요가 없어지게 된다. 이벤트가 일어나는 즉시, 옵저버에게 알려지는 구조인 것이다.

구조는 객체에서 이벤트를 감지할 옵저버 혹은 옵저버들을 객체 혹은 리스트형태로 보관하게 되며, 객체가 이벤트를 발생시킬 때마다 보관중인 옵저버에게 이 사실을 알리고, 옵저버가 들어온 정보로 반응을 하는 구조이다.

## 예시 코드
```cpp
class Observer{
        public:
                virtual void update() = 0;
};

class ConcreteObserverA:public Observer{
        public:
                void update() { cout << "ObserverA Update" << endl; }
};

class ConcreteObserverB:public Observer{
        public:
                void update() { cout << "ObserverB Update" << endl; }
};

class Object{
        protected:
                list<Observer*> observerList;
        public:
                void attach(Observer* observer){
                        observerList.push_back(observer);
                }
                void detach(Observer* observer){
                        observerList.remove(observer);
                }
                void notify(){
                        list<Observer*>::iterator iter;
                        for(iter=observerList.begin();iter!=observerList.end();iter++){
                                (*iter)->update();
                        }
                }
};

class ConcreteObjectA:public Object{
        public:
                void eventA(){
                        cout << "EventA occur int ConcreteObjectA" << endl;
                        notify();
                }
                void eventB(){
                        cout << "EventB occur int ConcreteObjectA" << endl;
                        notify();
                }
};

void Client(){
        ConcreteObjectA* obj =  new ConcreteObjectA();
        ConcreteObserverA* observerA = new ConcreteObserverA();
        ConcreteObserverB* observerB = new ConcreteObserverB();

        obj->attach(observerA);
        obj->attach(observerB);
        obj->eventA();

        obj->detach(observerA);
        obj->eventB();

        delete(observerA);
        delete(observerB);
        delete(obj);
}

int main(){
        Client();

        return 0;
}
```

### 실행 결과
EventA occur int ConcreteObjectA</br>
ObserverA Update</br>
ObserverB Update</br>
EventB occur int ConcreteObjectA</br>
ObserverB Update</br>
