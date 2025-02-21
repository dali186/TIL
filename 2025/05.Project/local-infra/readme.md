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

##### ISSUE `docker stop` PERMISSION DENIED
> sudo aa-remove-unknown

apparmor를 제거하는 명령어.
docker를 snap으로 설치하는 경우, AppArmor profile이 쌓이고 충돌이 나는 경우라고 함

이후 과정은 [gitea 구축하기](https://medium.com/@dudwls96/gitea-runner-%ED%86%B5%ED%95%9C-gitea-actions-%EA%B5%AC%EC%84%B1%ED%95%98%EA%B8%B0-9f7f7544ee8e) 참고

