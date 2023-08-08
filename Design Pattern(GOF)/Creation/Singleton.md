# Singleton Pattern
>> 한 클래스에서 오직 하나의 인스턴스만을 생성되게 하는 디자인 패턴

## 코드
```c++
class Singleton{
    private:
        Singleton() {} // 생성자를 private으로 막아서 객체를 임의로 생성하는 것을 막음
        static Singleton* instance; // 전역범위에서는 접근 가능하지만, main이나 지역범위 안에서는 접근 불가
    public:
        static Singleton* getInstance(){
            if(instance != nullptr){ // 객체가 없다면 만들어서 주소 리턴
                return instance;
            }
            else{ // 이미 만들어진 객체가 있다면 해당 객체 주소 리턴
                instance = new Singleton();
                return instance;
            }
        }
};

Singleton* Singleton::instance = nullptr;

int main(){
    //Singleton obj(); // 생성자가 private로 막혀있음
    //Singleton* pobj = new Singleton(); // 이것도 생성자가 private로 막혀있어 불가능
    Singleton* obj = Singleton::getInstance();
    Singleton* obj2 = Singleton::getInstance();// obj와 같은 주소 값을 가지고 있음.

    return 0;
}
```

## 장단점
### 장점
* 단 하나의 객체만을 생성할 수 있기 때문에 여러 객체가 생기는 것을 막아 메모리를 줄일 수 있다
* 단 하나의 객체만 있기 때문에 다른 클래스에서 값을 참조할 때, 고민의 여지가 없다

### 단점
* 오직 하나의 객체만 존재하기 때문에 해당 클래스를 테스트 할 때, 기존의 객체를 초기화하고 진행해야 한다.
* 생성자가 private이기 때문에 자식클래스를 만들 수 없다.(자식클래스는 생성시 부모클래스 생성자를 자동으로 호출하기 때문)

>> 생각보다 단점이 꽤 있어서 많은 환경에서 쓰기에는 문제가 있다. 하지만, 장점이 너무 명확해서 특화된 상황에서는 강한 기능이다.