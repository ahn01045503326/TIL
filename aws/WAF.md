# AWS WAF (Web Application Firewall)

AWS 환경에서 발생하는 Layer 7 에 해당하는 보안 위협 (DDoS 공격 또는 웹 애플리케이션 공격) 에 대응하기 위한 보안 서비스이다. 배포할 수 있는 리소스는 다음과 같다.
- CloudFront
- Application LoadBalancer
- API Gateway 또는 AWS AppSync

---

### AWS WAF 기능
````
웹 트래픽 필터링 : IP 주소, HTTP 헤더 및 본문 또는 사용자 정의 URI와 같은 조건을 기준으로 웹 트래픽 필터링
AWS WAF Bot Control (옵션, 유료) : 일반적인 봇 트래픽을 제어하고 가시성을 확보
AWS WAF Fraud Control (옵션, 유료) : 애플리케이션의 로그인 페이지에서 손상된 자격 증명을 사용하여 사용자 계정에 대한 무단 액세스 모니터링
AWS Firewall Manager와 통합 : 여러 AWS 게정에 배포된 WAF를 중앙에서 구성 및 관리 가능
실시간 가시성 : IP 주소, 지리적 위치, URI, 사용자 에이전트 및 참조자에 관한 세부 정보를 포함하는 원시 요청을 캡처하고 실시간 지표를 제공
````

![waf.png](/image/waf.png)