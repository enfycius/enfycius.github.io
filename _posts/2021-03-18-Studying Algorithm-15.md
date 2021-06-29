---
title: "BOJ: 8958 OX퀴즈"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

"OOXXOXXOOO"와 같은 OX퀴즈의 결과가 있다. O는 문제를 맞은 것이고, X는 문제를 틀린 것이다. 문제를 맞은 경우 그 문제의 점수는 그 문제까지 연속된 O의 개수가 된다. 예를 들어, 10번 문제의 점수는 3이 된다.

"OOXXOXXOOO"의 점수는 $$1+2+0+0+1+0+0+1+2+3 = 10$$점이다.

OX퀴즈의 결과가 주어졌을 때, 점수를 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 테스트 케이스의 개수가 주어진다. 각 테스트 케이스는 한 줄로 이루어져 있고, 길이가 0보다 크고 80보다 작은 문자열이 주어진다. 문자열은 O와 X만으로 이루어져 있다.

## 출력

각 테스트 케이스마다 점수를 출력한다.

### 예제 입력 1

```shell
5
OOXXOXXOOO
OOXXOOXXOO
OXOXOXOXOXOXOX
OOOOOOOOOO
OOOOXOOOOXOOOOX
```

### 예제 출력 1

```shell
10
9
7
55
30
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    char arr[80] = {0,};
    int k;
    int i;
    int add = 0;
    int result = 0;

    cin>>k;

    cin.clear();
    cin.ignore(1, '\n');

    for(; k>0; k--) {
        i = 0;
        result = 0;
        add = 0;

        cin.getline(arr, 80);

        for(int i=0; i<80; i++) {
            if(arr[i] == 'O')
                add++;
            else if(arr[i] == 0)
                break;
            else
                add = 0;

            result += add;
        }

        cout<<result<<'\n';

        while(1) {
            if(arr[i] != 0)
                arr[i] = 0;
            else
                break;

            i++;  
        }
    }
    
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/8958)