#### Work List
- Algorithm
- TDD(WPMS)
- 대용량 트래픽 + Docker
- Next-Blog
	- 도메인 적용
	- SSL 인증서 적용
	- MongoDB Atlas 적용
	- 백업 정책
- Article 작성 (정리)
- Resume
- KNOU 과제
###### 04.09(수)
1. (NEXT-BLOG) 
	1. VM 마이그레이션
		1. GithubAction DockerHub 인증 오류
			next Error pull access denied for ---/next-blog, repository does not exist or may require 'docker login': denied: requested access to the resource is denied
			**=> YML 파일에 DockerHubId가 중복으로 기입되어있음**
	2. 코드 리팩터링
		2. BlobStorage 이미지 연동 확인
		3. 다크모드 CSS 수정
		4. 게시글 Update 로직 수정
		5. 로깅 수정
2. (SonarQube)
	1. SonarQube 구축
		- SonarQube와 PostgreSQL 필요
		- 컨테이너 환경에서 구축
		```yml
		services:
		  sonarqube:
		    image: sonarqube:latest
		    container_name: sonarqube
		    depends_on:
		      - db
		    ports:
		      - "9000:9000"
		    environment:
		      SONAR_JDBC_URL: jdbc:postgresql://db:5432/sonarqube
		      SONAR_JDBC_USERNAME: sonar
		      SONAR_JDBC_PASSWORD: sonar
		    volumes:
		      - sonarqube_data:/opt/sonarqube/data
		      - sonarqube_extensions:/opt/sonarqube/extensions
		      - sonarqube_logs:/opt/sonarqube/logs
		
		  db:
		    image: postgres:13
		    container_name: postgres-sonar
		    environment:
		      POSTGRES_USER: sonar
		      POSTGRES_PASSWORD: sonar
		      POSTGRES_DB: sonarqube
		    volumes:
		      - postgresql:/var/lib/postgresql/data
		
		volumes:
		  sonarqube_data:
		  sonarqube_extensions:
		  sonarqube_logs:
		  postgresql:
		```
		127.0.0.1:9000 접속 후 초기 설정
	2. Local Project 생성 후 토큰 발급
	3. 검사할 프로젝트 clone 및 환경설정
		- 테스트 진행한 프로젝트는 WPMS(Springboot + gradle)
		```build.gradle
		id "org.sonarqube" version '6.0.1.5171'
		
		sonar {
		        properties {
		                property 'sonar.projectKey', 'QUBE_TEST'
		                property 'sonar.host.url', 'http://localhost:9000'
		                property 'sonar.login', 'sqp_81addfaa473f585a4dac61c37a4db66a3d9fc9d5' // 발급받은  토큰 값
		                property "sonar.java.binaries", "build/classes"
		        }
		}
		
		```
	4. 빌드 진행
		- './gradlew build sonar'
	5. 결과 확인 (localhost:9000)

###### 04.10(목)
1. (NEXT-BLOG)
	1. Cursor 도입 
		1. middleware.ts 수정 설정
		2. 게시글 update 로직 구현
		3. logging 수정
	2. 레전드 상황발생
		4. 문제
			1. mongoDB 테스트 용으로 계정설정안해놓음
			2. All your data is backed up. You must pay 0.0045 BTC to bc1q7stxy9axrwmpu77kme55523a723spvcurnyt9x In 48 hours, your data will be publicly disclosed and deleted. (more information: go to http://2info.win/mdb)After paying send mail to us: rambler+1betfn@onionmail.org and we will provide a link for you to download your data. Your DBCODE is: 1BETFN
			3. 털림 ㅋㅋ
		5. 해결방안
			4. 보안그룹에서 포트를 내 PC만 적용
			5. mongodb 계정 설정
```
use admin
db.createUser({
	user: 'root',
	pwd: 'mongodbadmin',
	roles: [ 'root' ]
});

db.createUser({
	user: 'blogadmin',
	pwd: 'blogadmin',
	roles: [
		{ role: 'readWrite', db: 'blog' }
	]
});
```
	1. TO-DO
		1. 에러페이지
		2. 화면 전환
npx tailwindcss -i ./util/css/input/style.css -o ./util/css/output/style.css
npx tailwindcss -i ./public/css/input/style.css -o ./public/css/output/style.css

https://velog.io/@smat91/Docker%EC%95%88%EC%9D%98-MySQL-%EB%8D%B0%EC%9D%B4%ED%84%B0-Dump-exportimport

### Windows 외부 DNS 제거
Get-NetIPConfiguration
Get-DnsClientServerAddress
Set-DnsClientServerAddress -InterfaceAlias "Wi-Fi" -ResetServerAddresses

### CI/CD용 SSH 키 생성
1. ssh-keygen -t rsa -b 4096 -m PEM -f ~/.ssh/local.pem
2. cat ~/.ssh/local.pem.pub >> ~/.ssh/authorized_keys
3. chmod 700 ~/.ssh/
4. chmod 600 ~/.ssh/authorized_keys
5. chmod 600 ~/.ssh/local.pem
(FTP 설정)
6. apt-get install vsftpd
7. systemctl start vsftpd
(PowerShell)
8. ftp
9. open ${ip}