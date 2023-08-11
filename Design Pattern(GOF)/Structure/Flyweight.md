# Flyweight pattern
예시로 교실을 구성한다고 했을 때, 매우 큰 교실이어서 책상이 100개가 필요하다고 하자. 책상의 속성으로는 브랜드, 원재료, 책상의 x,y좌표가 있을 것이다. 그런데 이런 책상 인스턴스를 100개나 구성한다고 하면, 브랜드, 원재료는 같은 값을 공유하고 있을 것이다. 그러면 브랜드, 원재료 값의 크기의 x 99만큼 메모리가 낭비될 것이다. 이것을 해결하기 위해서 플라이웨이트 패턴을 활용한다.

>> 플라이웨이트(경량급) 패턴은 반복되는 객체 중 중복되는 값과 중복되지 않는 값을 분류해서 어떤 객체의 값이 이전에 객체의 중복되는 값과 일치하다면 그 값만 참조해서 추가적은 메모리를 사용하지 않게 하기 위함이다.

따라서 반복되는 객체 중에 중복되는 값만을 구성하는 model을 만들고 중복되지 않는 값만을 구성하는 class에 field(class 안의 멤버변수로 활용한다는 뜻)로 사용해서, 객체 생성시 factory에서 이전에 사용된 값과 일치하다면 그 값을 반환해주고 아니라면 새로만들고 그 내용을 저장하고 그 값을 반환해주는 형식이다.(중복되는 값을 공유한다는 큰 틀만 맞으면 다르게 구성해도 괜찮다.)

## 예시 코드
```cpp
class TableModel{
    string brand;
    string material;

    public:
        TableModel(string brand, string material){
            this->brand = brand;
            this->material = material;
        }
        string getBrand() { return brand; }
        string getMaterial() { return material; }
};

class Table{
    TableModel *tableModel;
    int x;
    int y;

    public:
        Table(TableModel *tableModel, int x, int y){
            this->tableModel = tableModel;
            this->x = x;
            this->y = y;
        }
        string getBrand() { return tableModel->TableModel::getBrand(); }
        int getX() { return this->x; }
        int getY() { return this->y; }
};

class TableFactory{
    map<string,TableModel* > tableValue;

    public:
        TableModel* getTableModel(string tableModelValue){
            if(tableValue.find(tableModelValue) != tableValue.end()){
                return tableValue.find(tableModelValue)->second;
            }
            else{
                istringstream ss(tableModelValue);
                string tmp1;
                string tmp2;
                getline(ss, tmp1,':');
                getline(ss, tmp2,':');
                TableModel *tmpModel = new TableModel(tmtmp2);
                tableValue.insert({tableModelValue, tmpModel});
                return tmpModel;
            }
        }
};

void printTable(Table *table){
    cout << table->getBrand() << endl;
    cout << table->getX() << ", " << table->getY() << endl;
}

void Client(){
    TableFactory *tf = new TableFactory();
    Table *t1 = new Table(tf->getTableModel("HiMart:Wood"), 10, 20);
    Table *t2 = new Table(tf->getTableModel("HiMart:Wood"), 20, 20);
    Table *t3 = new Table(tf->getTableModel("HuMart:Wood"), 30, 20);
    printTable(t1);
    printTable(t2);
    printTable(t3);
}

int main(){
    Client();

    return 0;
}
```