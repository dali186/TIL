##### 1. 디렉터리 구조 설정
/root
	/`src` 
		/`main`
			 `java` 생성 (com.example.demo)
			 `resources 생성
			 `webapp` 생성
		 /test 
##### 2. pom.xml 작성
/
```
<project xmlns="http://maven.apache.org/POM/4.0.0"  
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  
    <!-- 기본 프로젝트 정보 -->  
    <modelVersion>4.0.0</modelVersion>  
    <groupId>com.dali186</groupId>  
    <artifactId>framework</artifactId>  
    <version>1.0-SNAPSHOT</version>  
    <packaging>war</packaging>  
  
    <!-- Spring Info (JDK, Version) -->  
    <properties>  
        <java.version>1.8</java.version>  
        <spring.version>5.3.22</spring.version>  
        <maven.compiler.source>1.8</maven.compiler.source>  
        <maven.compiler.target>1.8</maven.compiler.target>  
    </properties>  
    <dependencies>        <!-- Spring Core -->  
        <dependency>  
            <groupId>org.springframework</groupId>  
            <artifactId>spring-context</artifactId>  
            <version>${spring.version}</version>  
        </dependency>        <!-- Spring MVC -->  
        <dependency>  
            <groupId>org.springframework</groupId>  
            <artifactId>spring-webmvc</artifactId>  
            <version>${spring.version}</version>  
        </dependency>        <!-- Servlet API -->  
        <dependency>  
            <groupId>javax.servlet</groupId>  
            <artifactId>javax.servlet-api</artifactId>  
            <version>4.0.1</version>  
            <scope>provided</scope>  
        </dependency>    </dependencies>  
    <build>        <plugins>            <plugin>                <groupId>org.apache.maven.plugins</groupId>  
                <artifactId>maven-war-plugin</artifactId>  
                <version>3.3.2</version>  
            </plugin>        </plugins>    </build></project>
```
**mvn clean install** (mvn 다운로드 및 환경변수 설정 선행)
##### 3. web.xml 작성
src/main/webapp/WEB-INF/web.xml
