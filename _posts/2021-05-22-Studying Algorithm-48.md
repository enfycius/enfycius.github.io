---
title: "BOJ: 2440 별 찍기 - 3"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

첫째 줄에는 별 $$N$$개, 둘째 줄에는 별 $$N-1$$개, ..., $$N$$번째 줄에는 별 1개를 찍는 문제

## 입력

첫째 줄에 $$N(1 \leq N \leq 100)$$이 주어진다.

## 출력

첫째 줄부터 $$N$$번째 줄까지 차례대로 별을 출력한다.

### 예제 입력 1

```shell
5
```

### 예제 출력 1

```shell
*****
****
***
**
*
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int n;

    cin>>n;

    for(int i=n; i>0; i--) {
        for(int j=0; j<i; j++)
            cout<<'*';
        cout<<endl;
    }

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/2440)
