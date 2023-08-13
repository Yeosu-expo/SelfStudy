# State pattern
만약 게임에서 한 플레이어의 상태를 나타낸다고 하면, 정상, 기절, 혼란, 배고픔, 아픔 등등 있을 것이다. 그리고 각 상태마다 정의 된 동작들과 상태들관의 상호작용이 있을 수도 있다. 이것을 플레이어 클래스에 모두 정의하면 새로운 상태를 추가할 때 모든 코드를 점검해봐야 한다. 이때 쓰는 패턴이다.

>> 스테이트 패턴은 객체의 상태를 추상화하여 하위 클래스로 상세한 상태를 구현하여, 객체가 상태를 필드로 가져 상태에 따라 다른 행위를 할 수 있게 해준다.

위의 예시에서는 상태라는 추상클래스가 있고, 하위 클래스로 정상, 기절, 혼란 등이 구현되어있다. 그리고 플레이어(Context)는 상태를 필드(멤버변수)로 갖는다. 이렇게 되면 상태에 따라 다른 행동을 할 수 있고, 새로운 상태를 가지더라도 수정이 편리하다.

스테이트 패턴은 추상클래스를 가지고 업캐스팅된 하위클래스에 따라 Context가 다른 행동을 취한다. 이는 Strategy 패턴과 유사하다. 둘의 차이점은 Strategy 패턴은 업캐스팅 된 하위 클래스에 따라 다른 행동을 취하고, 스테이트 패턴은 추상클래스를 필드로 가지는 Context의 **상태**에 따라 다른 행동을 취한다. 즉, 객체의 상태에 초점을 맞춘 것이다(스테이트 패턴은).

## 예시 코드
```cpp
class State{
        public:
                State* getInstance() { return nullptr; };
                virtual void heal() = 0;
                virtual void damage() = 0;
};

class NormalState:public State{
        static NormalState* normalState;
        NormalState() {}
        public:
                static State* getInstance(){
                        if(normalState == nullptr)
                                normalState = new NormalState();
                        return normalState;
                }
                void heal(){
                        cout << "Player is healed" << endl;
                }
                void damage(){
                        cout << "Player get damage" << endl;
                }
};

NormalState* NormalState::normalState =  nullptr;

class GoodState:public State{
        static GoodState* goodState;
        GoodState() {}
        public:
                static State* getInstance(){
                        if(goodState ==  nullptr)
                                goodState = new GoodState();
                        return goodState;
                }
                void heal(){
                        cout << "Player is too healthy" << endl;
                }
                void damage(){
                        cout << "Player get damage" << endl;
                }
};

GoodState* GoodState::goodState = nullptr;

class BadState:public State{
        static BadState* badState;
        BadState() {}
        public:
                static State* getInstance(){
                        if(badState == nullptr)
                                badState = new BadState();
                        return badState;
                }
                void heal(){
                        cout << "Player is healed" << endl;
                }
                void damage(){
                        cout << "Player can't get any worse" << endl;
                }
};

BadState* BadState::badState = nullptr;

class Player{
        State *state;

        public:
                Player(){
                        state = NormalState::getInstance();
                }
                void setState(State *state){
                        this->state = state; //this->state = state->getInstance()하면 세그폴트가 뜸 이유모름
                }
                void playerHeal(){
                        state->heal();
                        setState(GoodState::getInstance());
                }
                void playerGetDamege(){
                        state->damage();
                        setState(BadState::getInstance());
                }
};

void Client(){
        Player *player = new Player();

        player->playerHeal(); // Player is healed
        player->playerHeal(); // Player is too healthy
        player->playerGetDamege(); // Player get damage
        player->playerGetDamege(); // Player can't get any worse
}

int main(){
        Client();

        return 0;
}
```