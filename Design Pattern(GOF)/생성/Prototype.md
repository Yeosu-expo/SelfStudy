# Prototype  pattern
>> 일반적으로 어떤 객체에 수정을 하고 싶을 때, 원본에 바로 수정이나 추가를 하지않고, 복제본을 가지고 그것에 테스트를 해보게 된다. 이렇게 하면, 원본은 그대로 남게되서 변질의 우려가 없고, 수정과 추가, 삭제를 마음대로 해볼 수 있는 객체가 있기 때문에 이런 방법이 유리하다. 여기서 원본객체를 보존하고 같은 내용의 객체를 복제하는 것이 이 패턴이다.

## 예시 코드
```cpp
class Animal{
    public:
        virtual Animal* clone() = 0;
        virtual string getName() = 0;
};

class Dog: public Animal{
    private:
        string name;
    public:
        Dog(string name="no name"){this->name=name;}
        Dog(Dog &dog){this->name = dog->name;}
        Animal* clone(){
            return new Dog(*this);
        }
        string getName(){return this->name;}
};

class Cat: public Animal{
    private:
        string name;
    public:
        Cat(string name="no name"){this->name=name;}
        Cat(Cat &cat){this->name = cat->name;}
        Animal* clone(){
            return new Cat(*this);
        }
        string getName(){return this->name;}
};

int main(){
    Cat *cat = new Cat("navi");
    Dog *dog = new Dog("poppy");

    Animal *catClone = cat->clone();
    Animal *dogClone = dog->clone();

    cout << catClone->getName() << endl; // navi
    cout << dogClone->getName() << endl; // poppy

    return 0;
}
```