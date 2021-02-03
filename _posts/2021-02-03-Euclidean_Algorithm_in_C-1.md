---
title: "C 유클리드 호제법"

classes: wide

categories:
  - C
  - Algorithms
tags:
  - C
  - Algorithms
  - Programming
  - Coding
---

# 문제

## 내용

유클리드 호제법을 이용하여 최대 공약수를 구하는 프로그램을 작성하시오.

### 유클리드 호제법

#### 정리

$$a, b \in Z$$이고, a를 b로 나눈 나머지가 $$r$$이라고 하자. (여기서 $$a \geq b$$이고, $$r$$은 $$0 \leq r < b$$인 정수.)

$$a$$와 $$b$$의 최대공약수를 $$(a, b)$$라고 하면, 다음이 성립한다.

$$(a, b) = (b, r)$$.

#### 증명

$$a, b \in Z$$이고, $$a \geq b$$라고 하자.

그러면, $$a = bq + r$$을 만족하는 유일한 정수 $$q, r$$이 존재한다.

이때, $$0 \leq r < b$$이다.

$$(a, b) = d, a = d\alpha, b=d\beta$$라고 하자. 즉, $$\alpha$$와 $$\beta$$는 서로소이다.

$$a = bq + r$$

$$d\alpha = d\beta q + r$$

$$d\mid r.$$

즉, $$r$$은 $$d$$의 배수이다.

$$\because r = d\alpha - d\beta q$$


이제, $$r = d\rho.$$ 라고 하자.

만약 $$(\beta, \rho) = d\prime > 1$$라면,

$$\beta = d\prime \beta\prime, \rho = d\prime \rho\prime$$으로 두었을 때,

$$a = bq + r.$$

$$d\alpha = d\beta q + d\rho = dd\prime\beta\prime q + dd\prime\rho\prime = dd\prime(\beta\prime q + \rho\prime).$$

$$\alpha = d\prime(\beta\prime q + \rho\prime).$$

이 되므로, $$d\prime\mid\alpha$$이다.

즉, $$\alpha$$는 $$d\prime$$의 배수이다.

즉, $$d\prime\mid\alpha$$, $$d\prime\mid\beta$$가 되어 $$\alpha$$와 $$\beta$$는 서로소라는 것에 모순이다.

이는 $$(\beta, \rho) = d\prime > 1$$라는 가정에서 나타나는 모순이므로 $$(\beta, \rho) = 1$$이다.

$$\therefore (b, r) = d$$이다.

# 해결

## 코드

```c
#include <stdio.h>
 
int main(void)
{
    int i, j, k;
    
    printf("두 정수 입력(처음에 입력한 수가 더 커야 함): ");
    scanf("%d %d", &i, &j);
    
    if(i>j)
    {
        k=i%j;
        
        while(k!=0)
        {
            i=j; j=k; k=i%j;
        }
        
        printf("최대 공약수: %d \n", j);
    }
    else
        printf("처음에 입력한 수가 더 커야 합니다.\n");
    
    return 0;
}

```

# 참고문헌

[Wikipedia](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95, "Wiki Link")