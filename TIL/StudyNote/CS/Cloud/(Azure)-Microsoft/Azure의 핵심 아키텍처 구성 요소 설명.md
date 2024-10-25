[Ref 2. Link #2](https://learn.microsoft.com/ko-kr/training/modules/describe-core-architectural-components-of-azure/)
1. Azure 계정 시작
	1. Azure Account(계정) > Subscriptions(구독) > Resource groups(리소스 그룹) > Resources(리소스)
2. Azure 인프라
	1. 물리적 인프라 (: IDC를 의미)
		1. 영역 (: IDC의 위치를 의미)
		2. 가용성 영역(: IDC 내의 분리된 DC를 의미)
			VM, 관리 디스크, 부하 분산 장치 및 SQL 데이터베이스에 주로 사용
			1. 영역 서비스: 특정 영역(예: VM, 관리 디스크, IP 주소)에 리소스를 고정
			2. 영역 중복 서비스: 플랫폼이 영역에서 자동으로 복제 (예: 영역 중복 스토리지, SQL 데이터베이스)
			3. 비지역 서비스: 서비스는 Azure 지역에서 항상 사용할 수 있으며 영역 전체 중단뿐만 아니라 지역 전체 중단도 복원
		3. 지역 쌍
		4. 소버린 지역
	2. 관리 인프라
		1. 리소스 및 리소스 그룹
		2. 구독
		3. 관리그룹