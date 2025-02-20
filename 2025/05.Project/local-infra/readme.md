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
HostIP: VirtualBox IP / 
