#### JPA 
1. **Update**
	1. Dirty Check
	- [간단한 영속성 설명](https://study-easy-coding.tistory.com/105)
	- Entity를 조회하여 조회된 Entity 데이터 변경만 하면 데이터 베이스에 자동으로 반영
	```
	Member member = repository.findById(membersn);
	member.setMemberId("123);
	```
	- Entity에 Setter를 쓰면 OCP(Open Closed Principle, 개방 폐쇄 원칙)에 위배된다고 판단, Member Entity에 수정 메서드를 구현
2. Entity 기본생성자 필요
	- Hibernate는 엔티티 클래스를 생성할 때 기본 생성자를 사용하기 때문에 Entity에 필수로 들어가 있어야함
#### Test
1. Mockito
	- DB 연결없이 가짜 객체를 만들어서 테스트 진행
	- Junit5으로만 테스트 진행 시
		-  @Test를 수행하는 testsIsNotNullCodeList() 메서드 실행
		- 서비스 호출을 위해 ‘Local Server’를 실행시켜서 DB 데이터를 조회
		- 로컬 서버를 사용하지 않기 위해 Mockito로 대체

#### Logging
- Docker container 내부 Was의 로그를 Host에서 받아 보기 위해서
	1. 기본 로깅 설정 (application.yml)
		```
		  logging:
			  pattern:
				  console: "%d{yyyy-MM-dd HH:mm:ss} - %msg%n"  # 콘솔 로그 출력 패턴 설정
				  file: "%d{yyyy-MM-dd HH:mm:ss} - %msg%n"  # 파일 로그 출력 패턴 설정
			  level:
				  root: INFO
				  com.dali186.Mercado: DEBUG
		```
	1. Dockerfile 설정 (디렉터리 지정)
	2. docker-compose 설정 (docker volume 설정)
##### Chat
- 채팅방 정보는 Redis에 저장
- STOMP 연결이 지속되는 동안에는 redis에 저장
	- TTL을 사용하여 시간이 지나면 RDBMS에 저장하도록 트리거

##### 1. Redis 연결
1. gradle 추가
```
implementation 'org.springframework.boot:spring-boot-starter-data-redis'
```
2. RedisConfig 추가
	1. RedisConnectionFactory
		- Redis와의 연결을 위한 'Connection'을 생성하고 관리하는 메서드
		- 해당 여기서는 LettuceConnectionFactory를 사용하여 host와 port 정보를 기반으로 연결을 생성
	2. RedisTemplate<String, Object>
		- Redis 데이터 처리를 위한 템플릿을 구성하는 메서드입니다. 이 메서드에서는 Redis와의 데이터 통신을 처리하기 위한 직렬화를 수행합니다.


스웨거
Dev(Business Logic)+Ops(Cloud)
SRE
IASC:Infrastructure As A Code

AWS의 책임은 클라우드 보안에만 
기업 연혁을 보고 그때쯤에 유행하던 기술을 삭 보고 가라(infra는 잘 안바뀜)

인프라에서 캐시 (DB -> Redis -> In-memory), 자주 요청되는 query를 redis에 캐싱
캐싱 정책
이미지 리사이징 프로젝트

Internet Gateway
- 인터넷과 연결된 통로
	- VPC와 인터넷 연결
	- 퍼블릭 IP 통신 지원

ACL
Internet Gateway
VPC
NAT Gateway
Subnet
Routing Table

TIP
- 기본 VPC 사용하지 않기(국룰)
	- 삭제가 안되니 태그를 달아놓자 쓰지말라고
- VPC 마법사를 통해 신규 생성
- NAT Gateway는 프리티어가 없다. 개인 프로젝트에서는 굳이 사용 X
- private 서브넷에 중요 자원을 두고 보호