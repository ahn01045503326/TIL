# Exception 처리

---

### 1. ControllerAdvice를 이용한 예외 처리

- @ControllerAdvice 어노테이션을 사용하여 전역적으로 예외를 처리할 수 있습니다. ControllerAdvice는 모든 Controller에 적용됩니다.
````
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleException(Exception e) {
        ErrorResponse response = new ErrorResponse();
        response.setMessage(e.getMessage());
        response.setStatus(HttpStatus.INTERNAL_SERVER_ERROR.value());

        return new ResponseEntity<>(response, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
````
위 코드에서 @ControllerAdvice 어노테이션을 사용하여 전역 예외 처리를 할 수 있도록 설정하고, 
@ExceptionHandler 어노테이션을 사용하여 Exception 클래스를 처리하는 핸들러 메서드를 정의하였습니다. 
이 핸들러 메서드는 Exception 발생 시 ErrorResponse 객체를 생성하여 클라이언트에 에러 응답을 반환합니다.

---
### 2. @ExceptionHandler를 이용한 예외 처리
- @ControllerAdvice 어노테이션 없이 @ExceptionHandler 어노테이션을 사용하여 각각의 Controller에서 예외를 처리할 수 있습니다.
````
@RestController
public class UserController {

    @Autowired
    private UserService userService;

    @PostMapping("/users")
    public ResponseEntity<User> createUser(@RequestBody User user) {
        User createdUser = userService.createUser(user);
        return new ResponseEntity<>(createdUser, HttpStatus.CREATED);
    }

    @ExceptionHandler(DuplicateUserException.class)
    public ResponseEntity<ErrorResponse> handleDuplicateUserException(DuplicateUserException e) {
        ErrorResponse response = new ErrorResponse();
        response.setMessage(e.getMessage());
        response.setStatus(HttpStatus.BAD_REQUEST.value());

        return new ResponseEntity<>(response, HttpStatus.BAD_REQUEST);
    }
}
````
위 코드에서 @ExceptionHandler 어노테이션을 사용하여 DuplicateUserException 예외를 처리하는 핸들러 메서드를 정의하였습니다. 
이 핸들러 메서드는 DuplicateUserException 발생 시 ErrorResponse 객체를 생성하여 클라이언트에 에러 응답을 반환합니다.





