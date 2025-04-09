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
###### 04.09(수)
1. (NEXT-BLOG) 
	1. VM 마이그레이션
		1. GithubAction DockerHub 인증 오류
			next Error pull access denied for ---/next-blog, repository does not exist or may require 'docker login': denied: requested access to the resource is denied
			**=> YML 파일에 DockerHubId가 중복으로 기입되어있음**
	2. 코드 리팩터링
		1. BlobStorage 이미지 연동 확인
		2. 다크모드 CSS 수정
		3. 게시글 Update 로직 수정
		4. 로깅 수정
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
		```
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