# 모든 Request Header 값 가져오기

클라이언트 자체에 대한 자세한 정보를 DB에 저장하기 위해서 사용.

````
// 진입전
var req = new ContentCachingRequestWrapper((HttpServletRequest) request);
var res = new ContentCachingResponseWrapper((HttpServletResponse) response);

chain.doFilter(req, res);

Enumeration eHeader = req.getHeaderNames();
while (eHeader.hasMoreElements()) {
    String name = (String) eHeader.nextElement();
    String value = req.getHeader(name);
    log.info("header : {}, value : {}", name, value);
}
````