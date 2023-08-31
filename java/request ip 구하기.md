# request IP

````
public static String getClientIP(HttpServletRequest request) {
    // WebServer, WAS, L4, proxy IP
    String ip = request.getHeader("X-Forwarded-For");
    String headerName = "X-Forwarded-For";
    if (bEmptyOrNull(ip) ||bEqualIgnoreCase(ip,"unknown") ) {
        ip = request.getHeader("Proxy-Client-IP");
        headerName = "Proxy-Client-IP";
    }
    if (bEmptyOrNull(ip) ||bEqualIgnoreCase(ip,"unknown") ) {
        ip = request.getHeader("WL-Proxy-Client-IP");
        headerName = "WL-Proxy-Client-IP";
    }
    if (bEmptyOrNull(ip) ||bEqualIgnoreCase(ip,"unknown") ) {
        ip = request.getHeader("HTTP_CLIENT_IP");
        headerName = "HTTP_CLIENT_IP";
    }
    if (bEmptyOrNull(ip) ||bEqualIgnoreCase(ip,"unknown") ) {
        ip = request.getHeader("HTTP_X_FORWARDED_FOR");
        headerName = "HTTP_X_FORWARDED_FOR";
    }
    if (bEmptyOrNull(ip) ||bEqualIgnoreCase(ip,"unknown") ) {
        ip = request.getRemoteAddr();
        headerName = "getRemoteAddr";
    }
    if(bExistsDataOnString(ip) ) {
log.info("Header-Name: {} , IPs: {}", headerName, ip);
        // X-Forwarded-For 헤더의 값들은 일반적으로 왼쪽에서 오른쪽으로 기록하며 클라이언트에서부터 서버까지의 전달 순서대로 기록된다.
        // X-Forwarded-For: ip-address-1, ip-address-2, client-ip-address, nginx-ip-address
        String[] ips = ip.split(",");
        ip = ips[0];
        if( ips.length > 4) {
            ip = ips[ips.length-3];
        }
    }
    return ip;
}
````

### AWS 환경에서 X-Forwarded-For 헤더를 통해 ip 가져오기

AWS에서 cloudfront, ALB에서 x-forward-for 헤더에 ip 추가

````
       ------------------Client---------------------  --------------------Server---------------------
PROD : ip-address-1, ip-address-2, client-ip-address, cloudfront-ip-add, ALB-ip-add, nginx-ip-address
STAGE : ip-address-1, ip-address-2, client-ip-address, ALB-ip-add, nginx-ip-address
````

