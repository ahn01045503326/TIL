# StringBuffer / StringBuilder 는 가변

StringBuffer나 StringBuilder의 경우 문자열 데이터를 다룬다는 점에서 String 객체와 같지만, 객체의 공간이 부족해지는 경우 버퍼의 크기를 유연하게 늘려주어 가변(mutable)적이라는 차이점이 있다.

두 클래스는 내부 Buffer(데이터를 임시로 저장하는 메모리)에 문자열을 저장해두고 그 안에서 추가, 수정, 삭제 작업을 할 수 있도록 설계되어 있다.

---

String 객체는 한번 생성되면 불변적인 특징 때문에 값을 업데이트하면, 매 연산 시마다 새로운 문자열을 가진 String 인스턴스가 생성되어 메모리공간을 차지하게 되지만,

StringBuffer / StringBuilder 는 가변성 가지기 때문에 .append() .delete() 등의 API를 이용하여 동일 객체내에서 문자열 크기를 변경하는 것이 가능하다.

![StringBuffer](StringBuffer.png)

따라서 값이 변경될 때마다 새롭게 객체를 만드는 String 보다 훨씬 빠르기 때문에, 문자열의 추가, 수정, 삭제가 빈번하게 발생할 경우라면 String 클래스가 아닌 StringBuffer / StringBuilder를 사용하는 것이 이상적이라 말할 수 있다.

- StringBuilder 나 StringBuffer 클래스의 사용 문법은 둘이 똑같다.
- 다만 내부적으로 동작 차이점 존재하는데 이에 대해선 바로 뒤에서 다룬다. 지금은 둘이 동일시로 봐도 된다.

StringBuffer의 내부구조를 보면 상수(final) 키워드가 없는것을 볼 수 있다.

````
public final class StringBuffer implements java.io.Serializable {
    private byte[] value;
}
````
````
StringBuffer sb = new StringBuffer(); // new StringBuffer() 인수에 아무것도 넣어주지 않으면 기본 16으로 배열 길이를 잡음

// sb.capacity() - StringBuffer 변수의 배열 용량의 크기 반환
System.out.println(sb.capacity()); // 16

sb.append("1111111111111111111111111111111111111111"); // 40길이의 문자열을 append
System.out.println(sb.capacity()); // 40 (추가된 문자열 길이만큼 늘어남)
````

아래 코드는 별* 문자를 루프문을 순회할때마다 추가해 길다란 별 문자열을 만드는 예제로, 각각 String 객체와 StringBuffer 객체를 이용했을시 차이를 보여준다.

````
String star = "*";

for ( int i = 1; i < 10; i++ ) {
star += "*";
}
````
````
StringBuffer sb= new StringBuffer("*");
sb.append("*********");
````
![StringBuffer2](StringBuffer2.png)

String 객체일 경우 매번 별 문자열이 업데이트 될때마다 계속해서 메모리 블럭이 추가되게 되고, 일회용으로 사용된 이 메모리들은 후에 Garbage Collector(GC)의 제거 대상이 되어 빈번하게 Minor GC를 일으켜 Full GC(Major Gc)를 일으킬수 있는 원인이 된다.

반면 StringBuffer는 위 사진 처럼 자체 메모리 블럭에서 늘이고 줄이고를 할수 있기 때문에 훨씬더 효율적으로 문자열 데이터를 다룰 수 있다는 것을 볼 수 있다.