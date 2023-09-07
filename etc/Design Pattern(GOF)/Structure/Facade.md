# Facade pattern
예시로 피시방에서 컴퓨터 게임을 한다고 하자. 그러면 
피시방에 입장한다 -> 컴퓨터 전원을 킨다 -> 게임을 실행시킨다 -> 로그인을 한다 -> 게임을 시작한다는 과정이 있다. 이를 객체로 나누면 피사방, 컴퓨터, 게임 3개 객체로 나뉘게 되고, 각 객체의 멤버함수를 호출시키고 하는 코드를 작성해야한다. 이렇게 되면 Client입장에서 피시방에서 컴퓨터 게임을 한다는 이 동작에 많은 객체와 많은 함수를 호출하는 복잡한 과정을 겪어야하고, 전체 동작에 순서가 존재하기 때문에 객체들끼리 의존성이 높다(피시방에 입장하지 않으면, 컴퓨터 전원을 킨다는 함수를 실행하는 것이 모순이기 때문에). 이러한 상황에서 파사드 패턴을 활용한다.

>> 파사드 패턴은 저수준 객체들의 동작들을 관리하는 통합된 객체를 만들어서 관리해주는 고수준 객체를 만드는 패턴이다.

따라서, 피시방에서 컴퓨터 게임을 한다는 동작 전반을 관리해주는 고수준 객체 Facade를 만들어서 Client는 Facade객체의 멤버함수만 호출해주면, 모든 동작을 Facade 안에서 관리해서 해결해주는 것이다.

## 예시 코드
```cpp
class PCRoom{
    public:
        ~PCRoom() { cout << "get out of PCRoom" << endl; }
        void enterPCRoom() { cout << "enter PCRoom" << endl; }
};

class Computer{
        public:
        ~Computer() { cout << "Turn off the Computer" << endl; }
        void turnOn() { cout << "Turn on the Computer" << endl; }
};

class GameProgram{
    string ID;
    public:
        ~GameProgram() { cout << ID << " logout"<< endl; }
        void login(string ID) {
            this->ID =  ID;
            cout << ID << " login" << endl;
        }
        void gaming(){
            cout << ID << " is gaming" << endl;
        }
};

class Facade{
    PCRoom *pcroom;
    Computer *computer;
    GameProgram *gameProgram;
    public:
        Facade(){
            pcroom = new PCRoom();
            computer = new Computer();
            gameProgram = new GameProgram();
        }
        ~Facade(){
            cout << endl;
            delete(gameProgram);
            delete(computer);
            delete(pcroom);
        }
        void DoGame(string ID){
            pcroom->enterPCRoom();
            computer->turnOn();
            gameProgram->login(ID);
            gameProgram->gaming();
        }
};

void Client(){
    Facade *facade = new Facade();
    facade->DoGame("아무개");

    delete(facade);
}

int main(){
    Client();

    return 0;
}
```