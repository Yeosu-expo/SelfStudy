# Chain of Rsponsibility pattern
>> 객체에 어떤 명령이 들어오고, 이를 처리할 수 있는 객체들을 서로 연결하고 순서대로 명령을 받으며, 해당 명령을 수행할 수 있으면, 처리하고 없으면 다음 객체로 책임을 넘기는 클래스를 정의하는 패턴이다.

다시 설명하면, 어떤 복잡한 명령을 수행하기 위해, 조건에 따라 실행하던 과정을 위해 객체들간의 결합도를 증가시켰던 구조가 있었다. 그 구조에서 객체들 마다 처리할 수 있는 명령이 있고, 그 명령이 수행가능한 객체가 그 명령만 실행하며, 다음 객체로 전달되면서 조건이 충족하지 않으면 다음 객체로 넘기고 맞으면 요청을 처리하거나, 다음 객체로 넘길 수 있게 됨으로써, 결합도를 낮추고 객체지향 특징에 맞는 패턴이라고 할 수 있다.(결합도는 한 객체가 다른 객체에 얼마나 알고있는 정도이다.)

추가적으로, 객체들의 연결을 연결리스트 형태로 구현하게 되는데, 리스트 형태 뿐만 아니라, 트리로도 가능하고 혹은 어떤 어플리케이션의 특성에 따라 독자적인 연결 구조를 만들어도 된다. 

## 예시 코드
```cpp
enum Request{
        CASE_A,
        CASE_B,
        CASE_C,
};

class Handler{
        protected:
                Handler* nextHandler;
        public:
                void setNextHandler(Handler* handler){
                        this->nextHandler = handler;
                }
                virtual void handleRequest(Request request) = 0;
};

class ConcreteHandlerA:public Handler{
        public:
        void handleRequest(Request request){
                if(request == CASE_A){
                        cout << "CASE_A completed\n" << endl;
                }
                else{
                        cout << "CASE_A Failed" << endl;
                        nextHandler->handleRequest(request);
                }
        }
};

class ConcreteHandlerB:public Handler{
        public:
        void handleRequest(Request request){
                if(request == CASE_B){
                        cout << "CASE_B completed\n" << endl;
                }
                else{
                        cout << "CASE_B Failed" << endl;
                        nextHandler->handleRequest(request);
                }
        }
};

class ConcreteHandlerC:public Handler{
        public:
        void handleRequest(Request request){
                if(request == CASE_C){
                        cout << "CASE_C completed\n" << endl;
                }
                else{
                        cout << "CASE_C Failed" << endl;
                        nextHandler->handleRequest(request);
                }
        }
};

void Client(){
        Request request[3] = {CASE_A, CASE_B, CASE_C};

        ConcreteHandlerA *caseA = new ConcreteHandlerA();
        ConcreteHandlerB *caseB = new ConcreteHandlerB();
        ConcreteHandlerC *caseC = new ConcreteHandlerC();
        caseA->setNextHandler(caseB);
        caseB->setNextHandler(caseC);

        caseA->handleRequest(request[0]);
        caseA->handleRequest(request[1]);
        caseA->handleRequest(request[2]);
}

int main(){
        Client();

        return 0;
}
```
* Handler : 요청을 처리하는 객체들의 상위클래스. 즉, 연결된 객체들의 상위클래스.

### 실행 결과
CASE_A completed

CASE_A Failed</br>
CASE_B completed

CASE_A Failed</br>
CASE_B Failed</br>
CASE_C completed