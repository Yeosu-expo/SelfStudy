# Abstract Factory Pattern(추상 팩토리 패턴)
예시를 들어 설명하면, 삼성컴퓨터와 LG컴퓨터를 만든다고 했을 때, 컴퓨터에는 모니터, 본체, 마우스, 키보드로 구성된다고 하면 각 컴퓨터는 삼성컴퓨터이면 삼성구성품으로 구성되어 있고, LG컴퓨터이면, LG구성품으로 구성되어 있을 것이다. 여기서 마우스만 본다면, 삼성마우스와 LG마우스가 있다. 이때, 팩토리 패턴으로 마우스를 관리하는 팩토리를 만들 수 있을 것이다. 근데 이 예시에서만 구성품이 4개이고, 그러면 팩토리만 4개를 더 만들어 줘야한다. 이를 좀 더 관리하기 쉽게 각 구성품의 팩토리를 만들지 않고, 컴퓨터만 팩토리를 만들어서 삼성컴퓨터이면 삼성구성품을 생성하게 하는 것이다. 즉, 각 구성품의 팩토리를 만들어서 관리하는 것이 아니라, 구성품 전체를 관리하는 컴퓨터팩토리 하나로 관리하는 것이다.

예시를 보기전에 추상화의 개념을 잡고가야한다.
일반적인 상속은 상위클래스의 내용을 하위클래스에 계승하는 방식이라면, 추상화에서는 상위클래스는 객체의 정의만하고 구체적인 정의나 생성, 동작등의 구현은 하위클래스에서 한다.
참고로, 함수 뒤에 =0이 붙으면 함수의 구현이 없고, 하위클래스에서 구현하다는 것을 명시적으로 나타낸 것이다. 즉, 해당 클래스는 추상화클래스라는 것을 의미한다.

## 예시 코드
이번 예시에서는 구성품은 마우스와 모니터만 해보겠습니다.
```cpp
class Mouse{};

class SamsungMouse: public Mouse{
    public:
        SamsungMouse(){
            cout << "Create Samsung Mouse" << endl;
        }
};

class LGMouse: public Mouse{
    public:
        LGMouse(){
            cout << "Create LG Mouse" << endl;
        }
};

class Monitor{};

class SamsungMonitor: public Monitor{
    public:
        SamsungMonitor(){
            cout << "Create Samsung Monitor" << endl;
        }
};

class LGMonitor: public Monitor{
    public:
        LGMonitor(){
            cout << "Creat LG Monitor" << endl;
        }
};

class ComputerFactory{
    public:
        virtual Mouse createMouse() = 0;
        virtual Monitor createMonitor() = 0;
};

class SamsungComputerFactory: public ComputerFactory{
    public:
        virtual Mouse createMouse(){
            return new SamsungMouse();
        }
        virtual Monitor createMonitor(){
            return new SamsungMonitor();
        }
};

class LGComputerFactory: public ComputerFactory{
    public:
        virtual Mouse createMouse(){
            return new LGMouse();
        }
        virtual Monitor createMonitor(){
            return new LGMonitor();
        }
};

class SlecterOfComputerFactory{ // 어떤 컴퓨터 팩토리를 사용할 것인지 string값으로 정하는 클래스
    public:
        void createComputer(string type){
            ComputerFactory CF = NULL;
            
            switch(type){
                case Samsung:
                    CF = new SamsungComputerFactory();
                    break;
                case LG:
                    CF = new LGComputerFactory();
                    break;
                default:
                    cout << "Unkown type." << endl;
                    return;
            }

            CF.createMouse();
            CF.createMonitor();
        }
};

int main(){
    SlecterOfComputerFactory s = new SlecterOfComputerFactory();
    s.createComputer(Samsung);

    return 0;
}
```
### 장단점
하나의 팩토리에서 관리하기 때문에 관리하기 편하지만, 새로운 객체를 추가할 때, 모든 클래스에 변경을 필요로한다.
