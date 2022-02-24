---
layout: single
title: "Spring - DI(생성자)"
categories: ['Framework']
---

#### 실습 내용
* 애완동물을 키우는 사람을 예시로 하여 실습 진행
* 이게 뭐라고.. 이해하는데 도움됨.ㅋㅋㅋ
   
***
   
#### 사람 클래스 생성
* 클래스명 : Owner
* test case도 생성
   
``` java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Owner {
	private String name;
	private int age;
	private Dog dog;
}
```
   
***

#### 애완동물 클래스 생성
   
``` java
package com.kh.di.pet;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class Dog {
	private String name;
	
	public String bark() {
		return "멍멍~";
	}
}

// --------------------------------
package com.kh.di.pet;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class Cat {
    private String name;
	
	public String bark() {
		return "야옹~";
	}
}
```
   

***

#### test 코드 작성
   
``` java
private Owner owner;

@Test
@Disabled
public void nothing() {
}

@Test
public void create() {
    Owner owner = new Owner("홍길동", 20, new Dog("댕댕이"));
    // Owner owner = new Owner("홍길동", 20, new Cat("고영희"));
    
    assertThat(owner).isNotNull();
    assertThat(owner.getDog()).isNotNull();
    // assertThat(owner.getCat()).isNotNull();
}
```
   
Cat 객체를 사용하면 에러가 난다.   
이유는 Owner 객체는 Dog만 갖고 있기 때문이다.   
그래서 Cat 객체를 갖게 하려면 아래와 같이 Owner 클래스를 수정해야한다.   
   
``` java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Owner {
	private String name;
	private int age;
	private Cat cat; // Cat으로 수정
}
```
   
* 여기서 확인 가능한 것은 고양이를 키우기 위해 연결 되어있는 모든 파일을 수정했다.   
지금은 연결 되어 있는 파일이 별로 없지만 프로젝트 내에서는 많은 파일이 수정될 것이다.   
이런 상황을 결합도가 높다라고 표현한다.   
   
***

#### 생성자를 통한 의존성 주입
   
**Pet interface 생성**
   
``` java
package com.kh.di.pet;

public interface Pet {
	public String bark(); // 추상 메서드
}
```
   
-
   
**Dog / Cat 클래스 수정**
   
``` java
// Pet 클래스를 상속하도록 수정
package com.kh.di.pet;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class Dog implements Pet {
	private String name;
	
	@Override
	public String bark() {
		return "멍멍~";
	}
}

// --------------------------------
package com.kh.di.pet;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class Cat implements Pet {
    private String name;
	
	@Override
	public String bark() {
		return "야옹~";
	}
}
```
   
-
   
**Owner 클래스 수정**
   
``` java
import com.kh.di.pet.Pet;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class Owner {
	private String name;
	private int age;
	private Pet pet; // Pet으로 수정
}
```
   
-
   
**test 코드 수정**
   
``` java
@Test
public void create() {
    // Owner owner = new Owner("홍길동", 20, new Dog("댕댕이"));
    Owner owner = new Owner("홍길동", 20, new Cat("고영희"));
    
    assertThat(owner).isNotNull();
    assertThat(owner.getPet()).isNotNull();
}
```
   
이렇게까지 수정하면 Dog / Cat 모두 받을 수 있다.
















