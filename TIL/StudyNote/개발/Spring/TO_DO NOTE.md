공통응답 및 공통예외처리
#### 목표
- Controller Advice + CustomException으로 예외처리 공통화
- ErrMsg, SuccessMsg 등, 상수값 인터페이스에 정의
- DTO를 사용하여 Request, Response 명확화
- @ResponseBody로 응답 시, 공통 응답 모듈 생성.

## 1. 공통응답모듈
**Ajax - Spring**통신 시, 해당 응답 메세지나 결과를 공통 모듈로 전달하기 위해 리팩터링

[Ref. Spring Docs](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/http/ResponseEntity.html)
응답 형식 | 예외처리 | AJAX 받는 변수들...
jqXHR.responseText


- **`NoArgsConstructor (access = AccessLevel.PROTECTED)`**
- JPA proxy 조회 (지연로딩)
