# Iterator pattern
>> 어떤 객체를 담는 객체의 집합체가 있고 그 집합체를 탐색할 때, 객체의 종류에 따라 맞는 검색방법을 구현하는 것이 아닌, 어떤 객체 집합체가 들어와도 검색할 수 있는 클래스를 만드는 패턴이다.

이렇게 하면, 객체 집합체마다 검색을 위한 구현을 생략할 수 있고, 캡슐화 되기 때문에 어떤 집합체인지 상관없이 모든 객체를 검색할 수 있다.

## 예시 코드
```java
public class IteratorInJava{
        public class Object{
                private String info;

                public Object(String info){
                        this.info = info;
                }

                public String getInfo(){
                        return info;
                }
        }

        public interface Colletion{
                public Iterator createIterator();
        }

        public class ObjectColletion implements Colletion{
                private Object[] objects;
                private int last = 0;

                public ObjectColletion(int size){
                        objects = new Object[size];
                }
                public Object getObject(int index){
                        return objects[index];
                }
                public int getLength(){
                        return last;
                }
                public void appendObject(Object object){
                        if(last < objects.length){
                                this.objects[last++] = object;
                        }
                        else{
                                System.out.println("Collection is fulled");
                        }
                }
                @Override
                        public Iterator createIterator(){
                                return new ObjectColletionIterator(this);
                        }
        }

        public class ObjectColletionIterator implements Iterator<Object>{
                private ObjectColletion objectColletion;
                private int index = 0;

                public ObjectColletionIterator(ObjectColletion objectColletion){
                        this.objectColletion = objectColletion;
                }
                @Override
                        public boolean hasNext(){
                                return index < objectColletion.getLength();
                        }
                @Override
                        public Object next(){
                                Object object = objectColletion.getObject(index++);
                                return object;
                        }
        }

        public static void main(String args[]){
                ObjectColletion objectColletion = new ObjectColletion(5);

                Object object1 = new Object("object1");
                Object object2 = new Object("object2");
                Object object3 = new Object("object3");
                Object object4 = new Object("object4");
                Object object5 = new Object("object5");

                objectColletion.appendObject(object1);
                objectColletion.appendObject(object2);
                objectColletion.appendObject(object3);
                objectColletion.appendObject(object4);
                objectColletion.appendObject(object5);

                Iterator iter = objectColletion.createIterator();
                while(iter.hasNext()){
                        Object object = (Object) iter.next();
                        System.out.println(Object.getInfo());
                }
        }
}
```

~~c++에는 Iterator클래스가 없어서 직접 구현해야함. 그래서 자바로 했는데 컴파일이 안됨. 근데 코드는 맞음. 컴파일 방법 알면 수정예정.~~