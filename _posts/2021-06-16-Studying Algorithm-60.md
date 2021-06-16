---
title: "BOJ: 10869 사칙연산"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

두 자연수 $$A$$와 $$B$$가 주어진다. 이때, $$A+B, A-B, A*B, A/B, A%B$$를 출력하는 프로그램을 작성하시오.

## 입력

두 자연수 $$A$$와 $$B$$가 주어진다. $$(1 \leq A, B \leq 10,000)$$

## 출력

첫째 줄에 $$A+B$$, 둘째 줄에 $$A-B$$, 셋째 줄에 $$A*B$$, 넷째 줄에 $$A/B$$, 다섯째 줄에 $$A%B$$를 출력한다.

### 예제 입력 1

```shell
7 3
```

### 예제 출력 1

```shell
10
4
21
2
1
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int a, b;

    cin>>a>>b;

    cout<<a+b<<'\n';
    cout<<a-b<<'\n';
    cout<<a*b<<'\n';
    cout<<a/b<<'\n';
    cout<<a%b<<'\n';

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/10869)