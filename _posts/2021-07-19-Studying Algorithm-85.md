---
title: "BOJ: 2441 별 찍기 - 4"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

첫째 줄에는 별 $$N$$개, 둘째 줄에는 별 $$N-1$$개, ..., $$N$$번째 줄에는 별 1개를 찍는 문제

하지만, 오른쪽을 기준으로 정렬한 별(예제 참고)을 출력하시오.

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
#include <bits/stdc++.h>

using namespace std;

int main(void) {
    int n;

    cin>>n;
    
    for(int i=0; i<n; i++) {
        for(int j=0; j<n-i; j++)
            cout<<'*';
        
        cout<<'\n';

        for(int j=0; j<=i; j++)
            cout<<' ';
    }

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/2441)