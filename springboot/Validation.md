# validation check

---

#### 1. JSR-303(Bean Validation) 기반의 어노테이션 사용:
- Spring Boot는 JSR-303 스펙에 따라 유효성 검사를 수행할 수 있는 어노테이션을 제공합니다.
- 일반적으로 DTO(Data Transfer Object)나 엔티티 클래스에 어노테이션을 추가하여 유효성을 검사합니다.
- 주요한 어노테이션으로는 @NotNull, @NotBlank, @Size, @Min, @Max, @Email, @Pattern 등이 있습니다.

````
public class UserDTO {
    @NotBlank(message = "이름은 필수 입력 항목입니다.")
    private String name;

    @Email(message = "올바른 이메일 주소를 입력하세요.")
    private String email;

    // Getter, Setter, 등...
}
````

#### 2. 커스텀 Validator 구현:
- Spring Boot에서는 유효성 검사를 위한 커스텀 Validator를 구현하여 사용할 수도 있습니다. 
- Validator 인터페이스를 구현하고, validate() 메서드에서 유효성 검사 로직을 작성합니다. 
- 이후 해당 Validator를 사용하고자 하는 클래스에 @Validated 어노테이션과 @Valid 어노테이션을 사용하여 유효성 검사를 수행합니다.

````
@Component
public class UserValidator implements Validator {

    @Override
    public boolean supports(Class<?> clazz) {
        return UserDTO.class.isAssignableFrom(clazz);
    }

    @Override
    public void validate(Object target, Errors errors) {
        ValidationUtils.rejectIfEmptyOrWhitespace(errors, "name", "name.required", "이름은 필수 입력 항목입니다.");
        UserDTO user = (UserDTO) target;
        if (!isValidEmail(user.getEmail())) {
            errors.rejectValue("email", "email.invalid", "올바른 이메일 주소를 입력하세요.");
        }
    }

    private boolean isValidEmail(String email) {
        // 이메일 유효성 검사 로직
        // ...
    }
}
````

````
@RestController
@RequestMapping("/users")
@Validated
public class UserController {

    private final UserValidator userValidator;

    public UserController(UserValidator userValidator) {
        this.userValidator = userValidator;
    }

    @PostMapping
    public ResponseEntity<String> createUser(@RequestBody @Valid UserDTO userDTO) {
        // 유효성 검사를 통과한 경우 처리
        // ...
    }
}
````
