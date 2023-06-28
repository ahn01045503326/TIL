# 인터셉터(Interceptor)

쉽게 말해 요청에 대한 작업 전 / 후로 가로챈다고 보면 된다.

Dispatcher Servlet이 Controller를 호출하기 전 / 후에 인터셉터가 끼어들어 요청과 응답을 참조하거나 가공할 수 있는 기능을 제공한다.

웹 컨테이너에서 동작하는 필터와 달리 인터셉터는 스프링 컨텍스트에서 동작한다.

디스패처 서블릿이 핸들러 매핑을 통해 컨트롤러를 찾도록 요청하는데, 그 결과로 실행 체인(HandlerExecutionChain)을 돌려준다.
여기서 1개 이상의 인터셉터가 등록되어 있다면 순차적으로 인터셉터들을 거쳐 컨트롤러가 실행되도록 하고,
인터셉터가 없다면 바로 컨트롤러를 실행한다.

실제로 Interceptor가 직접 Controller로 요청을 위임하는 것은 아니다.

![interceptor](/image/interceptor.png)

---

### 인터셉터(Interceptor)의 메소드 종류

인터셉터를 추가하기 위해서 org.springframework.web.servlet의 HandlerInterceptor 인터페이스를 구현(implements) 해야 하며, 다음과 같은 메소드를 가진다.

````
public interface HandlerInterceptor {

	default boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
			throws Exception {
 
		return true;
	}
 
	default void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler,
			@Nullable ModelAndView modelAndView) throws Exception {
	}
 
	default void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler,
			@Nullable Exception ex) throws Exception {
	}
````

preHandle()
- Controller가 호출되기 전에 실행된다.
- 컨트롤러 이전에 처리해야 하는 전처리 작업이나 요청 정보를 가공하거나 추가하는 경우에 사용할 수 있다.

postHandle()
- Controller가 호출된 후에 실행된다. ( View 렌더링 전)
- 컨트롤러 이후에 처리해야 하는 후처리 작업이 있을 때 사용할 수 있다. 
- 이 메소드는 컨트롤러가 반환하는 ModelAndView 타입의 정보가 제공되는데, 최근에는 JSON 형태로 데이터를 제공하는 RestAPI 기반의 컨트롤러(@RestController)를 만들면서 자주 사용되지 않는다.

afterCompletion()
- 모든 뷰에서 최종 결과를 생성하는 일을 포함해 모든 작업이 완료된 후에 실행된다. ( View 렌더링 후)
  요청 처리 중에 사용한 리소스를 반환할 때 사용할 수 있다.

### 인터셉터(Interceptor)와 AOP 비교

인터셉터 대신에 컨트롤러들에 적용할 부가기능을 어드바이스로 만들어 AOP를 적용할 수도 있다.

하지만 다음과 같은 이유들로 컨트롤러의 호출 과정에 적용되는 부가기능들은 인터셉터를 사용하는 편이 낫다.

1. 컨트롤러는 타입과 실행 메소드가 모두 제각각이라 포인트컷(적용할 메소드 선별)의 작성이 어렵다.
2. 컨트롤러는 파라미터나 리턴 값이 일정하지 않다.

즉, 타입이 일정하지 않고 호출 패턴도 정해져 있지 않기 때문에 컨트롤러에 AOP를 적용하려면 번거로운 부가 작업들이 생기게 된다.