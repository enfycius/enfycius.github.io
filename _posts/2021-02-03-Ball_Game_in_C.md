---
title: "C언어 야구 게임"

classes: wide

categories:
  - C
tags:
  - Programming
  - Coding
---

# 야구 게임(숫자 맞추기 게임과 비슷)

컴퓨터는 0에서 9사이의 숫자 중에서 서로 다른 세 개의 숫자를 고르고, 사용자는 이것을 맞춰야 한다.

중요한 것은 숫자의 순서까지 정확히 맞춰야 한다는 것이다.

단, 사용자가 예상한 숫자를 입력할 때마다 컴퓨터는 입력된 숫자와 컴퓨터 자신이 생각한 숫자가 얼마나 비슷한지를 알려줘야 한다.

예를 들어, 컴퓨터가 고른 숫자가 1 4 9 이고, 사용자가 입력한 숫자가 4 0 9 이면, 두 개의 숫자 4와 9가 일치한다.

9는 숫자와 위치까지 일치하지만(1 strike), 4는 숫자만 일치한다(1 ball).

이런 경우 컴퓨터는 다음과 같은 메시지를 출력해 준다.

1strike, 1ball

만약에 사용자가 1 4 9를 입력하였다면 "3strike, 0ball"이 되어서 프로그램은 종료가 된다.

![Example](/assets/images/c/studying/game/ball_game_1.png)

# 코드

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
 
int main(void)
{
    int arr[3];
    int input[3];
    int i=0;
    int j=0;
    int count=0;
    int strike=0;
    int ball=0;
    
    printf("Start Game\n\n");
    
    srand((int)time(NULL));
    
    for(i=0;i<3;i++)
    {
        arr[i] = rand() % 10;
        
        for(j=0;j<i;j++)
        {
            if(arr[j] == arr[i])
            {
                i--;
                break;
            }
            else
                continue;
        }
    }
    
    printf("\n\n");
    
    while(1)
    {
        printf("\n3개의 숫자 선택: ");
        
        for(i=0;i<3;i++)
            scanf("%d", &input[i]);
        
        strike = 0;
        ball = 0;
        
        for(i=0;i<3;i++)
        {
            for(j=0;j<3;j++)
            {
                if(arr[i] == input[j])
                {
                    if(i == j)
                        strike++;
                    else
                        ball++;
                }
            }
        }
        
        count++;
        
        printf("%d번째 도전 결과: %dstrike, %dball\n", count, strike, ball);
            
        if(strike == 3)
            break;    
    }
     
    return 0;
}
```