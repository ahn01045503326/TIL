# Spring Framework

자바 엔터프라이즈 개발을 위한 "오픈소스" 애플리케이션 프레임워크

---

### Spring Framework 특징
````
1. IoC(Inversion of Control, 제어 반전)
개발자는 JAVA 코딩시 new 연산자, 인터페이스 호출, 데이터 클래스 호출 방식으로 객체를 생성, 소멸시킨다.
여기서 IoC란 객체의 생성부터 소멸까지 개발자가 아닌 스프링컨테이너가 대신 해주는 것이다
제어권이 개발자가 아닌 IoC에 있으며, IoC가 개발자의 코드를 호출해 필요한 객체를 생성, 소멸 하며 생명주기를 관리하는 것이다.

2. DI(Dependency Injection, 의존성 주입)
프로그램에서 구성 요소의 의존 관계가 소스코드 내부가 아닌 외부의 설정 파일을 통해 정의 되는 방식이다.
코드 간의 재사용을 높이고, 소스코드를 다양한 곳에 사용하며 모듈 간의 결합도를 낮출 수 있다.
대표적으로 라이브러리나 API, 프레임워크를 연동 할 때 연결하는 소스코드를 직접 작성하는게 아닌
외부 파일을 연결해 불러오는 방식이다.

3. AOP(Aspect Object Programming, 관점 지향 프로그래밍)
로깅, 트랜잭션, 보안 등 여러 모듈에서 공통적으로 사용하는 기능을 분리하여 관리 할 수 있다.
각각의 클래스가 있다고 가정하자. 각 클래스들은 서로 코드와 기능들이 중복되는 부분이 많다. 코드가 중복될 경우 실용성과 가독성 및 개발 속도에 좋지 않다. 중복된 코드를 최대한 배제하는 방법은 중복되는 기능들을 전부 빼놓은 뒤 그 기능이 필요할때만 호출하여 쓰면 훨씬 효율성이 좋다.
즉, AOP는 여러 객체에 공통으로 적용할 수 있는 기능을 구분함으로써 재사용성을 높여주는 프로그래밍 기법이다.

4. POJO(Plain Old Java Object) 방식
POJO는 Java EE를 사용하면서 해당 플랫폼에 종속되어 있는 무거운 객체들을 만드는 것에 반발하여 나타난 용어이다.
별도의 프레임 워크 없이 Java EE를 사용할 때에 비해 인터페이스를 직접 구현하거나 상속받을 필요가 없어 기존 라이브러리를 지원하기 용이하고, 객체가 가볍다.
즉, getter/setter를 가진 단순한 자바 오브젝트를 말한다.
````