# HTTP (Hypertext Transfer Protocol)
서버와 클라이언트가 인터넷 상에서 데이터를 주고받기 위한 프로토콜
````
서버-클라이언트 모델 
- 클라이언트가 서버에게 요청을 보내면, 서버가 요청을 처리해 클라이언트에게 응답을 보낸다.

무상태 (Stateless) 프로토콜
- 각각의 요청을 독립적으로 처리한다. 
- 클라이언트는 요청을 보내기 전에 서버와 연결하는 과정이 필요하다. 
- 요청에 대한 응답이 이뤄지면 연결은 유지되지 않는다. → 상태 유지가 필요한 경우 쿠키나 세션 등을 이용하여 상태를 저장한다.
````
![HTTP](/image/http.png)

---

### 1. HTTP Request Method (요청의 종류)
````
GET : 자원의 전송을 요청
- URI에서 PATH 뒤에 query string으로 데이터 전달 → 데이터가 URL에 노출
- 데이터는 키와 벨류의 쌍으로 전달하고 각각은 &로 구분 ex) id=abc&name=mango
- 인코딩/디코딩 과정이 없음
- URI의 길이 제약으로 큰 데이터 전송은 어려움

POST : 자원의 생성을 요청
- URL에 해당하는 자원을 생성 요청
- 데이터는 HTTP BODY에 담아서 전달

PUT : 자원의 수정을 요청
- URI에 지정한 자원이 없는 경우 새로 생성한다.

PATCH : 자원의 일부를 수정 요청

DELETE : 자원의 삭제를 요청
````

### 2. HTTP Response Status Code 응답 상태 코드
````
서버는 클라이언트의 요청에 대한 처리 결과를 응답 메시지에 담아 전송한다.


1XX - Information (정보 전송)

2XX - Success (성공)
  200 : OK
  201 : Created
  202 : Accepted
  204 : No content (요청은 성공했지만 응답할 데이터가 없는 경우)

3XX - Redirection (리다이렉션)

4XX - Client Error (클라이언트 요청 에러)
  400 : Bad Request (문법 상의 오류로 서버가 요청을 이해하지 못함)
  404 : Not found (요청한 문서를 찾지 못한 경우)
  405 : Method not allowed

5XX - Server Error (서버 에러)
  500 : Internal server error
````