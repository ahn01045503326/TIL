# IP 주소 필터링

IpAddressMatcher는 객체 생성 시에 접근을 허용할 IP 또는 IP 대역을 넘기도록 되어있다.

````
String address = "120.52.22.96/27";
ip = "120.52.22.98"

// IpAddressMatcher 객체 생성
IpAddressMatcher matcher = new IpAddressMatcher(address);
// cloudfront 여부 확인
isCloudfront = matcher.matches(ip);
````