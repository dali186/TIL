##### 1. Ubuntu SSH Port 변경
1. $ sudo vi /etc/ssh/sshd_config
2. Port 수정
3. $ sudo systemctl daemon-reload 
4. $ sudo systemctl restart ssh
##### 2. 6010 Port
> X11 포워딩은 SSH를 통해 원격 X11 애플리케이션을 로컬 머신에서 실행할 수 있게 해주는 기능

