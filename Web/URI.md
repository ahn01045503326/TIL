# URI (Uniform Resource Identifier) - 통합 자원 식별자
자원을 구분하고 접근하기 위해 사용하는 유일한 식별자.
````
URI의 종류
- URL (Uniform Resource Locator) : 자원의 위치(주소)로 자원을 식별한다.
- URN (Uniform Resource Name) : 자원에 이름을 붙여 식별한다.

모든 URI는 URL이다? X
→ URL은 URI의 한 종류이며 가장 흔한 형태이다. 다시 말하면 URI는 개념이고 URL은 개념을 구현한 하나의 형태
````
---

### 1. URL 구조
** 쿼리 스트링은 제외한 패스 부분까지가 URL이라는 관점이 있는데 뒤에 파라미터까지 전달해야 자원을 정확히 식별할 수 있기 때문에 쿼리 스트링을 포함한 전체가 URL에 해당한다.
![URL](/image/url.png)

````
scheme (protocol)
- 브라우저가 사용할 프로토콜. 대개 HTTP나 HTTPS

host
- 요청이 도달할 서버를 나타낸다. 
- 일반적으로 도메인 네임을 사용하지만 IP address를 직접 사용할 수도 있다.

port
- 서버에서 프로그램(서비스)이 사용하는 소켓을 구분. http는 80, https 443

path
- 서버에서 자원의 경로

query string
- 서버에 전달할 파라미터. 
- key=value 쌍으로 표기하고 복수 개의 경우 &로 구분한다.

fragment
- html 요소의 id를 가르켜 해당 지점으로 스크롤을 이동한다.
````
