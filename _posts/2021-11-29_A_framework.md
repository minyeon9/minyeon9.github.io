---
layout: single
title: "Framework / Setting"
categories: ['Framework']
---

#### Framework
* 개발자가 소프트웨어를 개발함에 있어 코드를 구현하는 개발 시간을 줄이고,   
코드의 재사용성을 증가 시키기 위해 일련의 클래스 묶음이나 뼈대, 틀을 제공하는 라이브러리를 구현해 놓은 것을 말한다.

***

#### Framework의 특징
* 개발자가 따라야 하는 가이드를 제공한다.
* 개발할 수 있는 범위가 정해져 있다.
* 개발자를 위한 다양한 도구, 플러그인들을 지원한다.
   
|장점|단점|
|-----|-----|
|개발 시간 감소|습득 시간 소요|
|정형화되어 있기 때문에 일정 수준 이상의 품질 기대 가능||
|비교적 쉬운 유지 보수||
   
***

#### Framework 종류
|구분|설명|종류|
|---|---------|-----|
|영속성|데이터의 저장, 조회, 변경, 삭제를 다루는 클래스 및 설정 파일들을 라이브러리화하여 구현한 프레임워크|Mybatis, Hibernate|
|자바|Java EE를 통한 웹 어플리케이션 개발에 초점을 맞추어 필요한 요소들을 모듈화 하여 제공하는 프레임워크|Spring Framework, 전자정부표준 - Spring, Struts|
|화면 구현|Front-End를 보다 쉽게 구현할 수 있게 틀을 제공하는 프레임워크| Bootstrap, Foundation, MDL|
|기능 및 지원|특정 기능이나 업무 수행에 도움을 줄 수 있는 기능을 제공하는 프레임워크|Log4j, JUnit 5, ANT, Maven, Gradle|
   
***

#### Setting
* [Spring Tools]
* 실습 때는 3버전을 다운로드 받았음
* 4버전 사용 시, Legacy Project 사용 불가
    * 플러그인으로 3를 다운 받아서 사용할 수 있으나 잘 안될 때도 있다고 함
    * 4버전은 Spring Boot에 최적화
* JDK-11 이상으로 사용할 것
   
[Spring Tools]: [https://spring.io/tools]
   
-
   
![Alt text](/assets/images/java/framework/setting01.jpg)   
   
-
   
![Alt text](/assets/images/java/framework/setting02.jpg)   
   
표시된 버전으로 다운 받기
   
-
   
![Alt text](/assets/images/java/framework/setting03.jpg)   
   
압축 풀고 해당 폴더로 들어가면 실행파일이 있다.   
이제 이걸로 실습 시작!
   
-
   
처음 이클립스 설정했던 것과 동일하게   
Encoding, Complier, Sever(tomcat) 설정 해주기.   
추가로 lombok도 추가해줬다. lombok 게시글에서 한 거랑 똑같음.
   
***

