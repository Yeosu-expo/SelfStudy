# Memento pattern
>> 객체(Originator)의 정보를 Memento라는 클래스에 담고 이 메멘토를 CareTaker라는 클래스가 관리하면서 실제 객체의 상태는 변화하지만 특정 조건이나 요구에 따라 메멘토에 담긴 객체정보를 불러와서 객체의 상태를 복원하거나 확인할 수 있게하는 패턴이다.

구현방법은 Originator에서 메멘토를 필요할 때마다 생성해 정보를 저장하고 이 생성된 메멘토를 CareTaker클래스를 통해 저장한다. CareTaker함수는 내부적으로 리스트나 맵을 필드로 가지고 있고 그곳에 메멘토를 저장한다. 그리고 필요에 따라 컨테이너에 담긴 메멘토 정보를 반환해준다.

## 예시 코드
```cpp
class Memento{
        private:
                string info;
        public:
                Memento(string info_):info(info_){}
                string getInfo(){ return info; }
                void printInfo(){
                        cout << "Memento Info:" << info << endl;
                }
};

class Originator{
        private:
                string info;
        public:
                Originator(string info_):info(info_){}
                void setInfo(string info){
                        this->info=info;
                }
                void printInfo(){
                        cout << "Originator Info:" << info << endl;
                }
                Memento* makeAndGetMemento(){
                        return new Memento(info);
                }
};

class CareTaker{
        private:
                list<Memento*> mementoList;
        public:
                void appendMemento(Memento* memento){
                        mementoList.push_back(memento);
                }
                Memento* getMemento(Memento* target){
                        list<Memento*>::iterator iter;
                        iter = find(mementoList.begin(), mementoList.end(), target);
                        return *iter;
                }
};

void Client(){
        Originator* originator = new Originator("CASE A");
        CareTaker careTaker;

        Memento* memento1 = originator->makeAndGetMemento();
        originator->setInfo("CASE B");
        Memento* memento2 = originator->makeAndGetMemento();
        originator->setInfo("CASE C");
        Memento* memento3 = originator->makeAndGetMemento();

        careTaker.appendMemento(memento1);
        careTaker.appendMemento(memento2);
        careTaker.appendMemento(memento3);

        originator->printInfo();
        Memento* tmp;
        tmp = careTaker.getMemento(memento1);
        tmp->printInfo();
        tmp = careTaker.getMemento(memento2);
        tmp->printInfo();
        tmp = careTaker.getMemento(memento3);
        tmp->printInfo();
}

int main(){
        Client();

        return 0;
}
```

## 실행 결과
Originator Info:CASE C</br>
Memento Info:CASE A</br>
Memento Info:CASE B</br>
Memento Info:CASE C</br>