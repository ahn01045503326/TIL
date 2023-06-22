# REST API

REST를 기반으로 만들어진 API를 의미합니다.

````
URI의 종류
- URL (Uniform Resource Locator) : 자원의 위치(주소)로 자원을 식별한다.
- URN (Uniform Resource Name) : 자원에 이름을 붙여 식별한다.

모든 URI는 URL이다? X
→ URL은 URI의 한 종류이며 가장 흔한 형태이다. 다시 말하면 URI는 개념이고 URL은 개념을 구현한 하나의 형태
````
---

### 1. REST

REST(Representational State Transfer)의 약자로 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것을 의미합니다.

````
1. HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고,
2. HTTP Method(POST, GET, PUT, DELETE, PATCH 등)를 통해
3. 해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미합니다.
````

#### CRUD Operation이란

CRUD는 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능인 Create(생성), Read(읽기), Update(갱신), Delete(삭제)를 묶어서 일컫는 말로 REST에서의 CRUD Operation 동작 예시는 다음과 같다.

````
Create : 데이터 생성(POST)
Read : 데이터 조회(GET)
Update : 데이터 수정(PUT, PATCH)
Delete : 데이터 삭제(DELETE)
````

### 2. REST 구성 요소
````
자원(Resource) : HTTP URI
자원에 대한 행위(Verb) : HTTP Method
자원에 대한 행위의 내용 (Representations) : HTTP Message Pay Load
````

### 3. REST API 설계 예시
````
1. URI는 동사보다는 명사를, 대문자보다는 소문자를 사용하여야 한다.
  Bad Example http://khj93.com/Running/
  Good Example  http://khj93.com/run/

2. 마지막에 슬래시 (/)를 포함하지 않는다.
  Bad Example http://khj93.com/test/  
  Good Example  http://khj93.com/test

3. 언더바 대신 하이폰을 사용한다.
  Bad Example http://khj93.com/test_blog
  Good Example  http://khj93.com/test-blog

4. 파일확장자는 URI에 포함하지 않는다.
  Bad Example http://khj93.com/photo.jpg  
  Good Example  http://khj93.com/photo

5. 행위를 포함하지 않는다.
  Bad Example http://khj93.com/delete-post/1  
  Good Example  http://khj93.com/post/1  
````