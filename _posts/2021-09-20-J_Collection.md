---
layout: single
title: "컬렉션(Collection)"
categories: ['Programing', 'Java']
---
   
#### 컬렉션(Collection)
* 객체의 모음
* 주요 인터페이스: List / Set / Map   
   
***
#### 장점
* 크기 제약 없음
* 추가, 삭제 및 정렬의 처리가 간단하게 해결
* 여러 타입의 데이터 저장 가능   
   
***
#### List
* 순서 존재
* 중복 허용
* ex) Wating List
* 구현 클래스: Vector / ArrayList / LinkedList    
   
1) ArrayList   
   
* List의 후손
* 초기 저장 용량 10으로 자동 설정
* 객체가 늘어날 경우 자동으로 늘어나고 고정도 가능
* 동기화 제공하지 않음
    * 동기화 : 하나의 데이터에 대해 여러 스레드가 접근하려 할 때 한 시점에서의 하나의 스레드만 사용할수 있도록 함   
    
2) Vector   
   
* ArrayLIst와 동일
* 동기화 제공
* List 객체들 중 성능이 제일 낮음   
   
3) LinkedList
* 연결된 형태로 데이터를 관리
* 특정 인덱스에서 객체를 추가하거나 제거할 때 편리   
   
***
#### Set
* 집합
    * 집합, 차집합, 교집합 등등
* null도 중복 불가
* Iterator / ListIterator / Enumeration   
   
1) HashSet   
   
* Set에 객체를 저장할 때 hash함수를 사용하여 처리 속도 빠름
* 동일 객체 뿐 아니라 동등 객체도 중복 저장하지 않음   
   
2) LinkedHashSet   
   
* HashSet과 고의 동일
* Set에 추가되는 순서 유지   
   
***
#### Enumeration / Iterator / ListIterator
* 컬렉션에 저장된 요소에 접근할 때 사용하는 인터페이스
* List / Set에서만 사용 가능   
   
***
#### Map
* Key와 Value로 구성, 둘 다 모두 객체
* 키 중복 불가  값 중복 가능
* 키/값 = entry 객체
* 구현 클래스: HashMap / HashTable / LinkedHashMap / Properties / TreeMap
* index가 없어서 Iterator 사용 불가
    * List, Set으로 변경해서 Iterator 받기   
   
```java
Map map = new HashMap();
Iterator it = map.entrySet().iterator();
```   
   
1) HashMap   
   
* 키 객체는 hashCode()와 equals()를 재정의해 동등 객체가 될 조건을 정해야 함
    * 키 타입은 hashCode()와 equals() 메서드가 재정의되어 있는 String 타입을 주로 사용   
    
``` java
Map<K, V> map = new HashMap<K, V>();
```   
   
2) HashTable   
   
* 스레드 동기화 된 상태
* 복수의 스레드가 동시에 HashTable에 접근해 객체를 추가, 삭제 하더라도 스레드에 안전(Tread safe)