# 상수 만들기
---

#### Java에서 상수(Constant)를 만들려면 final 키워드를 사용합니다. final 키워드는 변수에 할당된 값을 변경할 수 없도록 합니다.
````
public class Constants {
    public static final int MAX_SIZE = 100;
    public static final String NAME = "John Doe";
}
````
- 위 코드에서 MAX_SIZE와 NAME은 final 키워드를 사용하여 상수(Constant)로 선언되었습니다. 
- MAX_SIZE는 int 타입으로 선언되었으며, NAME은 String 타입으로 선언되었습니다. 
- 이렇게 선언된 상수(Constant)는 다음과 같이 사용할 수 있습니다.

````
int size = Constants.MAX_SIZE;
String name = Constants.NAME;
````
