

# Chapter별 Check List
### 핵심 개념 이해
- [x] 관계형 데이터베이스와 자바
- [x] ORM 개요
- [x] ORM 패러다임 불일치
- [x] JPA 프로그래밍 1. 프로젝트 세팅
- [x] JPA 프로그래밍 2. 엔티티 타입 맵핑
- [x] JPA 프로그래밍 3. Value 타입 맵핑
- [x] JPA 프로그래밍 4. 관계 맵핑
- [x] JPA 프로그래밍 5. 엔티티 상태와 Cascade
- [x] JPA 프로그래밍 6. Fetch
- [x] JPA 프로그래밍 7. 쿼리
- [x] 스프링 데이터 JPA 원리
- [x] 핵심 개념 마무리

### 스프링 데이터 JPA 활용
- [x] 스프링 데이터 JPA 활용 파트 소개
- [x] 스프링 데이터 Common 1. 리포지토리
- [x] 스프링 데이터 Common 2. 인터페이스 정의하기
- [x] 스프링 데이터 Common 3. Null 처리
- [x] 스프링 데이터 Common 4. 쿼리 만들기
- [x] 스프링 데이터 Common 4. 쿼리 만들기 실습
- [x] 스프링 데이터 Common 6. 비동기 쿼리 메소드
- [x] 스프링 데이터 Common 7. 커스텀 리포지토리 만들기
- [x] 스프링 데이터 Common 8. 기본 리포지토리 커스터마이징
- [x] 스프링 데이터 Common 9. 도메인 이벤트
- [x] 스프링 데이터 Common 10. QueryDSL 연동
- [x] QueryDSL 연동 보강
- [x] 스프링 데이터 Common 11. 웹 기능 1부 소개
- [x] 스프링 데이터 Common 12. 웹 기능 2부 DomainClassConverter
- [x] 스프링 데이터 Common 13. 웹 기능 3부 Pageable과 Sort
- [x] 스프링 데이터 Common 14. 웹 기능 4부 HATEOAS
- [x] 스프링 데이터 Common 15. 정리
- [x] 스프링 데이터 JPA 1. JpaRepository
- [x] 스프링 데이터 JPA 2. JpaRepository.save() 메소드
- [x] 스프링 데이터 JPA 3. JPA 쿼리 메소드
- [x] 스프링 데이터 JPA 4. Sort
- [x] 스프링 데이터 JPA 5. Named Parameter와 SpEL
- [x] 스프링 데이터 JPA 6. Update 쿼리
- [x] 스프링 데이터 JPA 7. EntityGraph
- [x] 스프링 데이터 JPA 8. Projection
- [x] 스프링 데이터 JPA 9. Specifications
- [x] 스프링 데이터 JPA 10. Query by Example
- [x] 스프링 데이터 JPA 11. 트랜잭션
- [x] 스프링 데이터 JPA 12. Auditing
- [x] 스프링 데이터 JPA 마무리

출처: (스프링 데이터 JPA - 백기선) - 인프런
  

# Chapter별 Summary
## 핵심 개념 이해
#### 3. 관계형 데이터베이스와 자바
  * JDBC
      * (관계형) 데이터베이스와 자바의 연결 고리
      * ![image](https://user-images.githubusercontent.com/20143765/95673121-fd965600-0be0-11eb-8680-561c558e3cd0.png)
      * DataSource / DriverManager
      * Connection
      * PreparedStatement
  * SQL
      * DDL
      * DML
  * 무엇이 문제인가?
      * SQL을 실행하는 비용이 비싸다.
      * SQL이 데이터베이스 마다 다르다.
      * 스키마를 바꿨더니 코드가 너무 많이 바뀌네...
      * 반복적인 코드가 너무 많아.
      * 당장은 필요가 없는데 언제 쓸 줄 모르니까 미리 다 읽어와야 하나...
  * Postgresql docker 설치
      * docker run -p 5432:5432 -e POSTGRES_PASSWORD=pass -e POSTGRES_USER=keesun -e POSTGRES_DB=springdata --name postgres_boot -d postgres
      * docker exec -i -t postgres_boot bash
      * su - postgres
      * psql springdata
      * 데이터베이스 조회
          * \list
      * 테이블 조회
          * \dt
          
#### 4. ORM 개요
  * JDBC 대신 도메인 모델 사용하려는 이유?
      * 객체 지향 프로그래밍의 장점을 활용하기 좋으니까.
      * 각종 디자인 패턴
      * 코드 재사용
      * 비즈니스 로직 구현 및 테스트 편함.
  * ORM은 애플리케이션의 클래스와 SQL 데이터베이스의 테이블 사이의 맵핑 정보를 기술한 메타데이터를 사용하여, 자바 애플리케이션의 객체를 SQL 데이터베이스의 테이블에 자동으로 (또 깨끗하게) 영속화 해주는 기술입니다.
      * In a nutshell, object/relational mapping is the automated (and transparent) persistence of objects in a Java application to the tables in an SQL database, using metadata that describes the mapping between the classes of the application and the schema of the SQL database.
          * Java Persistence with Hibernate, Second Edition
  * ![image](https://user-images.githubusercontent.com/20143765/95673127-0ab34500-0be1-11eb-9658-725366936db9.png)

#### 5. 패러다임 불일치
  * 객체를 릴레이션에 맵핑하려니 발생하는 문제들과 해결책
  * 밀도(Granularity) 문제
      * ![image](https://user-images.githubusercontent.com/20143765/95673134-17379d80-0be1-11eb-83a6-1d0acbe3df39.png)
      * 릴레이션에도 UDT로 사용자 정의타입을 만들수 있다. 
      * ORM이 해결책을 제공해준다.
  * 서브타입(Subtype) 문제
      * ![image](https://user-images.githubusercontent.com/20143765/95673137-1acb2480-0be1-11eb-8e20-2ce6423c110a.png)
      * ORM에서는 해당 문제에 대해 다양한 해결책을 제공해주고 다형성을 지원하는 해결책도 있음.
  * 식별성(Identity) 문제
      * ![image](https://user-images.githubusercontent.com/20143765/95673139-1f8fd880-0be1-11eb-9340-0d360793b111.png)
  * 관계(Association) 문제
      * ![image](https://user-images.githubusercontent.com/20143765/95673141-23235f80-0be1-11eb-8c57-288a5ce1c67a.png)
      * 다대다 => ManyToMany, 일대다 => OneToMany, 일대일 => OneToOne
  * 데이터 네비게이션(Navigation)의 문제
      * ![image](https://user-images.githubusercontent.com/20143765/95673143-26b6e680-0be1-11eb-97d5-e92eb05d122c.png)
      * n+1 문제
          * 스터디 조회가 1
          * 각 스터디의 각 오너 조회가 n
          * 총합: n+1

