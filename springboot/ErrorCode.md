# Error Code (enum)

---

#### Error code, message 정리
````
@AllArgsConstructor
@Getter
public enum ErrorCode {

    //400 BAD_REQUEST 잘못된 요청
    ORDERNUMBER_INVALID_PARAMETER(400, "주문번호 파라미터 값을 확인해주세요."),
    EMAIL_INVALID_PARAMETER(400, "이메일 파라미터 값을 확인해주세요."),
    PHONEMODEL_INVALID_PARAMETER(400, "폰모델 파라미터 값을 확인해주세요."),
    PHONECASE_INVALID_PARAMETER(400, "폰케이스 파라미터 값을 확인해주세요."),
    ORIGINIMAGE_INVALID_PARAMETER(400, "원본이미지 파라미터 값을 확인해주세요."),
    PREVIEWIMAGE_INVALID_PARAMETER(400, "프리뷰이미지 파라미터 값을 확인해주세요."),

    //404 NOT_FOUND 잘못된 리소스 접근
    ORDERNUMBER_NOT_FOUND(404, "존재하지 않는 주문번호 입니다."),
    EMAIL_NOT_FOUND(404, "존재하지 않는 이메일입니다."),
    PHONEMODEL_NOT_FOUND(404, "존재하지 않는 폰모델입니다."),
    PHONECASE_NOT_FOUND(404, "존재하지 않는 폰케이스입니다."),
    ORIGINIMAGE_NOT_FOUND(404, "존재하지 않는 원본 이미지입니다."),
    PREVIEWIMAGE_NOT_FOUND(404, "존재하지 않는 프리뷰 이미지입니다."),

    //409 CONFLICT 중복된 리소스
    ALREADY_SAVED_ORDERNUMBER(409, "이미 저장한 주문번호입니다."),
    ALREADY_SAVED_EMAIL(409, "이미 저장한 이메일입니다."),

    //500 INTERNAL SERVER ERROR
    INTERNAL_SERVER_ERROR(500, "서버 에러입니다. 서버 팀에 연락주세요!"),
    S3_SERVER_ERROR(500,"S3 업로드 에러입니다. 관리자에게 연락주세요!"),
    ORDER_INSERT_ERROR(500,"order insert 에러입니다. 관리자에게 연락주세요!"),
    FILEDATA_INSERT_ERROR(500,"file_data insert 에러입니다. 관리자에게 연락주세요!"),
    JWT_CREATE_ERROR(500,"JWT 생성 에러입니다. 관리자에게 연락주세요!"),
    JWT_DECODE_ERROR(500,"JWT 복호화 에러입니다. 관리자에게 연락주세요!");

    private final int status;
    private final String message;
}
````
