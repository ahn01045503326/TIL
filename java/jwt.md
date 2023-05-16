# JWT(Json Web Token)
웹에서 사용되는 JSON 형식의 토큰에 대한 표준 규격인데요. 주로 사용자의 인증(authentication) 또는 인가(authorization) 정보를 서버와 클라이언트 간에 안전하게 주고 받기 위해서 사용됩니다.

JWT 토큰 웹에서 보통 Authorization HTTP 헤더를 Bearer <토큰>으로 설정하여 클라이언트에서 서버로 전송되며, 서버에서는 토큰에 포함되어 있는 서명(signature) 정보를 통해서 위변조 여부를 빠르게 검증할 수 있게 됩니다.

JWT 토큰은 Base64로 인코딩이 되어 있어서 육안으로 보면 eyJ로 시작하는 아주 긴 문자열인데요. 온라인 디버거를 통해서 어렵지 않게 실제로 저장되어 있는 내용을 JSON 형태로 디코딩하여 확인해볼 수 있습니다.

JWT 구조
하나의 JWT 토큰은 헤더(header)와 페이로드(payload), 서명(signature) 이렇게 세 부분으로 이루어지며 각 구역이 , 기호로 구분됩니다.

<헤더>.<페이로드>.<서명>
첫 번째 부분인 헤더(header)에는 토큰의 유형과 서명 알고리즘에 명시되고, 중간 부분인 페이로드(payload)에는 소위 claim이라고도 불리는 사용자의 인증/인가 정보가 담기는데요. 마지막 부분인 서명(signature)에는 헤더와 페이로드가 비밀키로 서명되어 저장됩니다.

JWT 토큰은 네트워크로 전송되야 하기 때문에 공간을 적게 차지하는 것이 유리한데요. 그래서 독특하게도 JSON 형식으로 데이터를 저장할 때 키(key)를 3글자로 줄이는 관행이 있습니다.

아래는 전형적인 JWT 토큰의 디코딩 결과입니다.

````
헤더
{
    "alg": "HS256",
    "typ": "JWT"
}
````
````
페이로드
{
    "sub": "1234567890",
    "lat": 1516239022
}
````
JWT에서 자주 사용되는 JSON 키 이름은 다음과 같습니다.

- sub 키: 인증 주체(subject)
- iss 키: 토큰 발급처
- typ 키: 토큰의 유형(type)
- alg 키: 서명 알고리즘(algorithm)
- iat 키: 발급 시각(issued at)
- exp 키: 말료 시작(expiration time)
- aud 키: 클라이언트(audience)

---
#### jwt 라이브러리 추가
````
[build.gradle]

implementation 'io.jsonwebtoken:jjwt-api:0.11.5'
runtimeOnly 'io.jsonwebtoken:jjwt-impl:0.11.5','io.jsonwebtoken:jjwt-jackson:0.11.5'
````

#### jwt 생성 및 복호화
````
[java]

import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.io.Encoders;
import io.jsonwebtoken.security.Keys;
import lombok.experimental.UtilityClass;
import java.security.Key;
import java.util.Date;

@UtilityClass
public class JwtToken {
    private Key key = Keys.secretKeyFor(SignatureAlgorithm.HS256);
    private int expiration = 216000;

    // JWT 생성
    public String createJwt(String subject) {
        String secretString = Encoders.BASE64.encode(key.getEncoded());
        System.out.println(secretString);
        String jws = Jwts.builder().setSubject(subject).setExpiration(new Date(System.currentTimeMillis()+expiration)).signWith(key).compact();
        System.out.println(jws);
        return jws;
    }

    // JWT 유효성 검증 및 JWT parsing
    public Boolean validationToken(String jwt) {
        // if jwt가 유효한지 체크 필요
        try {
            String subjectDecode = Jwts.parserBuilder().setSigningKey(key).build().parseClaimsJws(jwt).getBody().getSubject();
            Date expirationDecode = Jwts.parserBuilder().setSigningKey(key).build().parseClaimsJws(jwt).getBody().getExpiration();
            System.out.println("subject : " + subjectDecode);
            System.out.println("expirationDecode : " + expirationDecode);
        } catch (Exception e) {
            System.out.println("decodeJwt false : " + e);
            return false;
        }
        return true;
    }
}

````