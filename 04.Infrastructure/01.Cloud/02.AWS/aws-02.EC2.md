##### 1. EC2 수명주기(LifeCycle)
> Pending -> Running -> Stopping -> Stopped -> Terminated

pending: 인스턴스 시작 준비 중 (부팅, 리소스 할당)
running: 정상 동작 중
stopping: 사용자가 중지 요청
stopped: 꺼진 상태, 다시 시작 가능
terminated: 완전 삭제, 복구 불가

##### 2. Auto Scaling Group (ASG)
> CPU 사용률 등 조건에 따라 수평 확장/축소

###### 2-1. VPC(Virtual Private Cloud)
1. VPC
	- AWS에서 사용할 네트워크 공간(IP 대역 지정)
2. Subnet
	- VPC 안에 있는 네트워크 단위 (public / private)
3. Internet Gateway
	- 인터넷 통신을 위한 게이트웨이
4. Route Table
	- 어떤 트래픽을 어디로 보낼지 지정
5. Security Group
	- 방화벽 역할

## 🛠️ VPC 생성 가이드 (Step by Step)
### 1. VPC 생성
1. AWS 콘솔 상단 검색창에 `VPC` 검색 → VPC 대시보드 진입
2. 왼쪽 메뉴 → **Your VPCs** 클릭 → [**Create VPC**] 버튼 클릭
3. **VPC Only** 템플릿 선택
4. 아래 입력

|항목|값|
|---|---|
|**Name tag**|`my-vpc`|
|**IPv4 CIDR block**|`10.0.0.0/16`|
|IPv6 CIDR block|(None 선택)|
|Tenancy|Default|

→ [Create VPC] 클릭
### 2. Subnet 생성
1. 왼쪽 메뉴 → **Subnets** → [Create subnet]
2. 아래 입력:

| 항목                    | 값                    |
| --------------------- | -------------------- |
| **Name**              | `my-public-subnet`   |
| **VPC**               | 위에서 만든 `my-vpc` 선택   |
| **Availability Zone** | 예: `ap-northeast-2a` |
| **IPv4 CIDR block**   | `10.0.1.0/24`        |

→ [Create subnet]
### 3. Internet Gateway 생성 & 연결
1. 왼쪽 메뉴 → **Internet Gateways** → [Create internet gateway] 
2. 이름: `my-igw` → [Create]
3. 생성 후 → 선택 → **Actions → Attach to VPC** → `my-vpc` 선택
### 4. Route Table 설정
1. 왼쪽 메뉴 → **Route Tables** → 생성된 Route Table 중 `my-vpc` 연결된 것 선택 
2. 하단 탭에서 **Routes** 클릭 → [Edit routes]
3. [Add route] 클릭:

| Destination | Target                         |
| ----------- | ------------------------------ |
| `0.0.0.0/0` | Internet Gateway (`my-igw`) 선택 |

→ [Save]
4. 하단 탭 **Subnet associations** → [Edit subnet associations]  
    → `my-public-subnet` 체크 후 저장
### 5. 보안 그룹(Security Group)
1. EC2 생성 시 사용할 예정 (포트 22, 80 열기)  
    → EC2 만들 때 같이 설정할 수 있어

```vbnet
VPC: 10.0.0.0/16
├── Subnet: 10.0.1.0/24 (my-public-subnet)
│   └── 연결된 라우트 테이블 (0.0.0.0/0 → IGW)
└── Internet Gateway 연결

```

