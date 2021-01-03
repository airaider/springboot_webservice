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
>   * 컨트롤러를 JSON을 반환하는 컨트롤러로 만들어 줌
>   * @ResponseBody를 각 메소드마다 선언했던 것을 한번에 사용할 수 있게 해줌
>2. @GetMapping
>   * HTTP Method인 Get의 요청을 받을 수 있는 API를 만들어 줌
>   * @RequestMapping(method = RequestMethod.GET)

* HelloControllerTest

> 1. 



### 2.3 Lombok



## 3장 : 스프링 부트에서 JPA로 데이터베이스 다뤄보자

You can rename the current file by clicking the file name in the navigation bar or by clicking the **Rename** button in the file explorer.

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

## 9장 : ㅋㅎ드가 푸시되면 자동으로 배포해 보자 - Travis CI 배포 자동화

You can delete the current file by clicking the **Remove** button in the file explorer. The file will be moved into the **Trash** folder and automatically deleted after 7 days of inactivity.

## 10장 : 24시간 365일 중단 없는 서비스를 만들자

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.

## 11장 : 1인 개발 시 도움이 될 도구와 조언들

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.

