# String

기본적으로 자바에서는 String 객체의 값은 변경할 수 없다.

이는 한번 할당된 공간이 변하지 않는다고 해서 '불변(immutable)' 자료형 이라고 불리운다. 그래서 초기공간과 다른 값에 대한 연산에서 많은 시간과 자원을 사용하게 된다는 특징이 있다.

---

실제로 String 객체의 내부 구성 요소를 보면 다음과 같이 되어 있다.

인스턴스 생성 시 생성자의 매개변수로 입력받는 문자열은 이 value 라는 인스턴스 변수에 문자형 배열로 저장되게 된다. 이 value 라는 변수는 상수(final)형이니 값을 바꾸지 못하는 것이다.

````
public final class String implements java.io.Serializable, Comparable {
    private final byte[] value;
}
````

jdk 8 까지는 String 객체의 값은 char[] 배열로 구성되어져 있지만, jdk 9부터 기존 char[]에서 byte[]을 사용하여 String Compacting을 통한 성능 및 heap 공간 효율(2byte -> 1byte)을 높이도록 수정되었다.



아래 예제 코드를 보면 변수 a 가 참조하는 메모리의 "Hello" 라는 값에 "World" 라는 문자열을 더해서 String 객체의 자체의 값을 업데이트 시킨 것으로 보일수 있다.

하지만 실제로는 메모리에 새로 "Hello World" 값을 저장한 영역을 따로 만들고 변수 a 를 다시 참조하는 식으로 작동한다.

````
String str = "hello";
str = str + " world";

System.out.println(str); // hello world
````
![string](/image/string.png)

이외에도 문자열을 다루는데 있어 가장 많이 사용하는 trim 이나 toUpperCase 메소드 사용 형태를 보면, 문자열이 변경되는 것 처럼 생각 될 수도 있지만 해당 메소드 수행 시 또 다른 String 객체를 생성하여 리턴할 뿐이다.

````
String sql = "abc";  // "abc"
sql.toUpperCase();  // "ABC"

System.out.println(sql); // "abc" - toUpperCase를 해도 자체 문자열은 변경되지 않는다 (불변)
````

[ 자바 언어에서 String을 불변으로 설정한 이유 ]

String 객체를 불변하게 설계한 이유는 캐싱, 보안, 동기화, 성능측면 이점을 얻기 위해서이다.

1. 캐싱 : String을 불변하게 함으로써 String pool에 각 리터럴 문자열의 하나만 저장하며 다시 사용하거나 캐싱에 이용가능하며 이로 인해 힙 공간을 절약할 수 있다는 장점이 있다.

2. 보안 : 예를 들어 데이터베이스 사용자 이름, 암호는 데이터베이스 연결을 수신하기 위해 문자열로 전달되는데, 만일 번지수의 문자열 값이 변경이 가능하다면 해커가 참조 값을 변경하여 애플리케이션에 보안 문제를 일으킬 수 있다.

3. 동기화 : 불변함으로써 동시에 실행되는 여러 스레드에서 안정적이게 공유가 가능하다.