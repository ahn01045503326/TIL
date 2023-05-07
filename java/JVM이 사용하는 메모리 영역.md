# JVM이 사용하는 메모리 영역

---
#### 1. Method Area (static, none static)
> 메서드의 바이트코드(기계어 코드)가 할당되는 공간
> static-zone과 none-static-zone으로 나누어진다.
> static 멤버들은 static-zone에 할당
#### 2. Heap Area
> 객체가 생성되는 메모리 공간 (new 연산자)
> GC(garbage collector)에 의해서 메모리가 수집된다.
#### 3. Stack Area (call Stack Frame Area) , PC register Native Method Area
> 메서드가 호출되면 메서드의 기계어코드를 할당 받고(Native Method Area) 메서드가 실행되는 메모리 공간 (지역변수, 매개변수들이 만들어지는 공간)
> PC(Program Counter)에 의해서 현재 실행중인 프로그램의 위치가 관리된다.
> LIFO구조로 운영이 되는 메모리 공간 (메서드의 호출 순서를 알 수 있다.)
#### 4. Runtime Constant Pool (Literal Pool)
> 상수 값 할당이 되는 메모리 공간
> 문자열 중 문자열 상수(Literal : 리터럴)가 할당 되는 메모리 공간