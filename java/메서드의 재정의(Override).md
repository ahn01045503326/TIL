# Override (메서드의 재정의)

---
````
public class Animal{
    pubic void eat(){
        System.out.println("?")
    }
}

public class Dog extends Animal{
    @override
    pubic void eat(){
        System.out.println("개처럼 먹다.")
    }
}

public class Cat extends Animal{
    @override
    pubic void eat(){
        System.out.println("고양이처럼 먹다.")
    }
}
````
#### 1. Override(재정의)
> 상속관계에서 하위클래스가 상위클래스의 동작을 재정의 하는 행위 (기능추가, 변경)