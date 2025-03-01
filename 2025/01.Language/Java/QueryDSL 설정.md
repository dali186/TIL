##### 0. Entity, Repository 작성
##### 1. 의존성 추가
```build.gradle
implementation 'com.querydsl:querydsl-jpa:5.0.0:jakarta'  
annotationProcessor "com.querydsl:querydsl-apt:${dependencyManagement.importedProperties['querydsl.version']}:jakarta"  
annotationProcessor "jakarta.annotation:jakarta.annotation-api"  
annotationProcessor "jakarta.persistence:jakarta.persistence-api"
```
##### 2. Repository 객체 생성
- QueryDSL을 사용할 interface 생성 `DomainRepositoryDSL`
- 기존 Repository interface에 implement `public interface DomainRepository extends JpaRepository<Domain, Long>, DomainRepositoryDSL`
- QueryDSL inteface 작성 후 구현체 작성
