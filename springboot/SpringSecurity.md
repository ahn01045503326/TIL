# Spring Security 설정
- API 서버에서 jwt로 인증할 때
---

#### 1. build.gradle
- dependencies 추가
````
    implementation 'org.springframework.boot:spring-boot-starter-security' // spring security
````

#### 2. SecurityConfig
````
@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfig {

    private final JwtService jwtService;
    private final JwtAuthenticationEntryPoint jwtAuthenticationEntryPoint;
    private final JwtAccessDeniedHandler jwtAccessDeniedHandler;

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
                .httpBasic().disable() // rest api 이므로 기본설정 사용안함. 기본설정은 비인증시 로그인폼 화면으로 리다이렉트 된다.
                .csrf().disable() // rest api이므로 csrf 보안이 필요없으므로 disable처리.
                .authorizeHttpRequests()
                .requestMatchers("/jwt/**").permitAll() // HttpServletRequest를 사용하는 요청들에 대한 접근 제한 설정
                //.anyRequest().authenticated()
                .and()
                .sessionManagement()
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS) // jwt token으로 인증하므로 세션은 필요없으므로 생성안함.
                .and()
                .addFilterBefore(new JwtAuthenticationFilter(jwtService), UsernamePasswordAuthenticationFilter.class) // jwt filter 적용
                .exceptionHandling()
                .authenticationEntryPoint(jwtAuthenticationEntryPoint) // 우리가 만든 클래스로 인증 실패 핸들링
                .accessDeniedHandler(jwtAccessDeniedHandler); // 커스텀 인가 실패 핸들링

        return http.build();
    }

    @Bean
    public WebSecurityCustomizer webSecurityCustomizer() {
        // WebSecurityCustomizer를 통해 Spring Security를 적용하지 않을 리소스를 설정
        return web -> web.ignoring().requestMatchers("/images/**"); // 정적 자원 및 루트 페이지 ignore
    }

}
````

#### 3. JwtAuthenticationFilter 
- (UsernamePasswordAuthenticationFilter 사용안하고 jwt 필터 사용하기 위해)
````
@RequiredArgsConstructor
public class JwtAuthenticationFilter extends GenericFilterBean {

    private final JwtService jwtService;

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        // 1. Request Header 에서 JWT 토큰 추출
        String token = resolveToken((HttpServletRequest) request);

        // 2. validateToken 으로 토큰 유효성 검사
        if (token != null && jwtService.validateJwt(token)) {

            List<GrantedAuthority> authorities = Arrays.asList(new SimpleGrantedAuthority("ROLE_USER"));
            // 토큰이 유효할 경우 토큰으로 Authentication 객체를 생성해서 SecurityContext 에 저장
            Authentication authentication = new PreAuthenticatedAuthenticationToken(token, null, authorities);
            SecurityContextHolder.getContext().setAuthentication(authentication);
            System.out.println("Security Context에 '{}' 인증 정보를 저장했습니다, uri: {}" +  authentication.getName());
        }
        chain.doFilter(request, response);
    }

    // Request Header 에서 토큰 정보 추출
    private String resolveToken(HttpServletRequest request) {
        String bearerToken = request.getHeader("Authorization");
        if (StringUtils.hasText(bearerToken) && bearerToken.startsWith("Bearer")) {
            return bearerToken.substring(7);
        }
        return null;
    }
}
````

#### 4. JwtAccessDeniedHandler  (권한이 없을때 403)

````
@Component
public class JwtAccessDeniedHandler implements AccessDeniedHandler {
    @Override
    public void handle(HttpServletRequest request, HttpServletResponse response, AccessDeniedException accessDeniedException) throws IOException {
        //필요한 권한이 없이 접근하려 할때 403
        System.out.println("필요한 권한이 없구나");
        response.sendError(HttpServletResponse.SC_FORBIDDEN);
    }
}
````

#### 5. JwtAuthenticationEntryPoint  (유효하지 않은 자격증명일 때 401)

````
@Component
public class JwtAuthenticationEntryPoint implements AuthenticationEntryPoint {

    @Override
    public void commence(HttpServletRequest request, HttpServletResponse response, org.springframework.security.core.AuthenticationException authException) throws IOException, ServletException {
        // 유효한 자격증명을 제공하지 않고 접근하려 할때 401(인증 실패)
        response.sendError(HttpServletResponse.SC_UNAUTHORIZED);
    }
}
````