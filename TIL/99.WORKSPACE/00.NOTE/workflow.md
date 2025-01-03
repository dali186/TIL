1. Microsoft Azure VM을 하나 생성한다.
2. 개발 할 Spring Boot Project를 생성한다.
3. Github Repository에 생성한다.
4. Gihub Actions를 이용하여 푸시할 때마다 배포

[Ref. 1](https://velog.io/@rivkode/Docker-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88%EB%A1%9C-Spring-MySQL-%EC%97%B0%EB%8F%99)
##### Github Actions Workflows 작성하기

- Git으로 클론한 프로젝트를 컨테이너화
1. 프로젝트 내 Dockerfile 파일 생성
2. git clone -b develop --single-branch 'repoURL' 으로 develop 브랜치 클론
3. ./gradlew build -x test

## Docker:WAS와 DB 연동하기
#### 1. WAS 컨테이너화
1. 프로젝트 내부에 Dockerfile 생성.
```
FROM openjdk:21
ARG JAR_FILE=build/libs/*.jar
COPY ${JAR_FILE} /Commerce.jar
ENTRYPOINT ["java", "-jar", "/Commerce.jar"]
```
2. 프로젝트 클론 (develop 브랜치 내용 가져옴)
`git clone -b develop --single-branch https://github.com/dali186/Commerce.git`
3. 프로젝트 빌드
```
chmod 777 gradlew
./gradlew build -x test
```
4. 프로젝트 컨테이너화
`docker build -t 컨테이너 이름 .`

#### 2. DB 컨테이너화
1. Mysql 이미지 pull
`docker pull mysql:latest`

#### 3. 네트워크 설정
1. docker 네트워크 생성
`docker network create was_net`
2. DB 컨테이너 실행
`docker run -d --name mysql --network was_net -p 3306:3306 -e MYSQL_ROOT_PASSWORD=mysqladmin -v mysql:/var/lib/mysql --restart unless-stopped mysql:latest`
__호스트에서 컨테이너 내부 Mysql 접속__
`docker exec -it ea5 mysql -u root -p`
```
CREATE DATABASE commerce_db CHARACTER SET utf8 COLLATE utf8_general_ci;
CREATE USER 'commerce_admin'@'%' IDENTIFIED BY 'commerceadmin12!@';
GRANT ALL PRIVILEGES ON commerce_db.* TO 'commerce_admin'@'%';
FLUSH PRIVILEGES;
```
3. WAS(Spring Boot) 실행
`docker run -d --name commerce_was --network was_net -p 8080:8080 --restart unless-stopped commerce_was:latest`

## docker-compose로 이미지 컨테이너화 묶기
1. 프로젝트 파일에 init.sql, docker-compose.yml 파일 생성
```
```
```

```