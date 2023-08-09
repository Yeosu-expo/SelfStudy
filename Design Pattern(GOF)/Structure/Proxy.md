# Proxy pattern
Client(프로그램에서 요청하는 주체)가 Service(요청을 처리하는 객체)에게 요청하는 흐름으로 프로그램은 돌아간다. 이때, Service단에서 추가적인 동작이 필요해지거나, 그 동작을 실험해봐야하는 경우가 있을 수도 있고, Client에서 Service에 직접 접근하는 것이 보안상으로 문제가 될 수도 있다. 혹은 많은 Client가 있어서 많은 요청이 들어왔을 때, Service에 과부하가 걸릴 수 도 있다. 이때 프록시 패턴을 활용한다.

>> 프록시 패턴은 Client와 Service사이에 존재한다. Proxy는 들어오는 요청을 Service에 보내기 전에 먼저 어떤 작업을 하거나, Service에 Client를 간접적으로 이어주는 역할이다.

구체적으로 Service에 추가기능이 필요한 경우 Serivce에 바로 코드를 수정하는 것이 아닌, Proxy에서 기능을 구현해서 Service 동작시 중간에 Proxy단에서 새로운 기능을 위해 한번 처리가 거쳐지고 Service로 가는 구조가 가능하다. 이러한 로직은 보안적인 이점도 있고, 들어오는 요청의 흐름을 관리할 수 있다는 점에서 특정상황에서는 유용하다.

## 예시 코드
```cpp
class Service{
    public:
        virtual void request() = 0;
};

class RealService:public Service{
    public:
        void request(){
            cout << "RealService request" << endl;
        }
};

class ProxyService:public Service{
    private:
        RealService *realService;
    public:
        ProxyService():realService(nullptr){}
        void request(){
            if(realService==nullptr)
                realService = newRealService();
            cout << "Here is Proxy Service and";
            realService->request();
        }
}

void Client(){
    RealService *real = new RealService();
    real->request();

    ProxyService *proxy = new ProxyService();
    proxy->request();
}

int main(){
    Client();

    return 0;
}
```