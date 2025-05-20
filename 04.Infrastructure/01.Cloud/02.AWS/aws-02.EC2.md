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
[[VPC 생성 가이드]]
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

