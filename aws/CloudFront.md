# CloudFront

AWS에서 제공하는 CDN 서비스 입니다.

캐싱을 통해 사용자에게 좀 더 빠른 전송 속도를 제공함을 목적으로 합니다. 

CloudFront는 전 세계 이곳저곳에 Edge Server(Location)을 두고 Client에 가장 가까운 Edge Server를 찾아 Latency를 최소화시켜 빠른 데이터를 제공합니다.

- Origin Server : 원본 데이터를 가지고 있는 서버입니다. 보통 AWS에서의 Origin Server는 S3, Ec2 instance입니다.
- Edge Server = Edge Location : AWS에서 실질적으로 제공하는 전 세계에 퍼져있는 서버입니다. Edge Server에는 요청받은 데이터에 대해서 같은 요청에 대해서 빠르게 응답해주기 위해 Cache 기능을 제공합니다.

![cloudfront.png](/image/Fcloudfront.png)

---

### 데이터 전송이 발생하는 과정은 어떻게 될까요?
1. 클라이언트로부터 Edge Server로의 요청이 발생한다.
2. Edge Server는 요청이 발생한 데이터에 대하여 캐싱 여부를 확인합니다.
3. 사용자의 근거리에 위치한 Edge Server 중 캐싱 데이터가 존재한다면 사용자의 요청에 맞는 데이터를 응답합니다.
4. 사용자의 요청에 적합한 데이터가 캐싱되어 있지 않은 경우 Origin Server로 요청이 포워딩됩니다.
5. 요청받은 데이터에 대해 Origin Server에서 획득한 후  Edge Server에 캐싱 데이터를 생성하고, 클라이언트로 응답이 발생합니다.


### CloudFront에서는 어떤 종류의 콘텐츠를 CDN으로 제공해 주나요?
- Downlad Distribution : HTTP 프로토콜을 이용해서 다운로드할 수 있는 일반적인 이미지 혹은 정적 파일을 제공받을 수 있습니다.
- Streaming Distribution : 스트리밍을 위해 사용할 수 있는  HTTP Proressive DownLoad 방식이나 RTSP(Real Time Streaming Protocol)을 지원하는 동영상 콘텐츠를 서비스받을 수 있습니다.


### Edge Server의 Cache는 무슨 특징이 있나요?
- 기본적으로 한번 발생한 요청에 대해서는 Edge Server에 캐싱된 상태로 저장됩니다.
- Edge Server의 기본 TTL은 24시간이고 사용자의 설정에 따라 변경이 가능합니다. (TTL 수정 시 Edge Server에 반영되는 시간이 한 시간 가량 소요됩니다.)
- 이러한 캐시의 설정 후 반영 시간 때문에 전체 데이터에 대한 TTL을 수정하는 게 아닌 각 개별 데이터에 대해서 invalidation API(특정 파일을 캐시에서 삭제하는 기능)을 통해 삭제할 수 있습니다.
- Invalidation API는 동시에 최대 3개의 요청을 발생시킬 수 있으며, 각 요청은 최대 1000개까지 가능합니다.
- Invalidation API는 Edge Node에 반영되기까지 5~10분 정도의 시간이 소요됩니다.