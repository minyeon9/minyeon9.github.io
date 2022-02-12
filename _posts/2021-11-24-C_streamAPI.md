---
layout: single
title: "Stream API - 최종 처리"
categories: ['Java']
---

#### Mathcing
* 최종 처리 단계에서 요소들이 특정 조건에 만족 여부 확인
    * true / false 리턴
* allMatch() : 모든 요소가 매개값으로 주어진 Predicate의 조건에 만족하는지
* anyMatch() : 최소 하나의 요소가 매개값으로 주어진 Predicate의 조건에 만족하는지
* nonMatch() : 모든 요소가 매가값으로 주어진 Predicate의 조건에 만족하지 않는지
   
```
int[] values = {2, 4, 6};
boolean result = false;

result = Arrays.stream(values)
        .allMatch(value -> value % 2 == 0); // 모두 만족
System.out.println(result); // true

result = Arrays.stream(values)
        .anyMatch(value -> value % 3 == 0); // 6 하나만 만족
System.out.println(result); // true

result = Arrays.stream(values)
        .noneMatch(value -> value % 4 == 0); // 만족하는 값 없음
System.out.println(result); // false
```
   
***

#### 실습 문제
```
List<Student> list = Arrays.asList(
    new Student("이원석", 20, "남자", 100, 100),
    new Student("하윤기", 18, "여자", 90, 80),
    new Student("이정현", 27, "남자", 80, 70)
);
boolean result = false;
```
   
-
   
**20살 이상인 사람이 모두 남자인지 확인**
   
```
result = list.stream()
            .filter(student -> student.getAge() >= 20)
            .allMatch(student -> student.getGender().equals("남자"));
System.out.println(result); // true
```
   
-
   
**남자 중 평균이 90점 이상인 사람이 한 명 이상인지 확인**
   
```
result = list.stream()
            .filter(student -> student.getGender().equals("남자"))
            .anyMatch(student -> ((student.getMath() + student.getEnglish()) / 2) >= 90);
System.out.println(result); // true
```   
   
***


