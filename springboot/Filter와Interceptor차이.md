# 필터(Filter)와 인터셉터(Interceptor)의 차이

### Request, Response 객체 조작 가능 여부

필터는 Request와 Response를 조작할 수 있지만, 인터셉터는 조작할 수 없다.

````
public class MyFilter implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
    throws IOException, ServletException {
        // 다른 request와 response를 넣어줄 수 있음
        chain.doFilter(request, response);
    }
}
````

필터가 다음 필터를 호출하기 위해서는 필터 체이닝(다음 필터 호출)을 해주어야 한다.

이때 request, response 객체를 넘겨주므로 우리가 원하는 request, response 객체를 넣어줄 수 있다.

하지만 인터셉터는 처리 과정이 필터와 다르다.

````
public class MyInterceptor implements HandlerInterceptor {

    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) 
    throws Exception {
        // Request, Response를 교체할 수 없고 boolean 값만 반환 가능
        return true;
    }
}
````

디스패처 서블릿이 여러 인터셉터 목록을 가지고 있고, 순차적으로 실행시킨다.

그리고 true를 반환하면 다음 인터셉터가 실행되거나 컨트롤러로 요청이 전달되며, false가 반환되면 요청이 중단된다.

그러므로 다른 request, response 객체를 넘겨줄 수 없다.

### 필터(Filter)와 인터셉터(Interceptor)의 사용 사례
````
필터(Filter)의 사용 사례

- 보안 및 인증/인가 관련 작업
- 모든 요청에 대한 로깅 또는 검사
- 이미지/데이터 압축 및 문자열 인코딩
- Spring과 분리되어야 하는 기능
- 필터는 기본적으로 스프링과 무관하게 전역적으로 처리해야 하는 작업들을 처리할 수 있다.
````

필터는 인터셉터보다 앞단에서 동작하기 때문에 보안 검사(XSS 방어 등)를 하여 올바른 요청이 아닐 경우 차단할 수 있다.
그러면 스프링 컨테이너까지 요청이 전달되지 못하고 차단되므로 안전성을 더욱 높일 수 있다.

또한, 필터는 이미지나 데이터의 압축, 문자열 인코딩과 같이 웹 어플리케이션에 전반적으로 사용되는 기능을 구현하기에 적당하다.

````
인터셉터(Interceptor)의 사용 사례

- 세부적인 보안 및 인증/인가 공통 작업
- API 호출에 대한 로깅 또는 검사
- Controller로 넘겨주는 정보(데이터)의 가공
- 인터셉터에서는 클라이언트의 요청과 관련되어 전역적으로 처리해야 하는 작업들을 처리할 수 있다.
````

대표적으로 세부적으로 적용해야 하는 인증이나 인가와 같이 예를 들어 특정 그룹의 사용자는 어떤 기능을 사용하지 못하는 경우가 있는데, 이러한 작업들은 컨트롤러로 넘어가기 전에 검사해야 하므로 인터셉터가 처리하기에 적합하다.

또한 인터셉터는 필터와 다르게 HttpServletRequest나 HttpServletResponse 등과 같은 객체를 제공받으므로 객체 자체를 조작할 수는 없다.
대신 해당 객체가 내부적으로 갖는 값은 조작할 수 있으므로 컨트롤러로 넘겨주기 위한 정보를 가공하기에 용이하다.

예를 들어 JWT 토큰 정보를 파싱해서 컨트롤러에게 사용자의 정보를 제공하도록 가공할 수 있는 것이다.
그 외에도 여러 목적으로 API 호출에 대한 정보들을 기록해야 하는 상황에 HttpServletRequest나 HttpServletResponse를 제공해주는 인터셉터는 클라이언트의 IP나 요청 정보들을 기록하기에 용이하다.

### 정리

![filter와interceptor](/image/filter와interceptor.png)

필터와 인터셉터 모두 비즈니스 로직과 분리되어 특정 요구사항(보안, 인증, 인코딩 등)을 만족시켜야 할 때 적용한다.

필터(Filter)는 특정 요청과 컨트롤러에 관계없이 전역적으로 처리해야 하는 작업이나 웹 어플리케이션에 전반적으로 사용되는 기능을 구현할 때 적용하고,

인터셉터(Interceptor)는 클라이언트의 요청과 관련된 작업에 대해 추가적인 요구사항을 만족해야 할 때 적용한다.