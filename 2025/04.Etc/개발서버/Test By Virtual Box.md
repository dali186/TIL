# 1. Test Server Spec
---
***(참고) 23년 하반기 적용 버전 (참고_2023년 하반기 G-클라우드 표준 템플릿 버전정보)***
*RHEL 8.8*
*or*
*Oracle Linux 8.8*

**==두개 리눅스에 호환이 가능한 RockyLinux 선정==**
#### 1. 테스트 서버 스펙
(OS) **Rocky Linux minimal 8.10**
(VM) **OracleVirtualBox 7.1.6**
(RAM) 8GB
(CPU) 4core
(Storage) 100GB(HDD)

###### Ref. VM 계정정보
`root` root / root
`관리자` nibp / nibp

#### 2. 작업내역
##### ~~1. Docker 설치 : RHEL~~
[Docker Document:RHEL Install](https://docs.docker.com/desktop/setup/install/linux/rhel/)
```Shell
sudo dnf install subscription-manager

sudo subscription-manager repos --enable codeready-builder-for-rhel-8-$(arch)-rpms
sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo dnf install pass

# enable EPEL as described above
sudo dnf install gnome-shell-extension-appindicator
sudo dnf install gnome-shell-extension-desktop-icons
sudo gnome-shell-extension-tool -e appindicatorsupport@rgcjonas.gmail.com

# sudo dnf install gnome-terminal

sudo dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
dnf update
sudo dnf install ./docker-desktop-x86_64-rhel.rpm
```

##### 2. Docker 설치 : RockyLinux
```Shell
sudo yum install -y yum-utils
sudo yum-config-manager \
	--add-repo \
	https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
```

##### 3. 디렉터리 생성
`/`
├─ `NIBP`
	├─ `docker-compose.yml`
	├─ `httpd`
	├─ `jboss`
	├─ `postgres`

###### docker-compose.yml
```yml
services:
  web:
    image: httpd:2.4.51
    container_name: httpd
    restart: always
    ports:
        - "80:80"
        - "443:443"
    volumes:
        - ./httpd/httpd.conf:/usr/local/apache2/conf/httpd.conf
        - ./httpd/conf.d/:/usr/local/apache2/conf/extra/
        - ./httpd/logs:/usr/local/apache2/logs
        - ./httpd/www:/usr/local/apache2/htdocs
        - ./httpd/ssl:/usr/local/apache2/conf/ssl
    networks:
        - nibp_dev
    depends_on:
        - was

  was:
    image: quay.io/wildfly/wildfly:26.1.3.Final
    container_name: jboss
    restart: always
    environment:
        - JBOSS_HOME=/opt/jboss/wildfly
        - WILDFLY_USER=nibp
        - WILDFLY_PASSWORD=nibp
    ports:
        - "8080:8080"
    volumes:
        - ./jboss/configuartion:/opt/wildfly/standalone/configuration
        - ./jboss/deployments:/opt/wildfly/standalone/deployments                
        - ./jboss/logs:/opt/wildfly/standalone/log    
    networks:
        - nibp_dev
    depends_on:
        - db

  db:
    image: postgres:14.8
    container_name: postgres
    restart: always
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: postgres
      PGDATA: /var/lib/postgresql/data
    ports:
        - "5432:5432"
    volumes:
        - ./postgres/postgresql.conf:/etc/postgresql/postgresql.conf  
        - ./postgres/pg_hba.conf:/etc/postgresql/pg_hba.conf          
        - ./postgres/data:/var/lib/postgresql/data                    
        - ./postgres/logs:/var/log/postgresql  
    networks:
        - nibp_dev

networks:
  nibp_dev:
    driver: bridge

volumes:
  postgres:
    driver: local

```

##### 4. 테스트 진행 
###### 설정파일 세팅
1. 먼저 컨테이너를 올리고 실행
2. exec 명령어로 해당 컨테이너에 설정파일 위치 확인
3. `docker cp <container_id>:/container/file/path /path/to/host` 명령어로 설정파일 copy
4. copy한 설정파일 수정 후 docker-compose에 mount 


Docker: mount / Dokcer: Volume
/var/lib/docker/image/overlay2/layerdb/sha256

1. Linux Group 및 Account 분리

##### Docker 설정
1. 설정파일 호스트 to 컨테이너 마운트
2. 컨테이너 로그 호스트 to 컨테이너 마운트
3. 