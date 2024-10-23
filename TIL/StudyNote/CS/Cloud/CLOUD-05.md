#### TIPS
---
[Azure 학습](https://learn.microsoft.com/ko-kr/training/azure/) _keyWord: "만들기"_
### 학습내용
---
**스토리지**
**스토리지 논리적 접근 단위 (정형/비정형)
- `파일` : 데이터 스트림이 파일로 저장되어 폴더로 구조화
- `블록` : 스토리지 하드웨어에 가장 가까운 수준의 최소 데이터 단위
- `데이터 세트` : 테이블, 단락, 레코드와 같은 형식으로 구성된 단위
- `오브젝트`: 객체 단위 구조화 (계층 X, 부여된 고유 ID로 접근)
**스토리지 다중화 및 확장 기술**
- `RAID(Redundant Arrays of Independent Disks)`
	- **다수의 디스크를 병렬적으로 구동하는 동시에 시스템의 신뢰성 향상**
		- 중복 데이터 분산 저장
		- 읽기 요청이 다수의 디스크가 나누어 처리, (읽기 속도 향상)
- `NAS(Network Attached Storage)`
- `SAN(Storage Area Network)`
##### 목표: 웹 서버 구축하고 접속
