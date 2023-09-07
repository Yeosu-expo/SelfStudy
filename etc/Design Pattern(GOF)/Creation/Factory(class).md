# Factory (Method) pattern
>> 클래스 단위에서의 디자인 패턴으로 OCP원칙을 따르며, 객체의 생성과 활용에 대한 책임을 서브클래스로 전가하기 위한 디자인 패턴. 즉, 유지보수 측면에서 용이함.

## 예시코드
```cpp
class Foodfactory{
    public:
        virtual Foodfactory makefood(){
            return new Foodfactory;
        }
};

class Pizza: public Foodfactory{
    public:
        virtual Foodfactory makefood(){
            printf("Here your Pizza!");
            return new Pizza;
        }
};

class Chicken: public Foodfactory{
    public:
        virtual Foodfactory makefood(){
            printf("Here your Chicken!");
            return new Chicken;
        }
};

```