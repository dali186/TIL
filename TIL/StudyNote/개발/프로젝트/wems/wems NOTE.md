Spring boot 3.3.4
Java 17
Jar
MySQL
JPA

- 사용자/관리자 화면 UI 구성 및 개발
- Report DB 구조 구성
- 모니터링 솔루션 시장 조사

1. Database Driver 설정
2. 사용자 도메인 생성(사용자/관리자)
3. API 명세, (일일, 주간, 월간, 연간)
4. 출력
	1. web 화면으로 출력
	2. pdf로 출력
5. Promethues 쿼리 API 분석
	1. 쿼리 쏘기 전 까지 개발
6. Report 유형 / 기간 / 대상 서버
	- 대상 서버 -> Report 유형 -> 기간

#### 순서 정리
1. DB Driver 설정
2. Basic Domain 생성
	1. Member
		- usersn, usernm, userid, userpwd, userrole,
	2. Comment