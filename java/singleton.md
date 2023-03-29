````
public class Singleton {
// Singleton 인스턴스 변수
private static Singleton instance = null;

// private 생성자
private Singleton() {}

// Singleton 인스턴스 반환 메소드
public static Singleton getInstance() {
if (instance == null) {
instance = new Singleton();
}
return instance;
}
}
````

Singleton 클래스가 하나의 인스턴스만 유지되도록 구현됩니다. 싱글톤 패턴에서는 클래스의 생성자가 private으로 선언되므로 다른 클래스에서는 이 클래스의 인스턴스를 생성할 수 없습니다.
getInstance() 메소드를 호출하면 Singleton 클래스의 인스턴스가 반환됩니다. 이 메소드는 먼저 instance 변수를 확인하여 null인 경우에만 인스턴스를 생성합니다. 