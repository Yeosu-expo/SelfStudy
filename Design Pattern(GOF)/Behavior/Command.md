# Command pattern
예시로 버튼이 있고 버튼을 누르면 전등에 불이켜지거나, 미사일이 발사될 수 있다. 이를 코드로 나타내면, 버튼 클래스가 있고, 전등클래스, 미사일클래스가 버튼클래스에 필드로 있어, 함수를 호출하는 방식을 커쳐야할 것이다. 이런구조는 OCP원칙에 위배된다. 왜냐하면, 여기서 새로운 동작을 위해 라디오클래스를 추가시키면, 버튼클래스를 직접 수정해야하는 일이 발생하기 때문이다.

>> 커맨드 패턴은 OCP원칙을 위해 객체 끼리 의존성으로 묶여서 동작하는 형태에서 객체와 객체 사이에 커맨드라는 클래스를 추가시켜 커맨드가 두 객체를 이어주고 두 객체는 서로 의존성을 낮출 수 있게 한다. 그럼으로 실제 기능의 사용을 커맨드라는 클래스로 묶어 관리하게 된다.

위의 예시에 적용시키면, 버튼클래스가 전등,미사일클래스에 직접 기능을 사용하는 것이 아니라, 중간에 커맨드 클래스가 기능을 사용한다. 즉, 커맨드 클래스의 하위클래스로 전등커맨드클래스, 미사일커맨드클래스를 만들고, 버튼클래스에서 커맨드클래스를 실행시키기만 하면, 어떤 커맨드클래스인지에 따라 동작하게 되는 것이다. 그럼으로써, 라디오클래스가 추가되면, 라디오커맨드클래스만 생성하면, 버튼클래스는 수정없이 사용할 수 있다. 죽, OCP원칙을 지키게 되는 것이다.

## 예시 코드
```cpp
class Command{
        public:
                virtual void execute() = 0;
};

class Button{
        Command *command;
        public:
                void setCommand(Command* command){
                        this->command = command;
                }
                void press(){
                        command->execute();
                }
};

class Missile{
        public:
                void launch(){
                        cout << "Missile fired" << endl;
                }
};

class Radio{
        public:
                void play(){
                        cout << "Radio play" << endl;
                }
};

class RadioCommand:public Command{
        Radio* radio;
        public:
                RadioCommand(Radio* radio){
                        this->radio=radio;
                }
                void execute(){
                        radio->play();
                }
};

class MissileCommand:public Command{
        Missile* missile;
        public:
                MissileCommand(Missile* missile){
                        this->missile = missile;
                }
                void execute(){
                        missile->launch();
                }
};

void Client(){
        Radio *radio = new Radio();
        RadioCommand* RC = new RadioCommand(radio);
        Missile* missile = new Missile();
        MissileCommand* MS = new MissileCommand(missile);

        Button button;
        button.setCommand(RC);
        button.press(); // Radio play

        button.setCommand(MS);
        button.press(); // Missile fired
}

int main(){
        Client();

        return 0;
}
```