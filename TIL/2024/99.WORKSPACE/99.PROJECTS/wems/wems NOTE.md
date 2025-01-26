Spring boot 3.3.4
Java 17
Jar
MySQL 8.4
JPA
https://velog.io/@juno7803/html-to-pdf
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

#### DB 구성
---
**Member**
- `memberSn` (PK): 멤버의 고유 식별자.
- `memberType`: 멤버의 유형 (예: `admin` 또는 `common`).
- `company` (FK): 멤버가 속한 회사의 외래 키로, `Company` 테이블의 `companySn`을 참조.
- `memberName`: 멤버 이름.
**Company**
- `companySn` (PK): 회사의 고유 식별자.
- `companyName`: 회사 이름.
**Project**
- `projectSn` (PK): 프로젝트의 고유 식별자.
- `projectName`: 프로젝트 이름.
- `company` (FK): 프로젝트가 속한 회사의 외래 키로, `Company` 테이블의 `companySn`을 참조.
**Server**
- `serverSn` (PK): 서버의 고유 식별자.
- `projectSn` (FK): `Project` 테이블의 `projectSn`을 참조하는 외래 키.
- `ip`: 서버의 IP 주소.
- `serverName`: 서버 이름.



