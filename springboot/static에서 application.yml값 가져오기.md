# static변수에서 application.yml의 값 가져오기

static은 ApplicationContext 초기화 이전에 메모리에 올라가기 때문에 ApplicationContext에 의존적인 값은 사용하실 수 없습니다. 

---

### 이러한 경우에는 setter 함수를 사용하여 Injection

````
@Component
public class iFaceUtils {
    private static StringNAME_STATIC;

    @Value("${spring.config.activate.on-profile}")
    public void setNameStatic(String name){
        iFaceUtils.NAME_STATIC= name;
    }
````