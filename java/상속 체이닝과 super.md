# 상속 체이닝과 super

---
````
public class Object{

}

public class Animal extends Object{
    public Animal(){
        super();    // new Object()
    }
}

public class Dog extends Animal{
    public Dog(){
        super();    // new Animal()
    }
}
````
#### 1. 상속 체이닝 (나보다 부모가 먼저야)
> 맨 위 부모클래스부터 객체가 생성되어 자식까지 연결되는 구조
#### 2. super()
> 상위 클래스의 생성자를 호출하는 메서드 <br>
> 생성자 메서드에서 가장 첫 문장에 사용해야 한다. <br>
> 상위 클래스의 기본생성자를 호출하는 super()는 생략되어 있다.