

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
      * ![image](https://user-images.githubusercontent.com/20143765/95673154-3df5d400-0be1-11eb-952d-5fa85ff00199.png)
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

#### 6. JPA 프로그래밍: 프로젝트 세팅
  * 데이터베이스 실행
      * PostgreSQL 도커 컨테이너 재사용
      * docker start postgres_boot
  * 스프링 부트
      * 스프링 부트 v2.*
      * 스프링 프레임워크 v5.*
  * 스프링 부트 스타터 JPA
      * JPA 프로그래밍에 필요한 의존성 추가
          * JPA v2.*
          * Hibernate v5.*
      * 자동 설정: HibernateJpaAutoConfiguration
          * 컨테이너가 관리하는 EntityManager (프록시) 빈 설정
          * PlatformTransactionManager 빈 설정
          * JPA를 사용하는 데 필요한 모든 빈들이 자동으로 등록된다.
  * application.properties
      * JDBC 설정
          * spring.datasource.url=jdbc:postgresql://localhost:5432/springdata
          * spring.datasource.username=keesun
          * spring.datasource.password=pass
      * spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
          * 불필요함
      * spring.jpa.hibernate.ddl-auto=create
          * 개발할때는 update를 사용하는게 편하지만 주의할점
              * Entity 객체에서 필드를 추가하면 테이블에도 필드가 추가됨. 하지만 Entity 객체에서 필드를 삭제해도 테이블에선 사라지지 않아서 지저분해질수 있다.
  * JPA, Hibernate API 사용해보기
  * ```
    @Transactional
    @Component
    public class JpaRunner implements ApplicationRunner {
        @PersistenceContext
        EntityManager entityManager;


        @Override
        public void run(ApplicationArguments args) throws Exception {
            Account account = new Account();
            account.setUsername("junho");
            account.setPassword("jpa");


            // jpa
    //        entityManager.persist(account);


            // hibernate
            Session session = entityManager.unwrap(Session.class);
            session.save(account);
        }
    }
    ```

#### 7. JPA 프로그래밍: 엔티티 매핑
  * @Entity
      * “엔티티”는 객체 세상에서 부르는 이름.
      * 보통 클래스와 같은 이름을 사용하기 때문에 값을 변경하지 않음.
      * 엔티티의 이름은 JQL에서 쓰임.
      * 엔티티의 이름은 테이블 이름과 별개
  * @Table
      * “릴레이션" 세상에서 부르는 이름.
      * @Entity의 이름이 기본값.
      * 테이블의 이름은 SQL에서 쓰임.
      * 특정 DB에서는 User 테이블을 만들수 없음(대표적으로 postgresql)
          * 클래스 이름을 User라고 하고 Entity의 name 속성에 users(user는 마찬가지로 안됨)라고 해도 됨. 하지만 설정을 줄이기 위해 Account라고 씀
  * @Id
      * 엔티티의 주키를 맵핑할 때 사용.
      * 자바의 모든 primitive 타입과 그 랩퍼 타입을 사용할 수 있음
          * 보통 랩퍼 타입을 사용한다
      * Date랑 BigDecimal, BigInteger도 사용 가능.
      * 복합키를 만드는 맵핑하는 방법도 있지만 그건 논외로..
  * @GeneratedValue
      * 주키의 생성 방법을 맵핑하는 애노테이션
      * 생성 전략과 생성기를 설정할 수 있다.
      * 기본 전략은 AUTO: 사용하는 DB에 따라 적절한 전략 선택
          * postgres는 기본적으로 SEQUENCE
      * TABLE, SEQUENCE, IDENTITY 중 하나.
  * @Column
      * unique
      * nullable
      * length
      * columnDefinition
          * sql문법을 사용해서 등록해야할경우
      * * ...
  * @Temporal
      * 현재 JPA 2.1까지는 Date와 Calendar만 지원.
  * @Transient
      * 컬럼으로 맵핑하고 싶지 않은 멤버 변수에 사용.
      * Getter, Setter는 없어도 컬럼으로 매핑됨
  * spring.jpa.hibernate.ddl-auto=update로 하면 중간에 column타입등을 바꿔도 적용되지 않음
  * application.properties
      * 직접 매번 console 들어가서 확인해야 하나? No!
      * spring.jpa.show-sql=true
          * 어떤 sql이 날라가는지 볼수 있음
      * spring.jpa.properties.hibernate.format_sql=true
          * 좀더 읽기 쉽게 formatting
          
#### 8. JPA 프로그래밍: Value 타입 매핑
  * 엔티티 타입과 Value 타입 구분
      * 식별자가 있어야 하는가. 독립적으로 존재해야 하는가.
          * => 엔티티 타입
  * Value 타입 종류
      * 기본 타입 (String, Date, Boolean, ...)
      * Composite Value 타입
      * Collection Value 타입
          * 기본 타입의 콜렉션
          * 컴포짓 타입의 콜렉션
  * Composite Value 타입 맵핑
      * @Embeddable
          * 임베디드할 객체에 붙임
      * @Embedded
          * @Entity 클래스에 붙임
      * @AttributeOverrides
      * @AttributeOverride
          * ![image](https://user-images.githubusercontent.com/20143765/95673175-6b428200-0be1-11eb-8869-04305ad9e8f6.png)
          * street name이라는 객체 필드를 home_street 테이블 필드로 매핑한다.

#### 9. JPA 프로그래밍: 1대다 맵핑
  * 관계에는 항상 두 엔티티가 존재 합니다.
      * 둘 중 하나는 그 관계의 주인(owning)이고
      * 다른 쪽은 종속된(non-owning) 쪽입니다.
      * 해당 관계의 반대쪽 레퍼런스를 가지고 있는 쪽이 주인.
  * 단방향에서의 관계의 주인은 명확합니다.
      * 관계를 정의한 쪽이 그 관계의 주인입니다.
  * 단방향 @ManyToOne
      * 기본값은 FK 생성
      * Study Entity 객체내에 Account owner필드에 @ManyToOne를 붙이면 주인은 Study
  * 단방향 @OneToMany
      * 기본값은 조인 테이블 생성
      * account_studies라는 테이블 자동 생성
  * 양방향
      * Study에 owner Account가 있고 Account에는 studies Set<Study>가 있는것이 양방향
          * Study Entity > owner Account필드 에 ManyToOne, Account Entity > studies Set<Study>필드에 OneToMany로 하면 양방향이 아님. 단방향이 두개인거
      * 양방향으로 만들려면 OneToMany쪽에 mappedBy 속성에 관계를 정의한 필드를 적어줘야함(=> owner)
          * ![image](https://user-images.githubusercontent.com/20143765/95673192-8f05c800-0be1-11eb-9541-c2d06d778225.png)
      * FK 가지고 있는 쪽이 오너 따라서 기본값은 @ManyToOne 가지고 있는 쪽이 주인.
      * 주인이 아닌쪽(@OneToMany쪽)에서 mappedBy 사용해서 관계를 맺고 있는 필드를 설정해야 합니다.
  * 양방향
      * @ManyToOne (이쪽이 주인)
      * @OneToMany(mappedBy)
      * 주인한테 관계를 설정해야 DB에 반영이 됩니다.
  * 아래 두줄 코드는 한 묶음이 되어야 한다.
      * ![image](https://user-images.githubusercontent.com/20143765/95673194-92994f00-0be1-11eb-87f3-860955cf3bf1.png)
      * 컨베니언트 메서드
      * ```
        public void addStudy(Study study) {
            this.getStudies().add(study);
            study.setOwner(this);
        }


        public void removeStudy(Study study) {
            this.getStudies().remove(study);
            study.setOwner(null);
        }
        ```


#### 10. JPA 프로그래밍: 엔티티 상태와 Cascade
  * 엔티티의 상태 변화를 전파 시키는 옵션.
      * Study에 상태가 변할때 Account상태가 변하도록 전파하고 싶다. 이때 ManyToOne or OneToMany에 cascade 옵션
  * 잠깐? 엔티티의 상태가 뭐지?
      * Transient: JPA가 모르는 상태
      * Persistent: JPA가 관리중인 상태 (1차 캐시, Dirty Checking, Write Behind, ...)
          * 1차 캐시
              * session이라는 Persistent Context에 저장된것임(session(hibernate API) or EntityManager(JPA API))
              * Account keesun = session.load(Account.class, account.getId());
                  * 이 시점엔 select 쿼리가 발생하지 않고 캐시에서 꺼냄
              * 관리중인 객체라는 의미는 변경사항을 계속 모니터링한다는것
              * dirtyChecking: 이 객체의 변경사항을 계속 감지
              * Write behind: 객체의 상태변화를 최대한 늦게(필요한 시점)에 적용
      * ```
        Account account = new Account();
        account.setUsername("junho");
        account.setPassword("jpa");

        Study study = new Study();
        study.setName("Spring Data Jpa");

        study.setOwner(account);
        account.getStudies().add(study);
        // jpa
        // entityManager.persist(account);

        // hibernate
        Session session = entityManager.unwrap(Session.class);
        session.save(account);
        session.save(study);
        
        Account keesun = session.load(Account.class, account.getId());
        keesun.setUsername("asdasd”); 
        keesun.setUsername("asdasd2”); 
        keesun.setUsername("asdasd3”); // dirty Checking, Write Behind
        System.out.println("-----------");
        System.out.println(keesun.getUsername());
        ```
      * Detached: JPA가 더이상 관리하지 않는 상태.
          * 트랜잭션이 끝나서 session 밖으로 나왔을떄
              * 예를 들어 Service에서 Repository 호출하고 Repository에서 트랜잭션이 끝남, 서비스에서 이 객체를 쓸땐 JPA, hibernate가 관리하는 객체가 아니다.(1차 캐시, dirty checking, write behind 발생 안함
              * Re attach를 사용해서 다시 persistent상태로 만듬
      * Removed: JPA가 관리하긴 하지만 삭제하기로 한 상태.
  * ![image](https://user-images.githubusercontent.com/20143765/95673212-b9f01c00-0be1-11eb-9fb0-ddb38f339c19.png)

      * save를 했다고 해서 바로 DB에 들어간게(insert query 발생 X) 아님, hibernate가 persistent 상태로 관리하고 있다가 때가 되면 insert
  * Post, Comment(Parent, Child 구조)를 이용한 Cascade
      * Post OneToMany에 cascade 옵션을 줘야 Comment 테이블에 데이터가 들어감.
      * Cascade옵션을 여러개를 줄수 있음. Persistent, Removed(삭제 시점에도 반영되도록)
  * ```
    @Override
    public void run(ApplicationArguments args) throws Exception {
        Post post = new Post();
        post.setTitle("Spring Data Jpa 언제 보나..");

        Comment comment = new Comment();
        comment.setComment("빨리 보고 싶어요");
        post.addComment(comment);

        Comment comment2 = new Comment();
        comment2.setComment("빨리 보고 싶어요2");
        post.addComment(comment2);

        Session session = entityManager.unwrap(Session.class);
        session.save(post);

        // REMOVE Cascade
        // Post post = session.get(Post.class, 1L);
        // session.delete(post);
    }
    
    @Entity
    public class Post {
        @Id
        @GeneratedValue
        private Long id;
        private String title;

        @OneToMany(mappedBy = "post", cascade = {CascadeType.PERSIST, CascadeType.REMOVE}) // 여기에 cascade 옵션을 여러개를 지정 가능
        private Set<Comment> comments = new HashSet<>();

        public void addComment(Comment comment) {
            this.getComments().add(comment);
            comment.setPost(this);
        }
        
        public Long getId() {
            return id;
        }

        public void setId(Long id) {
            this.id = id;
        }

        public String getTitle() {
            return title;
        }

        public void setTitle(String title) {
            this.title = title;
        }

        public Set<Comment> getComments() {
            return comments;
        }

        public void setComments(Set<Comment> comments) {
            this.comments = comments;
        }
    }

    @Entity
    public class Comment {
        @Id
        @GeneratedValue
        private Long id;
        private String comment;

        @ManyToOne
        private Post post;

        public Long getId() {
            return id;
        }

        public void setId(Long id) {
            this.id = id;
        }

        public String getComment() {
            return comment;
        }

        public void setComment(String comment) {
            this.comment = comment;
        }

        public Post getPost() {
            return post;
        }

        public void setPost(Post post) {
            this.post = post;
        }
    }
    ```

#### 11. JPA 프로그래밍: Fetch
  * 연관 관계의 엔티티를 어떻게 가져올 것이냐... 지금 (Eager)? 나중에(Lazy)?
      * @OneToMany의 기본값은 Lazy
      * @ManyToOne의 기본값은 Eager
  * @OneToMany에서 comment list 바로 가져오기
      * @OneToMany(mappedBy = "post", cascade = CascadeType.ALL, fetch = FetchType.EAGER)
  * post 타이틀과 post에 해당 하는 각 comment 가져오기
      * n+1이 재현되지 않는다. hibernate가 똑똑해졌다..
  * ```
    Post post = session.get(Post.class, 1L);
    System.out.println(post.getTitle());


    post.getComments().forEach(c -> {
        System.out.println(c.getComment());
    });
    ```

#### 12. JPA 프로그래밍: Query
    * JPQL (HQL)
        * Java Persistence Query Language / Hibernate Query Language
        * 데이터베이스 테이블이 아닌, 엔티티 객체 모델 기반으로 쿼리 작성.
        * JPA 또는 하이버네이트가 해당 쿼리를 SQL로 변환해서 실행함.
        * https://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#hql
        * ![image](https://user-images.githubusercontent.com/20143765/95673268-13584b00-0be2-11eb-92fa-a42e21262954.png)
            * Comment 왜가져오지?
                * toString떄문..
        * 단점: 타입세이프 하지 않음.
    * Criteria
        * 타입 세이프 쿼리
        * https://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#criteria
        * ![image](https://user-images.githubusercontent.com/20143765/95673271-16533b80-0be2-11eb-8afd-41fe937e9310.png)
    * Named query 사용
        * ![image](https://user-images.githubusercontent.com/20143765/95673272-19e6c280-0be2-11eb-8b96-9e1cbb9fb768.png)
        * ![image](https://user-images.githubusercontent.com/20143765/95673276-1d7a4980-0be2-11eb-9215-8e066f3ace82.png)
    * Native Query
        * SQL 쿼리 실행하기
        * https://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#sql
        * ![image](https://user-images.githubusercontent.com/20143765/95673277-21a66700-0be2-11eb-99c1-10801e7a4e7e.png)

#### 13. 스프링 데이터 JPA 소개 및 원리
  * 기존 방식
  * ```
    @Repository
    public class PostRepository {
        @PersistenceContext
        private EntityManager entityManager;


        public Post add(Post post) {
            entityManager.persist(post);
            return post;
        }


        public void delete(Post post) {
            entityManager.detach(post);
        }


        public List<Post> findAll() {
            return entityManager.createQuery("SELECT p FROM Post As p", Post.class)
                    .getResultList();
        }
    }
    ```

  * JpaRepository<Entity, Id> 인터페이스
      *  매직 인터페이스
      * @Repository가 없어도 빈으로 등록해 줌.
  * @EnableJpaRepositories
      * 매직의 시작은 여기서 부터
      * 원래 @Configuration붙은 클래스에 @EnableJpaRepositories를 붙여줘야하는데 Spring boot에서 자동으로 붙여줌(자동 설정에 의해)
  * 매직은 어떻게 이뤄지나? 
      * 시작은 @Import(JpaRepositoriesRegistrar.class)
          * 얘가 JpaRepsitory들을 빈으로 등록해줌
          * 
      * 핵심은 ImportBeanDefinitionRegistrar 인터페이스
          * 프로그래밍적으로 빈을 등록해줌
      * ```
        public class KeesunRegister implements ImportBeanDefinitionRegistrar {
            @Override
            public void registerBeanDefinitions(AnnotationMetadata importingClassMetadata, BeanDefinitionRegistry registry, BeanNameGenerator importBeanNameGenerator) {
                GenericBeanDefinition beanDefinition = new GenericBeanDefinition();;
                beanDefinition.setBeanClass(Keesun.class);
                beanDefinition.getPropertyValues().add("name", "pury");


                registry.registerBeanDefinition("keesun", beanDefinition);
            }
        }


        public class Keesun {


            private String name;


            public String getName() {
                return name;
            }


            public void setName(String name) {
                this.name = name;
            }
        }

        @Import(KeesunRegister.class)
        를 해주면 Keesun 객체가 빈으로 등록됨
        ```


----

## 스프링 데이터 JPA 활용
#### 15. 스프링 데이터 JPA 활용 파트 소개
  * ![image](https://user-images.githubusercontent.com/20143765/95673322-6205e500-0be2-11eb-8ea2-2c02ab0ec308.png) 
  * ![image](https://user-images.githubusercontent.com/20143765/95673324-6500d580-0be2-11eb-99af-747bc1d26c19.png)
      * 스프링 데이터 common
          * Reposity를 생성해서 빈으로 등록하는 방법 or 쿼리메서드를 만드는 기본 메커니즘이 들어있음
  * http://projects.spring.io/spring-data/
