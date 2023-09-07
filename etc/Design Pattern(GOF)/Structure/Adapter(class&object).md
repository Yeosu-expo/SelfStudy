# Adpater pattern
>> 서로 다른 종류의 객체 A,B가 있을 때, A의 기능을 B는 사용할 수 없다. 그때, 어댑터 패턴을 활용하면 B가 A의 기능을 쓸 수 있게 변환 해준다.(정확히는 확장, 추가, 수정같은 것이다.)

## 예시 코드 (object)
```cpp
class Animal{
    public:
        void walk() {cout << "Animal is walking" << endl;}
};

class Fish{
    public:
        void swim() {cout << "Fish is swiming" << endl;}
};

class FishApater: public Animal{
    Fish fish;
    
    public:
        FishAdpater(Fish fish){
            this->fish=fish;
        }
        void walk() {fish.swim();}
};

int main(){
    Animal animal;
    Fish fish;

    animal.walk(); // "Animal is walking"
    fish.walk(); // error!
    
    FishAdpater *fishAdapter =  new FishAdapter(fish);
    fishAdapter.walk(); // "Fish is swiming"

    return 0;
}

```

## 클래스 어댑터
오브젝트 애댑터 패턴에서 어댑터 클래스가 Animal과 Fish 모두 상속받아서 오버라이드해서 기능을 연결 시켜준다.