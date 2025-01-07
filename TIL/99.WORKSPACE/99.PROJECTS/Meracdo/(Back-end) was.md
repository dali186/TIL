#### JPA Update
1. Dirty Check
	- [간단한 영속성 설명](https://study-easy-coding.tistory.com/105)
	- Entity를 조회하여 조회된 Entity 데이터 변경만 하면 데이터 베이스에 자동으로 반영
	```
	Member member = repository.findById(membersn);
	member.setMemberId("123);
	```
	- 