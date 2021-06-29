---
title: "BOJ: 4101 크냐?"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

두 양의 정수가 주어졌을 때, 첫 번째 수가 두 번째 수보다 큰지 구하는 프로그램을 작성하시오.

## 입력

입력은 여러 개의 테스트 케이스로 이루어져 있다. 각 테스트 케이스는 한 줄로 이루어져 있으며, 두 정수가 주어진다. 두 수는 백만보다 작거나 같은 양의 정수이다. 입력의 마지막 줄에는 0이 두 개 주어진다.

## 출력

각 테스트 케이스마다, 첫 번째 수가 두 번째 수보다 크면 Yes를, 아니면 No를 한 줄에 하나씩 출력한다.

### 예제 입력 1

```shell
1 19
4 4
23 14
0 0
```

### 예제 출력 1

```shell
No
No
Yes
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int big_chk(int i, int j) {
    if(i>j)
        return 1;
    else
        return 0;
}

int main(void) {
    int i, j;

    while(1) {
        cin>>i>>j;

        if(i == 0 && j == 0)
            break;

        if(big_chk(i, j))
            cout<<"Yes"<<endl;
        else
            cout<<"No"<<endl;
        
    }

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/4101)
