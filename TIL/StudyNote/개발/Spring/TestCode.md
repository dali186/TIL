##### 통합 테스트(Integration Test)
**모듈을 통합하는 과정에서 모듈 간의 호환성을 확인하기 위한 테스트**
##### 단위 테스트(Unit Test)
**하나의 모듈[^1]을 기준으로 독립적으로 실행되는 가장 작은 단위의 테스트** 
#### 좋은 단위 테스트 기준(FIRST)
1. `Fast` : 빠르고
2. `Independent` : 독립적이고 (의존적이지 않고)
3. `Repeatable` : 반복 가능하고
4. `Self-Validating` : 자기 검증이 가능하고
5. `Timely` : 빨리 작성되야 한다.
#### Given•When•Then
- `given` : 입력이 있을 때
- `when` : 목표 모듈을 실행하면
- `then` : 예상한 출력이 나온다.
###### 사용한 라이브러리
```
testImplementation 'org.mockito:mockito-core:3.3.3'
testImplementation 'org.assertj:assertj-core:3.24.2'
```
##### 예제 코드(Service 단위 테스트)
```
@ExtendWith(MockitoExtension.class)  
public class ProductServiceTest {  
  
    @InjectMocks  
    private ProductService productService;  
  
    @Mock  
    private ProductRepository productRepository;  
  
    @Test  
    @DisplayName("상품 등록 테스트")  
    public void registerProductTest() {  
        //given  
        ProductRegisterDto registerDto = new ProductRegisterDto("TestProduct3", 25000, 15);  
        Product product = registerDto.toEntity();  
        //stub  
		BDDMockito.given(productRepository.save(any(Product.class))).willReturn(registerDto.toEntity());  
        //when  
        Long resultId = productService.registerProduct(registerDto);  
        //then  
        Assertions.assertThat(product.getId()).isEqualTo(resultId);  
    }  
}
```
> 해당 테스트는 Service의 메서드를 테스트 한다.
> `given`: 테스트의 입력이 될 객체를 생성한다. (Dto와 Entity 객체 둘 다 생성)
> `stub`: Repository의 save메서드의 반환 값을 지정. 이때 Mock객체로 `productRepositoy.save()`가 실행될 때 반환될 값을 지정해둔다.
> `when` : 실제 테스트의 수행 단계
> `then`: 예상한 결과가 도출됐는지 검증한다.

*사실 위 코드는 영양가가 없다. Service메소드에 특별한 비즈니*

[^1]: 하나의 기능 또는 메소드