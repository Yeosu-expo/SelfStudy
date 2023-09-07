# Mediator pattern
>> 객체들의 다대다 관계에서 중재자 클래스가 객체들의 관계를 중재해서 중재자와 각 객체로의 관계. 즉, 1:N (중재자:객체들)의 관계를 형성해서 복잡도를 낮추고 확장성을 늘리며, 캡슐화를 적용하는 패턴

자세히 설명하면, 각 객체들은 중재자클래스를 필드로 갖고, 객체에 이벤트가 생기면 중재자에게 알리고 중재자는 다른 객체들에게 이 이벤트를 전달하는 방식이다. 

여기서 이벤트가 객체에 일어나고 알린다는 점에서 옵저버 패턴과 유사하지만 옵저버 패턴은 이벤트를 감지하는데서 그치지만, 중재자 패턴은 다대다 관계에서 이벤트를 객체끼리 공유하게 중재한다는 점에서 다르다.

## 예시 코드
```cpp
class Mediator{
        public:
                virtual void receiveEvent(string event) = 0;
                virtual void sendEventToColleague(string event) = 0;
};

class Colleague{
        protected:
                string name;
                string event;
                Mediator *mediator;
        public:
                Colleague(string name){
                        this->name = name;
                }
                void setMediator(Mediator *mediator){
                        this->mediator = mediator;
                }
                void sendEvent(){
                        mediator->receiveEvent(event);
                }
                void eventing(string event){
                        this->event = event;
                        sendEvent();
                }
                virtual void recieve(string present) = 0;
};

class ConcreteColleagueA:public Colleague{
        public:
                ConcreteColleagueA(string name):Colleague(name){}
                void recieve(string present){
                        cout << name << "(ConcreteColleagueA)" << " recieve " << present << endl;
                }
};

class ConcreteColleagueB:public Colleague{
        public:
                ConcreteColleagueB(string name):Colleague(name){}
                void recieve(string present){
                        cout << name << "(ConcreteColleagueB)" << " recieve " << present << endl;
                }
};

class ConcreteColleagueC:public Colleague{
        public:
                ConcreteColleagueC(string name):Colleague(name){}
                void recieve(string present){
                        cout << name << "(ConcreteColleagueB)" << " recieve " << present << endl;
                }
};

class ConcreteMediator:public Mediator{
        private:
                string name;
                string event;
                list<Colleague*> colleagueList;
        public:
                ConcreteMediator(string nameValue):name(nameValue){}
                void addColleague(Colleague* colleague){
                        colleagueList.push_back(colleague);
                }
                void sendEventToColleague(string event){
                        list<Colleague*>::iterator iter;
                        for(iter=colleagueList.begin();iter!=colleagueList.end();iter++)
                                (*iter)->recieve(event);
                }
                void receiveEvent(string event){
                        this->event = event;
                        sendEventToColleague(event);
                }
};

void Client(){
        ConcreteMediator* mediator = new ConcreteMediator("mediator1");

        ConcreteColleagueA* colleagueA = new ConcreteColleagueA("colleagueA");
        ConcreteColleagueB* colleagueB = new ConcreteColleagueB("colleagueB");
        ConcreteColleagueC* colleagueC = new ConcreteColleagueC("colleagueC");

        colleagueA->setMediator(mediator);
        colleagueB->setMediator(mediator);
        colleagueC->setMediator(mediator);

        mediator->addColleague(colleagueA);
        mediator->addColleague(colleagueB);
        mediator->addColleague(colleagueC);

        colleagueA->eventing("event in colleagueA");
}

int main(){
        Client();

        return 0;
}
```
### 실행 결과
colleagueA(ConcreteColleagueA) recieve event in colleagueA</br>
colleagueB(ConcreteColleagueB) recieve event in colleagueA</br>
colleagueC(ConcreteColleagueB) recieve event in colleagueA</br>

***
이 코드에서는 이벤트가 발생된 곳에서도 중재자한테서 이벤트 알람을 받고 있다. 이것을 수정하면 더 좋을 듯.