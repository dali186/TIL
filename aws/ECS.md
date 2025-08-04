# AWS ECS 형목별 정보 정리

---

## 🚀 ECS 시작 유형 (Launch Type)

1. **EC2 Launch Type**

   * EC2 인스턴스를 직접 관리
   * ECS Agent가 컨테이너 시작/중지 담당
   * 인프라 구성 및 AutoScaling 직접 설정

2. **Fargate Launch Type**

   * Serverless 운영
   * Task 정의만 하면 AWS가 실행 및 관리
   * EC2 관리 불필요

---

## 🔑 ECS IAM 설정

1. **EC2 Instance Profile** (EC2 전용)

   * ECS Agent가 다음 작업을 수행할 수 있도록 권한 부여:

     * API 호출
     * CloudWatch 로그 전송
     * ECR 이미지 pull
     * SSM Parameter 또는 Secrets 가져오기

2. **ECS Task Role**

   * Task에서 외부 AWS 서비스 호출 시 사용
   * TaskDefinition에서 지정
   * Task마다 다르게 지정 가능

---

## 🌐 Load Balancer + ECS

* **ALB (Application Load Balancer)** 와 ECS 연동 가능
* **ELB (Classic Load Balancer)** 는 ECS와 연동 불가
* 고가용성 필요 시 **NLB (Network Load Balancer)** 활용

---

## 📂 EFS + ECS

* **EFS**는 AZ와 무관하게 여러 Task에서 파일 시스템 공유 가능
* **S3**는 파일시스템처럼 사용 불가 (객체 저장소임)

---

## ⚙️ ECS Service

* **Service**: Task를 계속 유지시키는 관리 단위 (ex: Daemon)
* **Task**: 작업 단위. 실행 후 종료됨 (ex: 배치 작업)

### AutoScaling

* 기준:

  * CPU 사용률
  * 메모리 사용률
  * 요청 수

* AutoScaling 유형:

  * **Target-based**: CloudWatch Metric 기반 목표 설정
  * **Step Scaling**: CloudWatch Alarm 기준 단계별 확장
  * **Scheduled**: 예약 기반 확장/축소

> ⚠️ **ECS Service AutoScaling(Task 수)** ≠ **EC2 AutoScaling(EC2 인스턴스 수)**

### Capacity Provider

* ECS 클러스터가 필요 시 EC2를 자동으로 늘리거나 줄임

### Rolling Update

* 최소/최대 Task 개수 기준으로 점진적 업데이트 수행

---

## 🏢 S3 / EventBridge / SQS + ECS Task 실행 예

* **S3 + EventBridge + ECS Task**: S3 이벤트 발생 시 ECS Task 실행
* **EventBridge + ECS Task**: 스케줄 혹은 이벤트 기반으로 Task 실행
* **SQS + ECS Task**: 메시지 큐 기반 비동기 Task 실행

---

## 🛋️ ECS Task Definition

* 1 Task 당 최대 10개 컨테이너 포함 가능

### 주요 설정 항목

* **이미지 정보** (ECR 등)
* **포트 바인딩 정보**
* **메모리/CPU 설정**
* **환경변수**:

  * 직접 입력
  * SSM Parameter Store / Secrets Manager
  * S3 파일로 일괄 로드
* **네트워크 모드**
* **IAM Role** (Task Role)
* **로깅 구성** (CloudWatch 등)

### Load Balancer 연동 시 주의

* **Fargate**는 호스트가 없기 때문에 **Private IP 사용 필수**
* **ALB는 동적 포트 매핑** 지원 → 포트 고정 불필요
* **ELB는 정적 포트만 가능** → Fargate와 부적합

### Sidecar 패턴

* **EC2**: 로컬 디스크 기반 공유 가능
* **Fargate**: 임시 디렉토리 기반 (ephemeral storage)

---

## 🧰 ECS Task 배치 전략

### 배치 전략 종류

* **binpack**: CPU나 메모리를 최대한 채우는 방식 (비용 최적화)
* **random**: 무작위 배치
* **spread**: 인스턴스 간 균등 분산 (가용성 ↑)

> 전략 혼합 가능 (ex: spread + binpack)

### 배치 제약 조건

1. **distinctInstance**: 같은 인스턴스에 동일 Task 배치 금지
2. **memberOf**: 특정 조건 만족 인스턴스에만 Task 배치

---

## 📄 Copilot

* ECS용 CLI 툴 (AWS 공식)
* ECS 구성, 배포, 모니터링 자동화 지원
* `copilot init`, `copilot deploy`, `copilot svc logs` 등 명령어 지원
