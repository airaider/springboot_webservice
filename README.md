# 스프링 부트와 AWS로 혼자 구현하는 웹 서비스

<img src="/img/book.jpg"></img>

이동욱 지음

<br>
****

## 1장 : 인텔리제이로 스프링 부트 시작하기



### 1.1. 인텔리제이의 장점 (이클립스에 비해)

	1. 추천 기능 (Smart Completion)
	2. 다양한 리팩토링, 디버깅
	3. 이클립스 Git에 비해 높은 자유도
	4. 프로젝트 시작 시, 인덱싱을 지원해 빠른 파일 검색 속도
	5. HTML, CSS, JS< XML 기능 지원
	6. 자바, 스프링 부트 버전업에 맞춘 빠른 업데이트



### 1.2. Gradle 설정

#### repositories

> ### mavenCentral
>
> * 이전부터 많이 쓰인 저장소
> * 라이브러리 업로드 시, 많은 과정 및 설정 필요

> ### jcenter
>
> * 라이브러리 업로드 간다화
> * jcenter에 라이브러리 업로드 -> mavenCentral에도 업로드 (자동화)





****


## 2장 : 스프링 부트에서 테스트 코드를 작성하자

<br>

### 2.1. TDD 와 단위 테스트(unit test)

####  Test Driven Development

<img src="/img/tdd.png"></img>

	1. 항상 실패하는 테스트를 먼저 작성하고 (Red)
	2. 테스트가 통과하는 프로덕션 코드를 작성하고 (Green)
	3. 테스트가 통과하면 프로덕션 코드를 리팩토링합니다 (Refactor)



#### 단위 테스트

	1. 빠른 피드백
	2. 자동 검증
	3. 시존 기능이 잘 작동되는 것을 보장
	
	* Java - JUnit
	* DB - DBUnit
	* C++ - CPPUnit
	* .net - NUnit



### 2.2 Application

#### @SpringBootApplication

스프링 부트의 자동 설정, 스프링 Bean 읽기와 생성을 모두 자동으로 설정

@SpringBootApplication이 있는 위치부터 설정을 읽어가기 때문에 **프로젝트의 최상단**에 위치해햐 합니다



#### 내장 WAS (Web Application Server)

별도로 외부에 WAS를 두지 않고 애플리케이션을 실행할 때 재부에서 WAS를 실행

서버에 톰캣(TomCat)을 설치할 필요가 없다

스프링 부트로 만들어진 Jar 파일로 실행

**언제 어디서나 같은 환경에서 스프링 부트를 배포**



#### 코드 설명

* HelloController

>1. @RestController
>   - 컨트롤러를 JSON을 반환하는 컨트롤러로 만들어 줌
>   - @ResponseBody를 각 메소드마다 선언했던 것을 한번에 사용할 수 있게 해줌
>
>2. @GetMapping
>   - HTTP Method인 Get의 요청을 받을 수 있는 API를 만들어 줌
>   - @RequestMapping(method = RequestMethod.GET)

* HelloControllerTest

> 1. @RunWith(SpringRunner.class)
>    - JUnit에 내장된 실행자 외에 SpringRunner 실행자 실행
>    - JUnit <-> 스프링 부트 테스트와 연결자 역할
>
> 2. @WebMvcTest
>    - @Controller, @ControllerAdvice 선언
>
> 3. @Autowired
>    - 스프링이 관리하는 빈(Bean) 주입
>
> 4. @private MockMvc mvc
>    - 웹 API 테스트할 때 사용
>    - 스프링 MVC 테스트의 시작점
>    - HTTP GET, POST 등에 대한 API 테스트 가능
>
> 5. mvc,perform(status.isOK())
>    - Mockmvc를 통해 /hello 주소로 HTTP GET 요청을 한다
>
> 6. .andExpect(status().isOk())
>    - mvc.perform의 결과를 검증한다
>    - HTTP Header의 Status를 검증한다
>
> 7. .andExpect(content().string(hello))
>    - mvc.perform의 결과를 검증
>    - 응답 본문의 내용을 검증



### 2.3 Lombok

자바 개발에 자주 사용하는 코드 Getter, Setter, 기본생성자, toString 등을 어노테이션으로 자동 생성

#### 코드 설명

* HelloResponseDto

> 1. @Getter
>    - 선언된 모든 필드의 get 메소드를 생성
> 2. @RequiredArgsConstructor
>    - 선언된 모든 final 필드가 포함된 생성자를 생성
>    - final이 없는 필드는 생성자에 포함되지 않는다

- HelloResponseDtoTest

> 1. asserThat
>
>    - 테스트 검증 라이브러리(assertj)의 검증 메소드
>    - 검증하고 싶은 대상을 베소드 인자로 받습니다
>    - 메소드 체이닝이 지원되어 isEqualTo와 같이 메소드를 이어서 사용 가능
>
> 2. isEqualTo
>
>    - assertj의 동등 비교 메소드
>    - assertThat에 있는 값과 isEqualTo의 값을 비교해서 같을 때만 성공
>
>    #### assertj
>
>    * coreMatchers와 달리 추가적인 라이브러리 불필요
>    * 자동완성이 좀 더 확실히 지원됨 (Junit 비교시)

- ResponseDto

> 1. @RequestParam
>    - 외부에서 API로 넘긴 파라미터를 가져오는 어노테이션

- HelloControllerTest

