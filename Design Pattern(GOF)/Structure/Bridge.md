# Bridge pattern
만약 사각형과 동그라미 모양이 있고, 빨강과 파랑 색이 있다면, 이 조건들로 조합을 만들면 4개의 조합이 된다. 그리고 각각 다른 특성을 가진 객체이기 때문에 다른 클래스로 분류된다. 여기서 다른 모양이나 색이 추가가 된다면, 점점 클래스의 수가 기하급수적으로 많아진다. 이때 브릿지 패턴을 활용한다.

>> 브릿지 패턴은 OCP원칙에 따라 독립적으로 확장할 수 있게하기 위해 비슷한 그룹끼리 추상화 하고 추상화된 클래스를 다리를 놓는 것처럼 이어주는 방식의 디자인 패턴이다. 

앞의 예시에서 브릿지 패턴을 적용하면, color 클래스와 shape 클래스로 추상화클래스(인터페이스)를 만들고 각각 자식 클래스로 구체화한다. 예시의 경우 shape클래스의 자식클래스로 circle과 rentangle을 만들고, color클래스의 자식클래스로 red와 blue를 만들어서 구체화 한다. 그리고 shape클래스에서 color클래스를 멤버변수로 생성해서 두 인터페이스를 연결하는 방식이다. 

## 예시 코드
```cpp
class Color{ // interface
    public:
        virtual ~Color() {}
        virtual string printColor() const = 0;
};

class Red:public Color{
    public:
        string printColor() const override {
            return "Red color!\n";
        }
};

class Blue:public Color{
    public:
        string printColor() const override {
            return "Blue color!\n";
        }
};

class Shape{ // interface
    protected:
        Color* color_;

    public:
        Shape(Color* color) : color_(color){}
        virtual ~Shape() {}
        virtual string funcShape() const {
            return "Shape: Base Shape with" + color_->printColor();
        }
};

class Circle:public Shape{
    public:
        Circle(Color* color) : Shape(color){}
        string funcShape() const override {
             return "Shape: Circle Shape with " + color_->printColor();
        }
};

void ClientCode(const Shape& shape){
    cout << shape.funcShape();
}

int main(){
    Color* color = new Red;
    Shape* shape =  new Circle(color);
    ClientCode(*shape);
    cout << endl;

    return 0;
}
```

##### tips
```cpp
Shape(Color* color) : color_(color){}
```
이 부분의 의미는 color_라는 멤버 변수에 color라는 매개변수를 넣겠다는 뜻이다. 따라서
```cpp
Shape(Color* color){
    color_ = color;
}
```
와 같은 코드이다.