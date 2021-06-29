---
title: "C 피보나치 수열"

classes: wide

categories:
  - C
  - Algorithms
tags:
  - C
  - Algorithms
  - Programming
  - Coding

toc: true
---

# 문제

피보나치 수열을 구현하시오.

# 해결

## 코드

```c
#include <stdio.h>
 
void fibonacci(int, int, int, int);
 
int main(void)
{
    int input = 0;
    
    printf("몇 개월?: ");
    scanf("%d", &input);
    
    if(input <= 1)
        printf("%d ", 1);
    else
    {
        printf("%d ", 1);
        fibonacci(input, 1, 1, 1);
    }
        
    return 0;
}
 
void fibonacci(int n, int y, int t, int k)
{
    
    if(n>t)
    {
        printf("%d ", y);
        fibonacci(n,y+k,t+1,y);
    }
    else
        return;
     
}
```