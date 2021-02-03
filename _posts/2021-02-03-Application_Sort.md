---
title: "C 정렬 응용 - 사전식 정렬"

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

# 질문

## 내용

5개의 문자를 입력받아 사전순으로 정렬하는 프로그램을 작성하시오.

# 해결

## 내용

아래의 코드에는 중복된 코드가 많이 보인다.

가독성을 위해서라도 아래의 코드를 함수화하는 것이 더 좋을것이다.

## 코드 

```c
#include <stdio.h>
#include <string.h>
 
int main(void)
{
    int i, j, k, t;
    char input[10][15];
    char cpr[50];
    int arrlen[10];
    
    for(i=0;i<5;i++)
    {
        printf("%d번째? ", i+1);
        scanf("%s", input[i]);
        arrlen[i] = strlen(input);
    }
    
    for(i=0;i<5;i++)
        printf("%s ", input[i]);
    
    printf("\n");
    
    for(i=0;i<5;i++)
    {
        for(j=0;j<4;j++)
        {
            if(j==i)
                continue;

            if(i==0)
            {
                if(strcmp(input[i], input[j]) < 0)
                {
                    
                    
                    t=0;
                    while(input[i][t] != NULL)
                    {
                        cpr[t] = input[i][t];
                        t++;
                    }
                    cpr[t]=0;
                    t=0;
                    while(input[j][t] != NULL)
                    {
                        input[i][t] = input[j][t];
                        t++;
                    }
                    input[i][t] = 0;
                    t=0;
                    while(cpr[t] != NULL)
                    {
                        input[j][t] = cpr[t];
                        t++;
                    }
                    input[j][t]=0;
                }
            }
            else
            {
                if(i<j)
                {
                    if(strcmp(input[i], input[j]) < 0)
                    {
                        t=0;
                        while(input[i][t] != NULL)
                        {
                            cpr[t] = input[i][t];
                            t++;
                        }
                        cpr[t]=0;
                        t=0;
                        while(input[j][t] != NULL)
                        {
                            input[i][t] = input[j][t];
                            t++;
                        }
                        input[i][t]=0;
                        t=0;
                        while(cpr[t] != NULL)
                        {
                            input[j][t] = cpr[t];
                            t++;
                        }
                        input[j][t]=0;
                    }
                }
                else
                {
                    if(strcmp(input[i], input[j]) < 0)
                    {
                        t=0;
                        while(input[i][t] != NULL)
                        {
                            cpr[t] = input[i][t];
                            t++;
                        }
                        cpr[t]=0;
                        t=0;
                        while(input[j][t] != NULL)
                        {
                            input[i][t] = input[j][t];
                            t++;
                        }
                        input[i][t]=0;
                        t=0;
                        while(cpr[t] != NULL)
                        {
                            input[j][t] = cpr[t];
                            t++;
                        }
                        input[j][t]=0;
                    }
                }
                
            }
        }
    }
    
    for(i=0;i<5;i++)
        printf("%s ", input[i]);
    
    return 0;
}
```