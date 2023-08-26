# MDC(Mapped Diagnostic Context)

현재 실행중인 쓰레드에 메타 정보를 넣고 관리하는 공간

멀티 클라이언트 환경에서 다른 클라이언트와 값을 구별하여 로그를 추적할 수 있도록 제공되는 map

ThreadLocal을 통해 구별할 수 있는 키 값을 저장하여 Thread가 살아있는 동안 해당 키값 활용

---

### MDC 필터 구현 및 로그 남기기

스프링에서 MDC에 uuid를 만들어 넣을만한 곳은 필터, 인터셉터 등이 있는데 가장 앞단인 필터에 적용하는 것이 좋다. 그리고 필터들 중에서도 가장 먼저 등록되도록 해주면 좋다. 이러한 필터를 구현하면 다음과 같다.

````
@Component
@Order(Ordered.HIGHEST_PRECEDENCE)
class MDCLoggingFilter implements Filter {

    @Override
    public void doFilter(final ServletRequest servletRequest, final ServletResponse servletResponse, final FilterChain filterChain) throws IOException, ServletException {
        final UUID uuid = UUID.randomUUID();
        MDC.put("request_id", uuid.toString());
        filterChain.doFilter(servletRequest, servletResponse);
        MDC.clear();
    }
}
````

여기서 주의할 점은 doFilter가 끝나서 나오면 clear를 해준다는 것이다. 