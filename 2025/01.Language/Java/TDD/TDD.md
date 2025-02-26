> UnitTest는 DB연결을 하지 않는다.
> 주요 로직에 대해서 TestCode를 작성한다.

##### 작업순서
1. 로직에 대한 구현은 배제, 테스트 코드를 작성
2. 테스트 코드의 에러(컴파일 등)을 제거하기 위해 실제코드를 수정 및 구현
3. 테스트를 성공시키기 위해 실제 코드를 수정 및 구현
4. 반복 진행 

### JUnit
---
- _@TestFactory_ – 동적 테스트를 위한 테스트 팩토리인 메서드를 나타냅니다.
- _@DisplayName_ – 테스트 클래스 또는 테스트 메서드에 대한 사용자 정의 표시 이름을 정의합니다.
- _@Nested_ – 주석이 달린 클래스가 중첩된 비정적 테스트 클래스임을 나타냅니다.
- _@Tag_ – 필터링 테스트를 위한 태그를 선언합니다.
- _@ExtendWith_ – 사용자 정의 확장을 등록합니다.
- _@BeforeEach –_ 주석이 달린 메서드가 각 테스트 메서드 전에 실행됨을 나타냅니다(이전에는 _@Before_ )
- _@AfterEach – 주석이 달린 메서드가 각 테스트 메서드(이전에는_ _@After_ ) 이후에 실행됨을 나타냅니다.
- _@BeforeAll_ – 주석이 달린 메서드가 현재 클래스의 모든 테스트 메서드보다 먼저 실행됨을 나타냅니다(이전에는 _@BeforeClass_ ). => static만 가능
- _@AfterAll_ – 주석이 달린 메서드가 현재 클래스의 모든 테스트 메서드 이후에 실행됨을 나타냅니다(이전에는 _@AfterClass_ ).
- _@Disabled_ – 테스트 클래스 또는 메서드를 비활성화합니다(이전에는 _@Ignore_ )

##### Assertions(주장) Assumptions(가정)
**Assertions**
- assertTrue()
- assertEquals()
- assertAll()

F.I.R.S.T
Fast
Independent
- 객체의 상태, 메소드, 이전 테스트 상태, 다른 메소드의 결과등에 의존해서는 안됩니다.
Repeatable
Self-validating
- Assert문 등에 의해 성공 여부가 결과로 나타나야함
Timely


### 1. `@Mock`

- **용도**: 테스트 대상 클래스에서 의존하는 외부 객체를 모의(mock) 객체로 생성합니다. 이는 실제 구현체가 아닌 가짜 객체로, 메서드의 호출을 기록하고 정의한 대로 동작할 수 있습니다.
- **예시**:
    
    java
    
    복사편집
    
    `@Mock private ArticleRepository articleRepository;`
    
    위 코드는 `ArticleRepository`의 Mock 객체를 생성합니다.

### 2. `@InjectMocks`

- **용도**: 테스트할 클래스에 Mock 객체를 주입(inject)합니다. 이 어노테이션을 사용하면 Mockito가 자동으로 Mock 객체를 찾아서 테스트 대상 클래스의 필드에 주입합니다.
- **예시**:
    
    java
    
    복사편집
    
    `@InjectMocks private ArticleService articleService;`
    
    위 코드는 `ArticleService` 객체를 생성하고, `@Mock`으로 생성된 `articleRepository`를 `ArticleService`의 필드에 주입합니다.