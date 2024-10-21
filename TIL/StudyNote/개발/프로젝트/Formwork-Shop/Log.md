Spring boot 3.3.4
Java 17
Jar
MySQL 8.4
JPA

#### 작업 리스트
- [ ] SpringSecurity 연동
- [ ] SNS Login 연동
- [ ] 결제
- [ ] 메일 일괄 발송
- [ ] 기본 쇼핑몰
	- [ ] 
# Windows
### DataBase
1. MySQL 8.4 Community 설정
	- [MySQL Download](https://dev.mysql.com/downloads/mysql/)
		- root / mysql
```
# Database 생성
CREATE DATABASE shop_db CHARACTER SET utf8 COLLATE utf8_general_ci;
# 계정 생성 (내부/외부)
CREATE USER 'shop_loc'@'localhost' IDENTIFIED BY 'shop12!@';
GRANT ALL PRIVILEGES ON shop_db.* TO 'shop_loc'@'localhost';
FLUSH PRIVILEGES;

CREATE USER 'shop_ext'@'%' IDENTIFIED BY 'shop12!@';
GRANT ALL PRIVILEGES ON shop_db.* TO 'shop_ext'@'%';
FLUSH PRIVILEGES;
```

```
application.yml
spring:  
  jpa:  
    database: mysql  
    hibernate.ddl-auto: update  
    show-sql: true  
  datasource:  
    driver-class-name: com.mysql.cj.jdbc.Driver  
    url: jdbc:mysql://localhost:3306/shop_db?serverTimezone=Asia/Seoul  
    username: shop_loc 
    password: shop12!@
```
