---
layout: single
title: "제어문 - 분기문"
categories: ['Programming', 'Java']
---
   
#### break
* 반복문에서 사용 시: 자신이 포함 된 가장 가까운 반복문 이탈   
* switch문에서 사용 시: case에서 종료   
   
``` java
for ( 초기식 ; 조건식 ; 증감식 ; ) {
    // 조건식이 true일 때까지 실행
    break;
}
```   
``` java
for ( int i = 0; i <= 10; i++) { // i가 10일 때까지 반복 출력
    System.out.print( i + " " );
    if ( i == 5 ) { // i가 5일 때
        System.out.println("반복문 종료");
        break; // 반복문 종료
    }
}
// 출력 결과 : 0 1 2 3 4 5 반복문 종료
```   
0부터 10까지의 숫자를 출력하다가,   
if문에서 i가 5일 때 반복문을 종료하도록 했다.   
   
``` java
int sum;
int random = 0;

while( true ) {
    sum = 0; // 계속 돌기 때문에 초기화 필요
    random = (int)( Math.random() * 10 + 1 );

    for (int i = 0; i <= random; i++) {
        sum += i;
    }

    if ( random == 5 ) {
        System.out.println("종료되었습니다.");
        break;
    }

    System.out.println("random : " + random);
    System.out.printf("1부터 %d까지의 합계 : %d\n", random, sum);
    break;
}
```   
1부터 랜덤값까지의 합계 구하기.   
랜덤값이 5가 나오면 반복문이 종료된다...! 이건 혼자 다시 하려고 하면 자꾸 이상하게 된다.  
이거 되면 저게 안 되고.... 다시 해봐야지.   
   
***
#### continue
* 반복문에서만 사용   
* 전체 반복 중 특정 조건을 제외할 때 사용   
* continue 아래 구문은 실행하지 않고 다시 반복문으로 이동   
기본 분법은 break문이랑 동일하다.   

``` java
for ( int i = 0; i <= 100; i++ ) {
    System.out.print( i + " ");
}
// 출력 결과 : 0 1 2 3 4 5 6 7 8 9 10 11 ... 100
```   
   
``` java
for ( int i = 0; i <= 100; i++ ) {
    if ( i % 5 == 0 ) { // 5의 배수
        continue;
    }

    System.out.print( i + " ");
}
// 출력 결과 : 0 1 2 3 4 6 7 8 9 11 ... 99
```   
break문을 사용하지 않는 이유는 i가 5의 배수일 때,   
그 후의 숫자들도 출력해야하기 때문이다.   

0 1 2 3 4 5 6 7 8 9 10 11 ... 100   
이렇게 출력을 하고,   

**0 1 2 3 4** 5 **6 7 8 9** 10 **11** ... 100   
이렇게 5의 배수만 제외시키고, 그 다음 숫자는 출력한다.    
break문을 사용하면 5까지만 출력하고 반복문이 종료된다.   

***
