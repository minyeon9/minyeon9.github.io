---
layout: single
title: "Spring - 프로젝트 세팅"
categories: ['Framework']
---

#### Spring DI 실습
* Spring Legacy Project로 프로젝트 생성
   
***

#### Java 버전 및 spring framework 버전 변경
* POM.xml
* [Spring] > Project > Spring Framework > 최신버전
* 수업 때는 5.3.14 버전이 최신이었는데 벌써 업데이트 됐네..
   
![Alt text](/assets/images/framework/spring/di/spring_di01.jpg)   
   
``` xml
<properties>
    <java-version>11</java-version>
    <org.springframework-version>5.3.14</org.springframework-version>
    <org.aspectj-version>1.6.10</org.aspectj-version>
    <org.slf4j-version>1.6.6</org.slf4j-version>
</properties>
```   
   
-
   
``` xml
<dependencies>
    <!-- Spring -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>${org.springframework-version}</version>
        <exclusions>
            <!-- Exclude Commons Logging in favor of SLF4j -->
            <exclusion>
                <groupId>commons-logging</groupId>
                <artifactId>commons-logging</artifactId>
                </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>${org.springframework-version}</version>
    </dependency>

    <!-- ... -->
</dependencies>
```   
   
spring-context / spring-webmvc 버전은
위에서 설정한 버전으로 자동으로 세팅된다.
   
***

#### Servlet / Servlet JSP 버전 수정
* [Maven repository]에서 servlet / Servlet jsp 검색
   
``` xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
    <scope>provided</scope>
</dependency>
<dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>javax.servlet.jsp-api</artifactId>
        <version>2.3.3</version>
        <scope>provided</scope>
    </dependency>
```
   
***

#### JSTL 라이브러리 추가
* [Maven repository]에서 taglibs 검색
   
``` xml
<dependency>
    <groupId>org.apache.taglibs</groupId>
    <artifactId>taglibs-standard-impl</artifactId>
    <version>1.2.5</version>
</dependency>

<dependency>
    <groupId>org.apache.taglibs</groupId>
    <artifactId>taglibs-standard-spec</artifactId>
    <version>1.2.5</version>
</dependency>

<dependency>
    <groupId>org.apache.taglibs</groupId>
    <artifactId>taglibs-standard-jstlel</artifactId>
    <version>1.2.5</version>
</dependency>

<dependency>
    <groupId>org.apache.taglibs</groupId>
    <artifactId>taglibs-standard-compat</artifactId>
    <version>1.2.5</version>
</dependency>
```
   
***

### Maven eclipse plugin 버전 수정
   
``` xml
<plugin>
    <artifactId>maven-eclipse-plugin</artifactId>
    <version>2.10</version> <!-- 여기 -->
    <configuration>
        <additionalProjectnatures>
            <projectnature>org.springframework.ide.eclipse.core.springnature</projectnature>
        </additionalProjectnatures>
        <additionalBuildcommands>
            <buildcommand>org.springframework.ide.eclipse.core.springbuilder</buildcommand>
        </additionalBuildcommands>
        <downloadSources>true</downloadSources>
        <downloadJavadocs>true</downloadJavadocs>
    </configuration>
</plugin>
```
   
***

#### Maven compiler plugin 버전 수정
* [Maven repository]에서 Maven compiler plugin 검색
* Java 버전은 위에서 설정한 버전으로 자동 세팅되도록 했다.
   
``` xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.8.1</version> <!-- 검색한 버전 -->
    <configuration>
        <source>${java-version}</source> <!-- Java 버전 -->
        <target>${java-version}</target> <!-- Java 버전 -->
        <compilerArgument>-Xlint:all</compilerArgument>
        <showWarnings>true</showWarnings>
        <showDeprecation>true</showDeprecation>
    </configuration>
</plugin>
```
   
***

#### JSTL 라이브러리 직접 추가
* maven을 사용하여 pom.xml에 추가를 했지만 이클립스의 오류라고 한다. 그래서 라이브러리를 직접 추가해줬다.
   
![Alt text](/assets/images/framework/spring/di/spring_di02.jpg)   
   
프로젝트 내에 잘 들어가 있지만..! 직접 추가가 필요하다고 하신다.   
   
-
   
![Alt text](/assets/images/framework/spring/di/spring_di03.jpg)   
   
lib 폴더를 생성하여 추가했다.   
   
***

#### Encoding 필터 등록 / 매핑
* 기존 : Encoding 필터 생성
* 이제는 스프렝에서 제공하는 필터를 web.xml에 등록한다.
   
``` xml
<filter> 
    <filter-name>encodingFilter</filter-name> 
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class> 
    <init-param> 
        <param-name>encoding</param-name> 
        <param-value>UTF-8</param-value> 
    </init-param> 
    <init-param> 
        <param-name>forceEncoding</param-name> 
        <param-value>true</param-value> 
    </init-param> 
</filter> 
<filter-mapping> 
    <filter-name>encodingFilter</filter-name> 
    <url-pattern>/*</url-pattern> 
</filter-mapping>
```
   
***

#### 프로젝트 실행
* 이 경로는 사실 http://localhost:8089/di/WEB-INF/view/home.jsp 인데 WEB-INF는 직접 접근 불가
* HomeController에서 처리해서 home.jsp를 열어줌
   
![Alt text](/assets/images/framework/spring/di/spring_di04.jpg)   
   
***

#### lombock / TDD 라이브러리 추가
   
``` xml 
<!-- lombok -->  	
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.22</version>
    <scope>provided</scope>
</dependency>

<!-- Test library -->
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>5.8.2</version>
    <scope>test</scope>
</dependency>

<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-params</artifactId>
    <version>5.8.2</version>
    <scope>test</scope>
</dependency>

<dependency>
    <groupId>org.assertj</groupId>
    <artifactId>assertj-core</artifactId>
    <version>3.21.0</version>
    <scope>test</scope>
</dependency>
```   
   
***

설정해줘야할 게 엄청 많다. 많이 하다보면 익숙해지겠지만 지금은 넘나 생소하다.   
   

[Spring]: [https://spring.io/]
[Maven repository]: [https://mvnrepository.com/]

















