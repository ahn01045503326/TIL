# HTTP Session이란?

HTTP는 상태가 유지되지 않는 Stateless한 비접속형 프로토콜이다. 

그래서 서버는 클라이언트의 보통 이전 상태를 기억하기 위해서 세션이라는 개념을 사용한다. 

서버는 고유한 세션 ID(JSESSIONID)를 웹 브라우저에 쿠키로 전달하고 클라이언트는 서버에 요청시 해당 쿠키(JSESSIONID)를 함께 전달한다. 

서버는 전달받은 세션 ID를 서버에 이미 저장되어있는 정보와 비교해서 클라이언트의 상태를 지속적으로 유지하게 된다. 

스프링 컨트롤러단에서 HttpSession 매개변수를 전달하면 HttpSession 인터페이스를 구현한 StandardSession 클래스 객체를 가져올 수 있다.

````
서버가 해당 서버(웹)로 접근(request)한 클라이언트(사용자)를 식별하는 방법

- 서버(웹)는 접근한 클라이언트(사용자)에게 response-header filed인 set-cookie 값으로 클라이언트 식별자인 session-id(임의의 긴 문자열)를 발행(응답)한다.
- 서버로부터 발행(응답)된 session-id는 해당 서버(웹)와 클라이언트(브라우저) 메모리에 저장된다. 이 때 클라이언트 메모리에 사용되는 cookie 타입은 세션 종료 시 같이 소멸되는 "Memory cookie"가 사용된다.
- 서버로부터 발행된 session(데이터)을 통해 개인화(사용자)를 위한 데이터(userInfo 등..)로 활용할 수 있다.
````

### HTTP Session 동작 순서
````
1. 클라이언트(사용자)가 서버로 접속(http 요청)을 시도한다.
2. 서버(웹)는 접근한 클라이언트의 request-header field인 cookie를 확인해 클라이언트가 해당 session-id를 보내왔는지 확인한다.
3. 만약 클라이언트로부터 발송된 session-id가 없다면 서버는 session-id를 생성해 클라이언트에게 response-header field인 set-cookie 값으로 sesion-id(임의의 긴 문자열)를 발행(응답)한다.
````

### 각 브라우저 별 Session Life Circle
````
IE
- 새로운 탭 활성화시 - 첫 번째 요청 session-id 값과 동일
- 새로운 창 활성화시 - 새로운 session-id을 발급

Chorme
- Chrome 브라우저와 같은 경우 첫 번째 요청 시 다른 브라우저들의 결과와 달리 response-header의 set-cookie 값이 아닌 두 번째 요청의 결과와 같은 request-header의 cookie 값으로 session-id가 포함되어 있다.
- 새로운 탭 활성화시 - 첫 번째 요청 session-id 값과 동일
- 새로운 창 활성화시 - 첫 번째 요청 session-id 값과 동일

Firefox
- 새로운 탭 활성화시 - 첫 번째 요청 session-id 값과 동일
- 새로운 창 활성화시 - 첫 번째 요청 session-id 값과 동일

Safari
- 새로운 탭 활성화시 - 첫 번째 요청 session-id 값과 동일(Safari 브라우저의 경우 이전 브라우저들의 결과와 달리 request-header cookie 값으로 session-id가 포함 되지 않는다.)
- 새로운 창 활성화시 - 첫 번째 요청 session-id 값과 동일
````