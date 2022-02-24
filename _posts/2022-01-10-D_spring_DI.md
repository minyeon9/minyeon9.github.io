---
layout: single
title: "Spring - DI(setter)"
categories: ['Framework']
---

#### DI XML 방식
* Spring 컨테이너 구동 시 spring의 환경 설정 관련된 xml 파일을 불러오는데, 이 파일에 bean, aop, transaction 등 여러 사항을 다 작성하여 구동하는 방식이다.
   
***

#### XML 방식 장단점
* 장점
	* 생성되는 모든 Bean을 XML에서 확인 할 수 있다.
	* 프로젝트를 운영하는 입장에서 관리의 편의성이 높다.
* 단점
	* Bean의 개수가 많아지면 XML 파일을 관리하기 어렵다.
	* 여러 개발자가 같은 설정 파일을 수정하면 설정에 충돌이 발생 할 수 있다.
	* DI에 필요한 적절한 setter 메소드 또는 생성자가 코드 내부에 반드시 존재해야 된다.
   
***

#### XML 구조
* beans 태그를 최상위 태그로 하여 beans 태그 안에 다양한 태그로 값을 설정할 수 있다.
   
**XML 주요 태그**
   
|태그명|내용|속성|
|----|----------|-----|
|beans xml|파일의 최상위 태그로 여러가지 namespace를 설정 namespace : p, c, aop, context, tx, mvc 등|
|bean|스프링에서 사용할 POJO 객체를 등록할 때 사용 Id, class, scope|
|import|설정 파일을 불러오는 태그 resource|
   
***

#### XML 태그 - bean
* POJO 객체를 컨테이너에 등록하여 컨테이너가 사용할 수 있게 만드는 태그
* Spring에서 관리하는 객체 하나
   
``` xml
<bean id name="명칭" class="클래스 풀네임" [기타 옵션] />
```
   
**bean 기본 속성**
   
|속성명|내용|
|id [="String"]|객체 생성 시 사용하는 변수라고 보면된다. 명명 규칙 : 낙타 표기법 사용 / 자바 식별자 작성 규칙 적용|
|name [="String"]|자바 식별자 작성 규칙을 따르지 않음 / 특수 기호 포함 시 사용|
|class [="클래스 풀네임"]|POJO객체를 지정 / 패키지를 포함한 클래스명 작성|
   
**bean 기타 속성**
   
|init-method [="메소드명"]|객체 생성 후 초기화 하거나 실행되어야 할 기능이 있는 경우|
|destroy-method [="메소드명"]|객체 삭제되기 전에 실행되어야 할 기능이 있는 경우|
|lazy-init [="true | false"]|객체가 즉시 로딩되지 않고 사용시 로딩 선택(true)|
|scope [="설정값"]|객체 생성 방식을 지정|
   
* scope 설정 값
	* singleton : spring 컨테이너 내에 단 하나의 객체만 생성(default)
	* prototype : 다수의 객체가 존재할 수 있음
	
***

#### bean 등록
* root-context.xml
* 등록한 bean은 객체를 만들어서 Application Context(Bean Factory)에 보관
   
``` xml
<!-- 
	Owner owner = new Owner("홍길동", 20, new Cat("고영희"));
	▲ 이 객체를 bean으로 등록
-->
<bean id="owner" class="com.kh.di.owner.Owner">
	<constructor-arg name="name" value="홍길동" />
	<constructor-arg name="age" value="20" />
	<!-- pet은 객체이기 때문에 bean으로 등록하고 그 bean의 id를 ref 속성에 작성 -->
	<constructor-arg name="pet" ref="cat" />
</bean>

<!-- 
	Pat pat = new Cat("고영희");
	▲ 이 객체를 bean으로 등록
-->
<bean id="cat" class="com.kh.di.pet.Cat">
	<constructor-arg name="name" value="고영희" />
</bean>

<bean id="dog" class="com.kh.di.pet.Dog">
	<constructor-arg name="name" value="댕댕이" />
</bean>
```
   
***

#### GenericXmlApplicationContext를 통해 xml 방식으로 변경
* 어제 생성자 주입으로 작성했던 코드를 xml 방식으로 변경해서 실습 진행
	* Spring 애플리케이션 컨텍스트를 활용하여 객체 간의 결합도를 낮춤 
* GenericXmlApplicationContext
	* ApplicationContext 를 구현한 Class
	* 일반적인 XML 형태의 문서를 읽어 컨테이너 역할을 수행
   
-
1. bean을 등록한 xml 파일 읽어오기
	* 경로, 파일명 명시
	* classpaht 기준으로 찾기
2. 객체 가져오기
   
``` java
@Test
public void contextTest() {
	// 2. 경로, 파일명을 지정하여 bean을 등록한 xml 파일 읽어오는 방법
	GenericXmlApplicationContext context = new GenericXmlApplicationContext("file:src/main/resources/spring/root-context.xml");

	// 2. classPath를 기준으로 파일을 읽어오는 방법
	// classPath를 : target > classes
	// classpath 키워드 생략 가능
	GenericXmlApplicationContext context = new GenericXmlApplicationContext("classpath:spring/root-context.xml");

	// 3. context를 통해 Owner 객체 가져오기(둘 중 아무거나 사용)
	// Owner owner = (Owner)context.getBean("owner");
	Owner owner = context.getBean("owner", Owner.class);
}
```
   
***

#### setter를 통한 DI
* property 태그 사용
   
``` xml
<bean id="owner" class="com.kh.di.owner.Owner">
	<constructor-arg name="name" value="홍길동" />
	<constructor-arg name="age" value="20" />
	<constructor-arg name="pet" ref="dog" /> <!-- dog로 변경 -->
</bean>

<!-- 
	setter 이용. ▼ 아래와 같은 작업
	Pat pat = new Dog("댕댕이");
	pat.setName("댕댕이");
-->
<bean id="dog" class="com.kh.di.pet.Dog">
	<property name="name" value="댕댕이">
</bean>
```
   
dog / cat으로 서로 변경할 때 여러 파일의 수정이 필요했는데,    
지금은 bean으로 등록해둔 것을 쓰기 때문에 bean의 id만 수정해주게 되었다.   
   
***





















