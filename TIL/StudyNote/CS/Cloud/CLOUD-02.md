#### TIPS
---
[Azure 학습](https://learn.microsoft.com/ko-kr/training/azure/) _keyWord: "만들기"_
### 학습내용
---
- 클라우드 서비스 모델은 CSP가 제공하는 IT 리소스의 수준에 따른 구분.
- 소프트웨어는 하드웨어, 운영체제, 라이브러리 및 런타임, 프레임워크 등의 기술이 결합되어 실행
	> Networking | Storage | Servers | Virturalization | O/S | Middleware | Runtime | Data | Applications
	- `IaaS(Infrastructure-as-a-Service)`: Virturalization(가상화)까지 제공
		공연장을 빌려서 무대 구축 + 무대 구성까지 준비
	- `PaaS(Platform-as-a-Service)`: Runtime 까지 제공
		공연장과 구축된 무대까지 대여, 무대 구성만 준비
	- `SaaS(Softeare-as-a-Service)`: 애플리케이션까지 제공
		공연과 무대준비 전부 다 해줌
	- `FaaS(Function-as-a-Service)`: 개발자는 인프라를 유지관리 할 필요 없이 *패키지를 기능으로 빌드,실행 관리(코드만 갈겨라)*
	- `CaaS(Container-as-a-Service)`: 컨ㅌ테이너 기반의 서비스 및 오케스트레이션 지원
- 클라우드 배포 모델: 애플리케이션을 배포할 수 있는 클라우드 환경에 따른 분류
	- `퍼블릭 클라우드`
	- `프라이빗 클라우드`
	- `하이브리드 클라우드`
	- `멀티 클라우드`
	- `커뮤니티 클라우드`
##### 목표: DB 구축
**Azure Database for PostgreSQL 유연한 서버**
	*유연하지 않으면 Windows에서만 사용가능*
**5단계**
1. **기본**
	1. 리소스 그룹
	2. 서버 정보
		1. 서버이름
		2. 지역
		3. ==워크로드 유형== (개발로해야 절약가능)
		4. ==컴퓨팅 + 스토리지==
	3. 고가용성 (중복으로 생성하여 가용성을 높임)
		~~azeruser/0643Kimkim!~~
1. **네트워킹**
	1. 네트워크 연결
		1. 퍼블릭 액세스
		2. 프라이빗 액세스
	2. 방화벽 규칙 (공용 엑세스 체크)
		1. 
2. **보안**
	1. DB에 저장되는 데이터 암호화
1. **태그**
2. **검토+만들기**
방화벽 규칙에서 IP 주소 구성 -> 방화벽에 설정 해두지 않았음
PostgreSQL 유연한 서버 탭 > 설정 > 데이터베이스 > 추가