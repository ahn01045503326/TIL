# ResponseEntity

---

- ResponseEntity는 HTTP 응답을 나타내는 Spring의 클래스입니다. 
- 이 클래스는 HTTP 응답 코드, 헤더 및 본문을 포함합니다. 
- ResponseEntity를 사용하여 컨트롤러에서 메서드 실행 결과를 클라이언트에게 전송할 수 있습니다.
---

#### 1. ResponseEntity 생성자
````
ResponseEntity(T body, HttpStatus status)
````
- body : HTTP 응답 본문에 포함될 객체
- status : HTTP 응답 상태 코드

#### 2. example Code
````
String message = "Hello, world!";
return new ResponseEntity<>(message, HttpStatus.OK);
````

````
MyObject myObject = new MyObject();
return new ResponseEntity<>(myObject, HttpStatus.OK);
````

````
HttpHeaders headers = new HttpHeaders();
headers.add("Custom-Header", "header-value");
return new ResponseEntity<>(message, headers, HttpStatus.OK);
````

````
String errorMessage = "Error message";
return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(errorMessage);
````