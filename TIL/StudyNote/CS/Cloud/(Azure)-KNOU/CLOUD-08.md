### 클라우드 기반 데이터 분석
---
###### Azure Machine Learning
- 리소스 생성 시,
	- 컨테이너 레지스트리만 새로 추가
1. Studio 시작하기
	1. 컴퓨팅 인스턴스 추가
	2. 새로 만들기
		1. 파이프라인 (새 파이프라인 만들기)
			1. 디자이너 탭
2. 디자이너 탭
	1. 데이터 자산 추가
		1. titanic, 타이타닉 탑승자, 데이터, 파일
		2. 웹 파일
		3. `https://raw.githubusercontent.com/jaehwachung/cloud_computing/refs/heads/main/data_analysis/Titanic_dataset.csv`
	2. 생성된 데이터 자산 파이프라인 추가
	3. 데이터 전처리 과정(필요한 데이터만 추출)
		1. Select Columns in Dataset
			1. 필요한 컬럼들만 추출 -> 데이터 미리보기
				1. 누락된(NULL)인 데이터 처리
				2. 0,1 로 boolean 타입이어야 할 컬럼이 Numeric 인 경우 처리
		2. 