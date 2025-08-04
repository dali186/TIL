# Amazon S3 고급 기능 및 보안 
---

## S3 성능 최적화 (Performance Optimization)

1. **Multipart Upload**

   * 대용량 파일(>100MB) 업로드에 사용
   * 병렬 업로드로 속도 향상 및 실패 복구 용이

2. **S3 Transfer Acceleration**

   * 전 세계 CloudFront 엣지를 통해 전송 가속
   * 업로드 시에도 전송 최적화 가능 (PUT 요청)

3. **Byte-Range Fetches**

   * 대용량 객체의 일부분만 읽어오는 기능
   * 병렬 처리에 유리 (ex: 동영상 스트리밍)

4. **Partial Download**

   * 파일 전체 다운로드 없이 필요한 부분만 요청 가능

---

##  S3 메타데이터 및 태그 (Metadata / Tag)

* **사용자 정의 메타데이터**: `x-amz-meta-<key>` 형식
* **Key-Value 구조**
* **검색 불가** → 외부 시스템 필요 (ex: DynamoDB, Elasticsearch)
* **사용 예**: 문서 분류, 다운로드 추적 등 부가정보 저장용

---

## ️ S3 클래스 이동 (Storage Class Lifecycle)

* **수명주기 정책**으로 자동 이동/삭제 설정 가능

  * Standard → IA → Glacier → Deep Archive
* **수명주기 작업**:

  * 객체 이동
  * 삭제
  * 미완료 Multipart 업로드 제거
  * S3 Storage Lens (Analytics)로 모니터링

---

## 🚨 S3 이벤트 알림 (Event Notification)

* \*\*Destination (SNS/SQS/Lambda)\*\*에 IAM 리소스 정책 설정 필요
* **S3 자체에는 권한 부여하지 않음**
* 필터링 가능 (접두사/확장자 기준)

---

##  S3 서버사이드 암호화 (Server-Side Encryption)

### 1. SSE-S3 (S3 Managed Keys)

* 암호화 방식: AES-256
* 헤더: `x-amz-server-side-encryption: AES256`

### 2. SSE-KMS (KMS Managed Keys)

* 헤더: `x-amz-server-side-encryption: aws:kms`
* KMS Key 직접 관리 가능
* CloudTrail 로깅 가능 (GenerateDataKey, Decrypt API)

### 3. SSE-C (Customer Provided Key)

* 키를 직접 제공 (CLI 사용만 가능)
* S3는 키를 저장하지 않음 → 요청마다 전달 필요
* HTTPS 필수

### 기타

* 클라이언트 암호화(SSL/TLS)도 가능
* 암호화 방식 변경 시 새 버전 생성됨
* **SecureTransport 강제**: 버킷 정책에서 `"aws:SecureTransport": true`

---

## ️ S3 MFA Delete

* **객체 버전 삭제** 또는 **버전 관리 중단 시** MFA 필요
* CLI를 통해서만 설정 가능

---

## S3 액세스 로그 (Access Logs)

* **허용/거부 요청 모두 기록**
* 로깅 대상은 **다른 S3 버킷**이어야 함

  * 같은 버킷 지정 시 재귀 호출로 문제 발생

---

##  S3 사전서명 URL (Presigned URL)

* URL을 통한 일시적 접근 권한 부여
* 생성 수단:

  * 콘솔: 12시간
  * CLI: 최대 168시간 (7일)
  * SDK: 커스터마이징 가능

---

##  S3 Access Point

* 특정 버킷 내 접두사(prefix)에 대한 엔드포인트 생성
* 각 포인트는 고유 DNS를 가짐
* IAM 역할 기반 권한 설정
* **VPC Access Point**도 가능 (VPC에서만 접근 가능)

---

##  보완 및 유의사항

* 암호화 방식 변경 시 객체 버전 증가 주의
* 버킷 정책이 객체 기본 암호화 설정보다 우선함
* 메타데이터/태그는 검색용으로 적합하지 않음
* CloudTrail + KMS 로깅 구성 필수 (보안 감사 목적)
