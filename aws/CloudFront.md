# CloudFront
---
## 1. CloudFront 캐시 정책

> **백엔드 오리진**: 요청을 처리하는 주체 또는 시스템
> CloudFront는 엣지에서 요청을 처리하지 못하면 오리진으로 전달

* 오리진 종류

  * `S3 버킷` (OAC: Origin Access Control, OAI: Origin Access Identity)
  * `HTTP 오리진`: EC2, ALB, API Gateway, 외부 HTTP 서버 등

### 🔧 정책 설정 값

#### TTL

* **Minimum TTL**: 최소 보존 시간 (초)
* **Default TTL**: 기본 보존 시간
* **Maximum TTL**: 최대 보존 시간

#### 캐시 키 (Cache Key)

| 항목          | 설정값                        | 설명                   |
| ----------- | -------------------------- | -------------------- |
| Header      | `All`, `None`, `Whitelist` | 캐시 키에 포함할 HTTP 헤더 지정 |
| QueryString | `All`, `None`, `Whitelist` | URL 쿼리 파라미터 기준 캐싱    |
| Cookie      | `All`, `None`, `Whitelist` | 쿠키 값 기준 캐싱           |

---

## 2. CloudFront 캐시 무효화 (Invalidation)

> TTL이 남아 있으면 오리진의 최신 코드가 반영되지 않음
> 수동 무효화를 통해 엣지 캐시 제거 가능

* 무효화 대상 예:

  * `/*` : 전체 파일 무효화
  * `/경로/*` : 특정 경로만 무효화
* 주의: 여러 개 등록할 경우, `"/*"`가 가장 **마지막**에 실행됨

---

## 3. CloudFront - 오리진 연결

* 연결 가능한 오리진: `S3`, `EC2`, `ALB`
* EC2 / ALB 연결 시:

  * 해당 오리진 보안그룹에 **CloudFront IP 범위 추가 필요**

    * AWS에서 [CloudFront IP 범위 JSON](https://ip-ranges.amazonaws.com/ip-ranges.json) 제공

---

## 4. 지리적 접근 제한 (Geo Restriction)

* CloudFront 자체 기능으로는 **Geo Restriction (허용/차단 국가 설정)**
* **더 정교한 제어**는 **AWS WAF**를 사용해 특정 국가/지역 차단 가능

---

## 5. CloudFront 서명 URL/서명 쿠키

> 퍼블릭 접근이 아닌 경우, **인증된 사용자만** 파일 접근 허용

| 유형         | 특징                                  |
| ---------- | ----------------------------------- |
| **서명 URL** | 파일 단위 제어 (1 URL = 1 파일)             |
| **서명 쿠키**  | 여러 파일을 하나의 쿠키로 통제 가능 (ex: 전체 경로 접근) |

* 주로 **프라이빗 콘텐츠 배포** 시 사용

---

## 6. CloudFront 가격 정책 (Price Class)

| Price Class | 포함 리전          | 용도        |
| ----------- | -------------- | --------- |
| **ALL**     | 모든 리전          | 지연 최소화 목적 |
| **200**     | 미국, 유럽, 아시아 일부 | 기본        |
| **100**     | 가장 저렴한 리전만     | 비용 절감 목적  |

* 비용은 요청 수, 데이터 전송량, 리전별 가격에 따라 결정됨

---

## 7. Multiple Origin 구성

> 고가용성 및 재해 복구(Disaster Recovery)를 위해 다중 오리진 설정 가능

* 예시:

  * `S3 버킷 A` → 정상 처리
  * 실패 시 `S3 버킷 B`로 자동 요청 리디렉션 (CloudFront 기능 활용)

### 로깅 활용

* **Kinesis Data Streams**: 실시간 스트리밍 로그 수집
* **Kinesis Firehose**: 반실시간 로그 수집 및 S3/Redshift로 전송