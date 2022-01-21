---
layout: single
title: "SQL - INDEX / PL_SQL"
categories: ['Oracle']
---

#### INDEX
* 명령문의 처리 속도를 향상 시키기 위해 컬럼에 생성하는 객체
* 데이터의 검색 속도를 향상 시키기 위해 사용
   
***

#### INDEX 장점
* 검색 속도 향상
* 시스템 부하를 줄여주기 때문에 시스템 성능 향상
   
#### INDEX 단점
* 인덱스를 위한 추가 저장 공간 필요
* 인덱스를 생성하는데 시간이 걸림
* 데이터의 변경 작업(INSERT/UPDATE/DELETE)이 자주 일어날 경우 오히려 성능 저하
   
***

#### INDEX 구조
![Alt text](/assets/images/oracle_index.png)  
   
***

#### INDEX 종류
1. 고유 인덱스 UNIQUE INDEX
    - PRIMARY KEY 제약 조건 생성 시 자동 생성
2. 비고유 인덱스 NONUNIQUE INDEX
    - 주로 WHERE 절에서 많이 사용하는 컬럼에 사용
3. 단일 인덱스 SINGLE INDEX
    - 한 개의 컬럼으로 구성
4. 결합 인덱스 COMPOSITE INDET
    - 두 개 이상의 컬럼으로 구성
5. 함수 기반 인덱스 FUNCTION-BASED INDEX
    - 함수나 수식을 INDEX로 등록
    - SELECT 절이나 WHERE 절에 산술 계산식이나 함수식이 사용된 경우
    - 계산식은 인덱스의 적용을 받지 않음
   
***

#### INDEX 생성
   
```
CREAT [UNIQUE] INDEX 인덱스명
ON 테이블명(컬럼명, 컬럼명 | 함수명, 함수 계산식);

-- 확인
SELECT * FROM USER_IND_COLUMNS;
```   
   
***

#### INDEX 재생성
* DML 작업(특히 DELETE 명령)을 수행한 경우, 해당 인덱스 엔트리가 논리적으로만 제거 되고, 실제 엔트리는 남아있게 되므로 제거된 인덱스가 필요 없는 공간을 차지하고 있지 않도록 인덱스 재생성 필요
* 강사님 ex) 책에 어떤 부분이 중간에 추가되었을 경우, 맨 앞 차례(INDEX)나 맨 뒤 색인(INDEX)도 수정 필요
   
***

#### INDEX를 활용한 정렬
* ORDER BY로 정렬하는 것보다 인덱스를 활용하는 것이 더 좋은 성능을 보임
   
***