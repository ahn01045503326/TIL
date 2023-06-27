# 필터(Filter)

필터는 말 그대로 요청과 응답을 거른뒤 정제하는 역할을 한다.

Dispatcher Servlet에 요청이 전달되기 전 / 후에 url 패턴에 맞는 모든 요청에 대해 부가 작업을 처리할 수 있는 기능을 제공한다.

즉, 스프링 컨테이너가 아닌 톰캣과 같은 웹 컨테이너에 의해 관리가 되는 것이고, 스프링 범위 밖에서 처리되는 것이다.
(스프링 빈으로 등록 가능)

![filter](/image/filter.png)

---

### 필터(Filter)의 메소드 종류

필터를 사용하기 위해서는 javax.servlet의 Filter 인터페이스를 구현(implements) 해야 하며, 다음과 같은 메소드를 가진다.

````
public interface Filter {

    public default void init(FilterConfig filterConfig) throws ServletException {}
 
    public void doFilter(ServletRequest request, ServletResponse response,
            FilterChain chain) throws IOException, ServletException;
 
    public default void destroy() {}
````

init()
- 필터 객체를 초기화하고 서비스에 추가하기 위한 메소드이다.
- 웹 컨테이너가 1회 init()을 호출하여 필터 객체를 초기화하면 이후 요청들은 doFilter()를 통해 처리된다.

doFilter()
- url-pattern에 맞는 모든 HTTP 요청이 디스패처 서블릿으로 전달되기 전에 웹 컨테이너에 의해 실행되는 메소드이다.
- doFilter의 파라미터로 FilterChain이 있는데, FilterChain의 doFilter 통해 다음 대상으로 요청을 전달할 수 있게 된다.
- chain.doFilter()로 전, 후에 우리가 필요한 처리 과정을 넣어줌으로써 원하는 처리를 진행할 수 있다.

destroy()
- 필터 객체를 제거하고 사용하는 자원을 반환하기 위한 메소드이다.
- 웹 컨테이너가 1회 destroy()를 호출하여 필터 객체를 종료하면 이후에는 doFilter에 의해 처리되지 않는다.
