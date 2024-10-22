#### TIPS
---
[Azure 학습](https://learn.microsoft.com/ko-kr/training/azure/) _keyWord: "만들기"_
### 학습내용
---
**가상화**: 애플리케이션, 서버, 스토리지, 네트워크 같은 IT 리소스를 논리적으로 분할/통합 -> 이용률 가용성 높임
- **파티셔닝**: 자원 분배
- **캡슐화**: 간단한 인터페이스 제공
- **격리**: 장애발생 시 주변 영향 X
- **H/W 독립화**: 할당 받은 자원만 사용할 수 있도록
	
==**여러 물리적인 서버를 통합하여 더 세분화 된 S/W로 분할**==
**가상머신(Virtual Machine)**
	- 가상화 기술을 통하여 나누어진 기초적 논리적 단위의 머신
	- 하드웨어 > 가상화 계층 > 여러개의 VM
***서버 가상화***
- 호스트 가상화 (실행환경 n개면, OS는 n+1개가 실행되어야 함.)
	-  H/W > O/S > 가상화 S/W > *게스트 OS* 여러개
		- VMWare Workstation
		- Microsoft Virtual Server
		- Oracle Virtural Box
- 하이퍼바이저 가상화
	- 특정 OS에 의존하지 않고 하드웨어 직접 설치되는 구조(호스트 OS가 없음, H/W 다음 바로 하이퍼바이저)
		- VMware ESXi
		- Mircrosoft Hyper-V
		- Citirx XenServer
	- 방식
		- 전가상화(full-virtualization)
			- H/W를 완전히 가상화
			- Dom0를 통해 게스트 OS의 커널 요청을 번역하여 H/W 전달
		- 반가상화(para-virtualization)
			- 게스트 OS가 하이퍼콜을 요청할 수 있도록 커널이 수정된 형태(Linux정도만 사용 가능)
- 컨테이너 방식
	- **애플리케이션을 동작시키는데 필요한 라이브러리 및 종속 리소스를 함께 패키지로 묶어 생성한 호스트 OS상의 논리적인 구역**
	- ==운영체제가 단 한개==
	- docker 대신에 container d, cri-o(대체 컨테이너 런타임 사용)
##### 목표: 키자격모음 + PostgreSQL 서버 관리
**키 자격 증명 모음**
**5단계**
	1. **기본**
	**2. 액세스 구성**
	**3. 네트워킹**
	**4. 태그**
	**5. 검토+만들기**
