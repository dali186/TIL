1. Virtual Box로 Ubuntu VM 생성
Ubutuntu-24.04 LTS live-server amd64.iso
RAM 8192MD(8GB)
CPU core 4
HDD 100GB
- 미리 전체 크기 할당 옵션 off (on 일 경우 생성 시 해당 크기만큼 차지)
[NTCreateFile 이슈](https://m.blog.naver.com/jrkim/221522494580)

1. 생성한VM SSH 접속
**HostOS에서 확인되는 VirtualBox IP**
`ipconfig /all`, 192.168.56.1
**VM이 할당받은 VitrualBox NAT IP**
10.0.2.15
**포트포워딩 설정**
HostIP: VirtualBox IP / Guest IP: VitrualBox NAT IP

##### VM Headless Mode Execute
가상머신을 백그라운드에서 실행하기
--환경변수 설정 생략--
1. VirtualBox 설치 경로 + VBoxManage 설치 경로 확인
	C:\Program Files\Oracle\VirtualBox
2. PowerShell 실행 후 해당 디렉터리로 이동
	dir C:\Program Files\Oracle\VirtualBox
3. 명령어 실행
	./VBoxManage startvm "가상 머신 이름" --type headless
	./VBoxManage startvm "ubuntu-local" --type headless
근데 좀 많이 느림

> VirtualBox를 설치하면 HostOS에 VirtualBox용 NIC가 생성되고 생성된 NIC 안 NAT처리된 사설네트워크IP 중 하나를 VM이 차지

### Docker용 사용자 생성
- Linux 사용자 생성
useradd -m -s /bin/bash dockerusr
- 비밀번호 설정
passwd dockerusr
- 그룹 추가
usermod -aG docker dockerusr

### Docker Network
- docker가 설치되면 `docker0`이라는 NIC가 생성됨
- _**해당 도커 컨테이너에 아무런 설정을 하지 않는다면 외부에서 접근할 수 없으며 오로지 해당 도커 컨테이너를 구동시킨 호스트에서만 접근 가능**_
- 