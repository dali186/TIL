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


스웨거
Dev(Business Logic)+Ops(Cloud)
SRE
IASC:Infrastructure As A Code

AWS의 책임은 클라우드 보안에만 
기업 연혁을 보고 그때쯤에 유행하던 기술을 삭 보고 가라(infra는 잘 안바뀜)

인프라에서 캐시 (DB -> Redis -> In-memory), 자주 요청되는 query를 redis에 캐싱
캐싱 정책
- 