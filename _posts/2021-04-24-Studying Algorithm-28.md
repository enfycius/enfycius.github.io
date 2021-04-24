---
title: "BOJ: 10998 AxB"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

두 정수 $$A$$와 $$B$$를 입력받은 다음, $$A \times B$$를 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 $$A$$와 $$B$$가 주어진다. $$(0 < A, B < 10)$$

## 출력

첫째 줄에 $$A \times B$$를 출력한다.

### 예제 입력 1

```shell
1 2
```

### 예제 출력 1

```shell
2
```

### 예제 입력 2

```shell
3 4
```

### 에제 출력 2

```shell
12
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int a, b;

    cin>>a>>b;

    cout<<a*b;

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/10998)
