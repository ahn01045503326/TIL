# Wrapper Class

기본 자료형(Primitive data type)에 대한 객체 표현을 Wrapper class라고 합니다.

기본 자료형 → Wrapper class로 변환하는 것을 Boxing이라 하며,

Wrapper class → 기본 자료형으로 변환하는 것을 UnBoxing이라 합니다.

---

### 래퍼 클래스란(Wrapper Class)?
````
자바의 자료형은 크게 기본 타입(primitive type)과 참조타입(reference type)으로 나누어진다.
대표적으로 기본 타입은 char, int, float, double, boolean 등이 있고 참조 타입은 class, interface 등이 있는데
프로그래밍을 하다 보면 기본 타입의 데이터를 객체로 표현해야 하는 경우가 종종 있다.
이럴 때에 기본 자료타입(primitive type)을 객체로 다루기 위해서 사용하는 클래스들을 래퍼 클래스(wrapper class)라고 한다.
자바는 모든 기본타입(primitive type) 값을 갖는 객체를 생성할 수 있다.
이런 객체를 포장 객체라고 하는데 그 이유는 기본 타입의 값을 내부에 두고 포장하기 때문이다.
래퍼 클래스로 감싸고 있는 기본 타입 값은 외부에서 변경할 수 없다. 만약 값을 변경하고 싶다면 새로운 포장 객체를 만들어야 한다.
````

### 래퍼 클래스 종류

| 기본 타입(primitive type) | 래퍼 클래스(wrapper class) |
|-----------------------|-----------------------|
| byte                  | Byte                  |
| char                  | Character}            |
| int                   | 	Integer              |
| float                 | 	Float                |
|double|	Double|
|boolean|	Boolean|
|long|	Long|
|short|	Short|

래퍼 클래스는 java.lang 패키지에 포함되어 있고, char타입과 int타입이 각각 Character와 Integer의 래퍼 클래스를 가지고 있고

나머지는 기본 타입의 첫 글자를 대문자로 바꾼 이름을 가지고 있다.

### primitive 자료형 - Wrapper 클래스 관계

| int	                                     | Integer                                           |
|------------------------------------------|---------------------------------------------------|
| primitive 자료형 (long, float, double ...)	 | Wrapper 클래스 (객체)                                  |
| 산술 연산이 가능하다.	                            | Unboxing을 하지 않으면 산술 연산이 불가능 하지만 null 값을 처리할 수 있다. |
| null로 초기화 할 수 없다.	                       | null 값 처리가 용이하기 때문에 SQL과 연동할 경우 처리가 용이함           |
|                                          | DB에서 자료형이 정수형이지만 null 값이 필요한 경우 Integer 사용 |

### 박싱(Boxing)과 언박싱(UnBoxing)
![박싱과 언박싱](boxing.png)
````
public class Wrapper_Ex {
    public static void main(String[] args)  {
        Integer num = new Integer(17); // 박싱
        int n = num.intValue(); //언박싱
        System.out.println(n);
    }
}
````

### Auto boxing / unboxing

자바에서는 모든 경우는 아니지만 대부분의 경우에 자동으로 boxing / unboxing을 해준다.

````
int i = 1;
Integer integer = i;		// int -> Integer ( Auto boxing )

int i2 = integer;		 // Integer -> int ( Auto unboxing )
````