#  try-with-resources

try-with-resources는 try-catch-finally의 문제점을 보완하기 위해 나온 개념입니다.
try( ... ) 안에 자원 객체를 전달하면, try블록이 끝나고 자동으로 자원 해제 해주는 기능을 말합니다.
따로 finally 구문이나 모든 catch 구문에 종료 처리를 하지 않아도 되는 장점이 있습니다.

자바에서  외부 자원에 접근하는 경우 주의해야할 점은 외부자원을 사용한 뒤 제대로 자원을 닫아줘야 한다.

자원을 닫을 때 try - catch - finally 구문 대신 try - with - resources 구문을 사용하면 코드의 가독성이 더 증가한다.

---

### try-catch-finally로 자원 해제
1. try-catch-finally 구문으로 자원을 해제하려면 코드가 길어지고 지저분하다.
2. 아래는 try-catch-finally을 사용한 자원해제의 예제 코드이다.

        FileOutputStream out = null;
        try {
            out = new FileOutputStream("exFile.txt");
            // ... 이후 입출력 로직 처리 ...
        }catch (FileNotFoundException e) {
            e.printStackTrace();
        }finally {
            if(out != null) { //스트림이 null인지 체크
                try {
                    out.close();
                }catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }


### try-with-resources로 자원 쉽게 해제

1. Java 7에서 try - with - resources 구문이 추가되었다.
2. try - with - resources를 사용하기 위해서는 close메소드를 정의하기 위한 AutoCloseable 인터페이스를 구현해야 한다.
3. 위에서 기존의 입출력 처리시의 예외처리는 다음과 같이 바뀌어 사용된다.
4. 아래의 코드는 try-with-resources 를 사용하여 자원을 쉽게 해제하는 예제이다. 실행결과는 위의 예제와 동일하다.

        try(FileOutputStream out = new FileOutputStream("exFile.txt")) {
            // ...이후 입출력 로직 처리...
        }catch (IOException e) {
            e.printStackTrace();
        }

5. try - with - resources 는 위의 코드와 같이 try(. . .)에 자원 객체를 전달하면, try 코드 블록이 끝나고 자동으로 자원을 해제해주는 기능이다.
6. 즉, 따로 finally 구문이나 모든 catch 구문에 종료 처리를 하지 않아도 된다.


이 때, try에 전달할 수 있는 자원은 AutoCloseable 인터페이스의 구현체로 한정된다.

AutoCloseable은 JDK 1.7부터 추가된 인터페이스다.
````
/**
 * @author Josh Bloch
 * @since 1.7
 */
  public interface AutoCloseable {
    void close() throws Exception;
  }
````

아래와 같이 try( ) 안에 복수의 자원 객체를 전달할 수 있다.

````
try(Something1 s1 = new Something1();
Something2 s2 = new Something2()) {

} catch(...) {
...
}
````