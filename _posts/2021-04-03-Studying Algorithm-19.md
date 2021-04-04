---
title: "BOJ: 10872 팩토리얼"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

$$0$$보다 크거나 같은 정수 $$N$$이 주어진다. 이때, $$N!$$을 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 정수 $$N(0 \leq N \leq 12)$$가 주어진다.

## 출력

첫째 줄에 $$N!$$을 출력한다.

### 예제 입력 1

```shell
10
```

### 예제 출력 1

```shell
3628800
```

### 예제 입력 2

```shell
0
```

### 예제 출력 2

```shell
1
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int input;
    int result = 1;

    cin>>input;

    while(input != 0) 
        result *= (input--);

    cout<<result;

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/10872)
