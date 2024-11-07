Azure for Students 구독에서 기본으로 제공해주는 공인 IP는 최대 3개이다.
추가 요청을 할 수있다는데... 귀찮으니까 공인 IP를 제거해보자.

Docker가 아닌 그냥 VM으로 구성하다보니까 공인 IP를 인스턴스 당 하나씩 부여 받았다. (WEB, WAS, DB)
Jenkins도 일단 WAS에 구축 했다...

인스턴스를 하나 더 생성해서 Jenkins 올리고 구현이 완료되면,
WAS, WEB, DB 하나 씩 더 생성해서 로드밸런싱 구현하는게 목표

SSH key로 연결하는 방법을 찾았으니, (배스천 호스트 방식 아님, 그냥 pem 키로 접속)
Jenkins를 다시 구축하고, promethus까지 올리는게 목표
```
sudo ssh -i /home/infra-admin/3-tier-pair-key.pem infra-admin@10.1.0.5
```

공인 IP를 제거했으니, 포트포워딩으로 젠킨스 서버의 8080을 web서버의 포트로 물려보자

SSH 접속
```
root@3-tier-web:/# ssh -i /home/infra-admin/keyrings/3-tier-pair-key-jenkins.pem infra-admin@10.1.0.7
The authenticity of host '10.1.0.7 (10.1.0.7)' can't be established.
ED25519 key fingerprint is SHA256:m8R41bknMfLjMfdThW5RxXUKF8WYsR2IoY1WHAkLE80.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.1.0.7' (ED25519) to the list of known hosts.
Welcome to Ubuntu 24.04.1 LTS (GNU/Linux 6.8.0-1017-azure x86_64)
```
내 Web 서버 VM에 pem키를 올려두고 pem키를 이용해서 다른 VM에 SSH 접속하는 방식으로 시작했다.
잘 모르겠지만 일단 넘어가고 다음에 봅시다...

우선 포트포워딩을 진행해보자
젠킨스를 8080 포트로 구축하고, 해당 포트를 웹서버의 8081로 열어줘보자
