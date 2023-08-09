# Decorator pattern
예시로 고양이라는 상위클래스가 있다고 하자. 여기서 새로운 특징을 넣은 자식 클래스를 만든다고 하면, 줄무니가 있는 고양이, 얼룩무니가 있는 고양이, 검은 고양이, 혹은 줄무니가 있고 얼룩무니가 있는 고양이 등 특징의 가짓수나 그 특징의 조합에 따라 무수히 많은 자식클래스가 생기게 된다. 이를 해결하기 위해 데코레이터 패턴을 활용한다.

>> 데코레이터 패턴은 어떤 클래스 A의 확장을 위해 새로운 Decorator클래스를 만들고 이 두 클래스를 한 곳에 묶을 상위 클래스를 만든다. 그리고 Deocorator클래스를 자식클래스로 확장시켜 구체적인 특징을 구현해서 A클래스와 엮어서 사용한다. 여기서 A클래스와 Decorator클래스가 공통된 상위클래스가 있어 두 클래스의 조합을 편하게 한다.

## 예시 코드
```cpp
class Cat{
    public:
        virtual void descCat() = 0;
};

class MyCat:public Cat{
    public:
        void descCat(){
            cout << "MyCat: ";
        }
};

class DecoratorCat:public Cat{
    Cat *cat;
    public:
        DecoratorCat(Cat *cat) { this->cat = cat; }
        void descCat(){
            cat->descCat();
        }
        virtual void descDeco() = 0;
};

class BlackCat:public DecoratorCat{
    private:
        void descDeco(){
            cout << "Black ";
        }
    public:
        BlackCat(Cat *cat):DecoratorCat(cat){}
        void descCat(){
            DecoratorCat::descCat();
            this->descDeco();
        }
};

class SpottedCat:public DecoratorCat{
    private:
        void descDeco(){
            cout << "Spotted ";
        }
    public:
        SpottedCat(Cat *cat):DecoratorCat(cat){}
        void descCat(){
            DecoratorCat::descCat();
            this->descDeco();
        }
};

void Client(){
    // MyCat: Black
    Cat *blackCat = new BlackCat(new MyCat());
    blackCat->descCat();
    cout << endl;

    //MyCat: Spotted Black
    Cat *blackSpottedCat = new BlackCat(new SpottedCa(new MyCat()));
    blackSpottedCat->descCat();
    cout << endl;
}

int main(){
    Client();

    return 0;
}
```

Client에서 첫번째는 BlackCat 데코레이터만 엮은 MyCat이고, 두번째는 BlackCat, SpottedCat을 MyCat에 엮은 것이다.
이렇게 확장할 것을 데코레이터 클래스로 Concrete하고 MyCat에 원하는 만큼 조합해서 활용할 수 있다. 이 모든 것이 상위클래스 Cat으로 묶여있기 때문에 원하는 만큼 조합이 가능한 것이다.

##### 참고
* Componet : Cat
* ConcreteComponet : MyCat
* Decorator : DecoratorCat
* ConcreteDecoratorA : BlackCat
* ConcreteDecoratorB : SpottedCat