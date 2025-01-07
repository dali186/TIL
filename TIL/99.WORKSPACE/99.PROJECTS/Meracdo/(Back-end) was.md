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