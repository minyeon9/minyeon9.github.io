---
layout: single
title: "Apache Maven"
categories: ['Framework']
---

#### Apache Maven
* 자바용 프로젝트 관리 도구
* project object model(POM) XML 문서를 통해 해당 프로젝트의 버전 정보 및 라이브러리 정보들을 통합하여 관리하는 프레임워크
   
***

#### 라이브러리 종속성
* 일반적인 프로젝트는 개발자가 필요한 라이브러리를 직접 찾아서 추가 필요
* Maven 사용 시 pom.xml 문서에 사용하고자 하는 라이브러리를 등록 
    * 라이브러리가 프로젝트에 자동 추가되어 라이브러리 관리 편의성 제공
    * Sevlet/JSP 실습 때 'lib' 폴더에 필요한 라이브러리를 직접 추가했던 것을 자동으로 추가할 수 있게 됨
   
***

#### POM
* Project Object Model
* 하나의 프로젝트에서 사용하는 자바 버전, 라이브러리, 플러그인 구성을 통합하여 관리할 수 있게 각 설정 정보를 XML로 문서화 한 파일
* [라이브러리 관련 정보 제공 사이트]
    * maven repository에서 필요한 라이브러리를 다운 받아서 추가
* 프로젝트의 최상위에 위치
* 프로젝트당 하나씩 존재
    
***

#### pom.xml의 구성
   
``` xml
<project>
    <modelVersion>4.0.0</modelVersion> <!-- Maven version 정보 : Maven 2 버전 이후 POM의 경우 항상 4.0.0 -->
    <groupId>com.kh</groupId> <!-- 최초 만든 패키지 1, 2레벨 --> 
    <artifactId>spring</artifactId> <!-- 최초 만든 패키지 3레벨 : context-path -->
    <name>springProject</name> <!-- 프로젝트 명 -->
    <version>1.0</version>
    
    <dependencies> <!-- 라이브러리 의존성 주입 -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
            <scope>test</scope> <!-- 이 라이브러리는 테스트 실행 및 컴파일에만 사용 -->
        </dependency>
    </dependencies>
</project>
```
   
* pom.xml 변경 시, 프로젝트 우클릭 > maven > update project 클릭하고 실행해보기.   
    * 단축기 Alt + f5(난 왜 단축키 안 먹지?)

***

#### maven 다운로드
* [maven]
   
![Alt text](/assets/images/framework/maven/maven01.jpg)   
   
위에 표시된 걸로 다운로드 받기
   
-
   
![Alt text](/assets/images/framework/maven/maven02.jpg)   
   
window - preferences - maven - installations   
Add 버튼 클릭해서 다운 받은 maven 추가하기.   
원래는 내장되어 있는데 다운로드 받은 것도 추가 가능하다고 하셨다.   
   
-
   
![Alt text](/assets/images/framework/maven/maven03.jpg)   
   
window - preferences - maven - user settings   
브라우저 버튼 클릭하고 해당 경로에 있는 settings.xml로 설정해주기.   
   
***

#### maven project 생성
   
![Alt text](/assets/images/framework/maven/maven04.jpg)   
   
메이븐 프로젝트 열기
   
-
   
![Alt text](/assets/images/framework/maven/maven05.jpg)   
   
maven-archetype-quickstart 검색해서 선택하기.   
이건 이번에만 이렇게 해보는 거라고 하셨음. 간단한 실습용으로.   
   
-
   
![Alt text](/assets/images/framework/maven/maven06.jpg)   
   
표시된 거처럼 적어주고 finish 버튼 클릭해서 프로젝트 생성하기.   
   
-
   
![Alt text](/assets/images/framework/maven/maven07.jpg)   
   
***

#### 라이브러리 추가
* [라이브러리 관련 정보 제공 사이트]
* 위 사이트 접속 후 필요한 라이브러리 검색
   
![Alt text](/assets/images/framework/maven/maven08.jpg)   
   
버전 정보 클릭하기.   
artifact 블라블라 경고창 뜨는 건 강사님이 나중에 알려주신다고 함..   
oracle 버전 관련해서 뭐라고 하는 거 같았음.
   
-
   
![Alt text](/assets/images/framework/maven/maven09.jpg)   
   
코드 부분을 클릭하면 자동으로 복사가 된다.   
   
-
   
![Alt text](/assets/images/framework/maven/maven10.jpg)   
   
pom.xml 파일에 복사한 코드를 추가했다.   
이렇게만 하면 라이브러리가 추가된다니.   
   
-
   
![Alt text](/assets/images/framework/maven/maven11.jpg)   
   
프로젝트에서 해당 폴더를 보면 추가해준 라이브러리가 잘 추가되어 있는 것을 확인 할 수 있다.   
나머지는 수업 때 다 같이 추가한 라이브러리들.   
생각보다 많은 라이브러리가 필요했는데 
모든 라이브러리를 pom.xml에 추가하여 한 번에 관리하는 것이 효율적이겠구나 라는 생각이 들었다.
   
-
   
![Alt text](/assets/images/framework/maven/maven12.jpg)   
   
실제 다운로드된 위치는 위와 같다. 신기하다...
어떻게 된 건데..?ㅋㅋㅋ 난 코드만 추가했는데.
   
-
   
![Alt text](/assets/images/framework/maven/maven15.jpg)   
   
여기서도 확인 가능.
   
-
   
![Alt text](/assets/images/framework/maven/maven13.jpg)   
   
위에서 프로젝트 maven 세팅할 때 추가했던 settings.xml에   
라이브러리가 다운로드 되는 경로가 지정되어 있다고 한다.   
변경할 일은 거의 없지만 변경이 필요한 경우 여기서 변경해주면 된다고 한다.   
   
***










[라이브러리 관련 정보 제공 사이트]: [https://mvnrepository.com/]
[maven]: [https://maven.apache.org/]