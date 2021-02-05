---
title: "Recursion"

classes: wide

categories:
  - Data Structures
tags:
  - Data Structures
  - Programming
  - Coding

toc: true
---

# 개념

## 정의

**재귀함수**란 함수 내에서 자기 자신을 호출하는 함수를,

**재귀호출**이란 자기 자신을 호출하는 행위를 일컫는다.

## 장점

재귀함수를 이용해서 자료구조나 알고리즘 분야에 적용하면 복잡하고 난해한 문제들을 비교적 쉽게 해결할 수 있다.

## 단점

계속적인 자기 자신의 함수 호출로 시간과 메모리 공간의 효율이 저하되는 문제가 있다.

그러므로 프로그램 개발 시 Recursion을 이용한다면, 신중해질 필요가 있다.

## 코드

### return문을 이용한 재귀 호출

수학에서 $$n!$$은 $$n*(n-1)*...*2*1$$와 같은 표현이다.

또한 $$n!$$은 $$n*(n-1)!$$으로 다시 표현할 수 있다.

이것을 재귀함수로 구현해보면 factorial(n) 함수에서 다시 factorial(n-1)을 호출하면 된다.

```c
#include <stdio.h>
 
void self_service(void);

int main(void)
{
    int a;
    int result;
 
    printf("정수 입력: ");
    scanf("%d", &a);
 
    result = factorial(a);
    printf("%d 팩토리얼은 : %d입니다. \n", a, result);
    
    return 0;
}
 
int factorial(int n)
{
    if(n<=1)
        return 1;
    else
        return n * factorial(n-1);
}
```

# 문제

다음은 문제가 있는 코드이다.

이 코드에서 문제를 찾아내어 이를 해결하시오.

```c
#include <stdio.h>
 
void self_service(void);
 
int main(void)
{
    self_service();
    return 0;
}
 
void self_service() 
{ 
    printf("셀프 서비스\n");
    self_service();
}
```

## 설명

위 코드는 메모리가 부족할 때까지 계속 self_service() 함수를 호출하여 실제로 메모리가 부족하면 실행이 끝난다.

구체적으로는 Runtime Error가 발생하여 함수가 무한 반복되는 상태로 진입하게 되고 결국 Memory Overflow가 발생하여 실행이 중단된다.

이러한 문제를 해결하려면 특정 조건이 참이 되었을 경우에 함수의 무한 반복 상태를 탈출하게끔 해줘야 한다.

즉, 이에 대한 별도의 조건문이 마련되어야 한다.

# 해결

## 코드

```c
#include <stdio.h>
 
void self_service(void);
 
int main(void)
{
    
    self_service();
    return 0;
}
 
void self_service() {
 
    static int i = 0;
 
    if(i>5)
        return;
 
    printf("셀프 서비스\n");
    i++;
    self_service();
 
}
```

## 설명

필자는 static keyword를 이용하여 정적 지역 변수를 선언한 이후에 조건을 걸어서 조건을 만족하면, 함수가 종료되게끔 코드를 작성하였다.
(지역 변수를 사용하지 않고 정적 지역 변수를 사용한 이유는 재귀 호출이라는 것이 겉으로는 같은 함수를 호출하는 것처럼 보이지만 실제로는 원함수를 copy(복사)하는 concept이기 때문에 지역 변수를 사용하게 되면 count가 되지 않는 문제가 발생하여 무한 반복 상태에 빠지게 된다.)

하지만 정적 지역 변수 같은 경우에는 전역 변수를 보완했음에도 불구하고, 프로그램 종료시까지 메모리 상에 남아있기 때문에 남용 시 공유 자원에 대한 잘못된 접근으로 부작용을 낳을 수 있다.

그러므로 이것을 최대한 피하는 것이 바람직하다.

그러므로 이번에는 매개변수를 이용한 재귀호출을 보이고자 한다.

### 매개변수를 이용한 재귀 호출

```c
#include <stdio.h>
 
void self_service(int);
 
int main(void)
{
    int a = 1;
    self_service(a);
    return 0;
}
 
void self_service(int n) {
    if(n>5)
        return;
 
    printf("셀프 서비스 %d회 \n", n);
    self_service(n+1);
}
```










