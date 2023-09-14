# CORS(교차 출처 리소스 공유, Cross-Origin Resource Sharing)

CORS란 도메인이 서로다른 2개의 사이트가 데이터를 주고 받을 때 발생하는 문제입니다.

예를 들어 domain-a.com ↔ domain-b.com으로 데이터를 주고받을시 따로 설정 하지 않으면 CORS 에러를 만나게 됩니다.

※ 브라우저는 보안 상의 이유로, 스크립트에서 시작한 교차 출처 HTTP 요청을 제한한다.

따라서 다른 서버의 리소스를 불러오기 위해서는, 그 출처에서 CORS에 대한 내용을 Response의 헤더에 추가해줘야 합니다.

````
Access-Control-Allow-Orgin : 요청을 보내는 페이지의 출처 [ *, 도메인 ]
Access-Control-Allow-Methods : 요청을 허용하는 메소드. Default : GET, POST
Access-Control-Max-Age : 클라이언트에서 preflight 요청 (서버의 응답 가능여부에 대한 확인) 결과를 저장할 시간
Access-Control-Allow-Headers : 요청을 허용하는 헤더
````