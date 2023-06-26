# Spring Data JPA (Java Persistent API)

![JPA](/image/JPA.png)

---

### 1. JDBC (Java DataBase Connectivity)

자바언어로 데이터베이스 프로그래밍을 하기위한 라이브러리

````
String jdbcDriver = "com.mysql.cj.jdbc.Driver";
String jdbcUrl = "jdbc:mysql://localhost:3306/user?serverTimezone=Asia/Seoul";
    try {
        Class.forName(jdbcDriver).newInstance();
        Connection con = DriverManager.getConnection(jdbcUrl, "root", "root123!@#");
        Statement st = con.createStatement();
        
        String sql = "SELECT * FROM user";
        ResultSet rs = st.executeQuery(sql);
        
        while(rs.next()){
            String name = rs.getString(1);
            String age = rs.getString(2);
            String email = rs.getString(3);
            System.out.println(name + " " + age + " " + email);
        }
        
        rs.close();
        st.close();
        con.close();
        
    } catch (Exception e) {
        e.printStackTrace();
    }
````

### 2. Hibernate
Hibernate는 JPA를 구현한 구현체이다.

````
JPA의 핵심들인 EntityManagerFactory, EntityManager, EntityTransaction 등을 상속받아 구현한다.

JPA를 구현하는 다른 구현체들로는 EclipseLink나 DataNucleus 등이 있다.

만약 JPA를 구현하는 구현체들이 마음에 들지 않는다면 개발자가 직접 JPA 구현체를 만들어 사용할 수도 있다.

Hibernate는 내부적으로 JDBC를 이용해 관계형 데이터베이스와 커넥션을 맺고 상호작용한다.
````

### 3. JPA
자바 ORM(Object Relational Mapping) 기술에 대한 인터페이스

ORM이란 객체와 관계형 데이터 베이스를 매핑해 주는 기술

````
JPA는 라이브러리가 아닌 ORM을 사용하기 위한 인터페이스의 모음이다.

이러한 JPA는 인터페이스의 모음, 단순한 명세이기 때문에 구현이 없다. 

자바 애플리케이션에서 관계형 데이터베이스를 어떻게 사용할지 정의하는 하나의 방법일 뿐이다.

따라서 이러한 JPA의 구현체 있어야 JPA를 사용할 수 있다.
````

### 4. Spring Data JPA
Spring Data JPA는 JPA를 사용하기 편하도록 만들어놓은 모듈이다. 

````
Spring Data JPA는 JPA를 한 단계 더 추상화시킨 Repository 인터페이스를 제공한다. 

이러한 Spring Data JPA는 Hibernate와 같은 JPA구현체를 사용해서 JPA를 사용하게 된다. 

Spring Data JPA를 사용하면 사용자는 더욱 간단하게 데이터 접근이 가능해진다. 
````
### 5. appication.yml
````
spring:
  jpa:
    show-sql: true
    properties:
      hibernate:
        format_sql: true
        dialect: org.hibernate.dialect.MySQL8Dialect
    hibernate:
      ddl-auto: validate
  datasource:
    url: jdbc:mysql://localhost:3306/user?useSSL=false&useUnicode=true&allowPublicKeyRetrieval=true
    driver-class-name: com.mysql.cj.jdbc.Driver
    username: username
    password: password
````

### 정리
````
JPA는 자바 진영의 ORM 기술에 대한 API 표준 명세이며

Hibernate는 JPA의 구현체이고, 내부적으로 JDBC를 이용한다.

Spring Data JPA는 JPA를 사용하기 쉽게 스프링에서 제공하는 모듈로 내부적으로 JPA 구현체를 이용한다.
````
 

 