> 1. param
>    - API 테스트할 때 사용될 요청 파라미터를 설정
>    - String만 허용
>    - 숫자/날짜 등의 데이터도 등록될 때는 문자열로 변경해야만 가능
> 2. jsonPath
>    - JSON 응답값을 필드별로 검증할 수 있는 메소드
>    - $를 기준으로 필드명을 명시
>    - $.name, $.amount





## 3장 : 스프링 부트에서 JPA로 데이터베이스 다뤄보자

#### JPA(Java Persistence API) / ORM(Object Relational Mapping)

	1. iBatis, myBatis는 Mapper를 활용하여 데이터베이스 쿼리 작성
	2. SQL 다루는 시간이 너무 많다
	3. 객체지향 프로그래밍 >>> 테이블 모델링
	4. 패러다임 불일치
	5. SQL에 종속적인 개발을 하지 않아도 된다
	
	* JPA <- Hibernate <- Spring Data JPA
	* 구현체 교체의 용이성
	* 저장소 교체의 용이성



#### h2

	1. 인메모리 관계형 데이터베이스
	2. 프로젝트 의존성
	3. 애플리케이션 재시작 마다 초기화 -> 테스트에 용이



#### 코드 설명

* Posts

> 1. @Entity
>
>    - 테이블과 링크될 클래스
>
>    - 기본값으로 클래스의 카멜케이스 -> 언더스코어 네이밍으로 테이블 매칭
>
>      ex) SalesManager.java -> sales_manager table
>
> 2. @Id
>
>    - 해당 테이블의 PK 필드
>
> 3. @GeneratedValue
>
>    - PK의 생성 규칙
>    - GenerationType.IDENTITY -> auto_increment
>
> 4. @Column
>
>    - 해당 클래스의 필드는 모두 칼럼
>    - 기본값 외에 추가로 변경이 필요한 옵션이 있으면 사용

- PostsRepositoryTest

> 1. @After
>    - Junit에서 단위 테스트가 끝날 때마다 수행되는 메소드를 저장
>    - 배포 전 전체 테스트를 수행할 때 테스트간 데이터 침범을 막기 위해 사용
>    - H2에 담겨있는 데이터 초기화를 위해
> 2. postsRepository.save
>    - 테이블 posts에 insert/update 쿼리를 실행합니다
>    - id 값이 있다면 update, 없다면 insert 쿼리를 실행
> 3. postsRepository.findAll
>    - 테이블 posts에 있는 모드 데이터를 조회해오는 메소드


#### Repository

	1. iBatis, MyBatis에서 DAO로 불리는 DB Layer 접근자
	2. Interface로 생성
	3. JpaRepository<Entity 클래스, PK 타입> 을 통해 기본적인 CRUD 생성
	4. Entity 클래스와 기본 Entity Repository는 함께 위치해야 한다
	5. 도메인 패키지에서 함께 관리


#### Setter 메소드를 무작정 추가하지 않는 이유

	1. 인스턴스 값의 변경을 코드상 어디서 하는지 명확하지 않아서
	2. 차후 기능 변경 시 복잡해짐
	3. 값 변경이 필요하면 명확히 그 목적과 의도를 나타내는 메소드를 추가해야함
	4. 생성자를 통해 최종값을 채운 후 DB에 삽입
	5. @Builder를 통해 관리



#### API

	1. Request 데이터를 받을 Dto
	2. API 요청을 받은 Controller
	3. 트랜잭션, 도메인 기능 간의 순서를 보장하는 Service



<img src="/img/spring.png"></img>

	* Web Layer
		- @Controller, JSP/Freemarker 등의 뷰 템플렛 영역
		- @Filter, 인터셉터, 컨트롤러 어드바이스(@ControllerAdvice) 외부 요청과 응답에 대한 전반적인 영역
	* Service Layer
		- @Service에 사용되는 서비스 영역
		- Contoller와 Dao의 중간 영역에서 사용
		- @Transactional이 사용되어야 하는 영역
	* Repository Layer
		- Database와 같이 데이터 저장소에 접근하는 영역
		- Dao(Data Access Object) 영역
	* Dtos
		- Dto(Data Transfer Object)는 계층 간에 데이터 교환을 위한 객체
	* Domain Model
		- 개발 대상을 모든 사람이 동일한 관점에서 이해할 수 있고 공유할 수 있도록 단순화시킨 것
		- @Entity
		- VO
		- 비즈니스 처리





## 4장 : 머스테치로 화면 구성하기

You can delete the current file by clicking the **Remove** button in the file explorer. The file will be moved into the **Trash** folder and automatically deleted after 7 days of inactivity.

## 5장 : 스프링 시큐리티와 OAuth 2.0으로 로그인 기능 구현하기

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.

## 6장 : AWS 서버 환경을 만들어보자 - AWS EC2

The file explorer is accessible using the button in left corner of the navigation bar. You can create a new file by clicking the **New file** button in the file explorer. You can also create folders by clicking the **New folder** button.

## 7장 : AWS에 데이터베이스 환경을 만들어보자 - AWS RDS

All your files and folders are presented as a tree in the file explorer. You can switch from one to another by clicking a file in the tree.

## 8장 : EC2 서버에 프로젝트를 배포해 보자

You can rename the current file by clicking the file name in the navigation bar or by clicking the **Rename** button in the file explorer.

## 9장 : 코드가 푸시되면 자동으로 배포해 보자 - Travis CI 배포 자동화

You can delete the current file by clicking the **Remove** button in the file explorer. The file will be moved into the **Trash** folder and automatically deleted after 7 days of inactivity.

## 10장 : 24시간 365일 중단 없는 서비스를 만들자

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.

## 11장 : 1인 개발 시 도움이 될 도구와 조언들

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.

