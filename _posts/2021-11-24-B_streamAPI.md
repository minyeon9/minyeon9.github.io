---
layout: single
title: "Stream API - 중간처리"
categories: ['Java']
---

#### Filtering
* 중간 처리 기능
* 요소를 걸러내는 역할
    * distinct() : 중복 제거. Stream의 경우 Object.equals() 메서드가 true를 리턴할 경우 동일 객체로 판단
    * ilter(Predicate) : 매개값으로 전달되는 Predicate가 false를 리턴하는 요소 제거
   
***

```
List<String> names = Arrays.asList("김", "이", "박", "김", "최");
		
Stream<String> stream = names.stream();

stream.forEach(s -> System.out.print(s + " ")); // 김 이 박 김 최
```   
   
***

#### 중복 제거
* 위에 코드를 사용하여 중복 제거 하기
   
```
List<String> names = Arrays.asList("김", "이", "박", "김", "최");
		
Stream<String> stream = names.stream();

stream.distinct().forEach(s -> System.out.print(s + " ")); // 김 이 박 최
```
   
두 개였던 김 중 마지막 요소가 삭제되었다.   
   
***

#### 필터링
```
List<String> fruits = Arrays.asList("사과", "포도1", "복숭아", "포도2", "딸기");
		
Stream<String> stream = fruits.stream();

// startsWith: 포로 시작하는 요소
stream.filter(f -> f.startsWith("포")).forEach(f -> System.out.println(f));

// forEach는 최종 처리 메서드이기 때문에 다시 사용할 경우 새로 stream 받기
fruits.stream()       // 새로 stream을 받고
        .distinct()   // 중복 제거하고
        .filter(f -> f.startsWith("복")).forEach(f -> System.out.println(f));
        // 출력하기 : 복숭아
```
   
***
