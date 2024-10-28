### #1 클라우드 기반 데이터 분석
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
	3. **데이터 전처리 과정(필요한 데이터만 추출)**
		1. Select Columns in Dataset
			1. 필요한 컬럼들만 추출 -> 데이터 미리보기
				1. 누락된(NULL)인 데이터 처리
				2. 0,1 로 boolean 타입이어야 할 컬럼이 Numeric 인 경우 처리
		2. Clean Missing Data
			1. 누락된(NULL)인 데이터 처리
			2. 누락된 값의 row를 제거할 지, 중간 값으로 채울 지 결정
		3. Edit Metadata
			1. 타입이 다른 값을 수정하는 과정
	4. **훈련 데이터 / 검증 데이터 분리**
		1. 7:3 분리
	5. 알고리즘 선택
		1. [Azure Machine Learning Cheat Sheet](https://learn.microsoft.com/ko-kr/azure/machine-learning/algorithm-cheat-sheet?view=azureml-api-1)
		2. Two-Class Boosted Descision Tree

### #2 일기 예보 전송 서비스 구현
---
[날씨 정보 API](https://openweathermap.org/)
