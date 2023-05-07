# Upcasting과 Downcasting

---
````
------------ Upcasting --------------
Animal x = new Dog();
x.eat();

Animal x = new Cat();
------------ Downcasting --------------
Cat c = (Cat)x;
c.night();

((Cat)x).night();
````
#### 1. Upcasting (자동형변환)
> 하위클래스의 타입을 상위클래스의 타입으로 바꾸는 행위
#### 2. Downcasting(강제형변환)
> 상위클래스의 타입을 하위클래스의 타입으로 바꾸는 행위