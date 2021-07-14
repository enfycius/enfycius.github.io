---
title: "BOJ: 11382 꼬마 정민"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

꼬마 정민이는 이제 $$A + B$$ 정도는 쉽게 계산할 수 있다. 이제 $$A + B + C$$를 계산할 차례이다!

## 입력

첫 번째 줄에 $$A, B, C (1 \leq A, B, C \leq 10^{12})$$이 공백을 사이에 두고 주어진다.

## 출력

$$A+B+C$$의 값을 출력한다.

### 예제 입력 1

```shell
77 77 7777
```

### 예제 출력 1

```shell
7931
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

int main(void) {
    long long a, b, c;
    
    cin>>a>>b>>c;
    
    cout<<a+b+c;
    
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/11382)