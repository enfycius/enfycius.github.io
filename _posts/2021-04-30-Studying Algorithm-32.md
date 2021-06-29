---
title: "BOJ: 8393 합"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

$$n$$이 주어졌을 때, 1부터 $$n$$까지 합을 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 $$n(1 \leq N \leq 10,000)$$이 주어진다.

## 출력

1부터 $$n$$까지 합을 출력한다.

### 예제 입력 1

```shell
3
```

### 예제 출력 1

```shell
6
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int n;
    int result = 0;

    cin>>n;

    for(int i=1; i<=n; i++)
        result += i;

    cout<<result;

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/8393)
