##### 1. EC2 수명주기(LifeCycle)
> Pending -> Running -> Stopping -> Stopped -> Terminated

pending: 인스턴스 시작 준비 중 (부팅, 리소스 할당)
running: 정상 동작 중
stopping: 사용자가 중지 요청
stopped: 꺼진 상태, 다시 시작 가능
terminated: 완전 삭제, 복구 불가

##### 2. Auto Scaling Group (ASG)
> CPU 사용률 등 조건에 따라 수평 확장/축소

