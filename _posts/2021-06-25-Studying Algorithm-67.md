---
title: "BOJ: 11720 숫자의 합"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

$$N$$개의 숫자가 공백 없이 쓰여있다. 이 숫자를 모두 합해서 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 숫자의 개수 $$N (1 \leq N \leq 100)$$이 주어진다. 둘째 줄에 숫자 $$N$$개가 공백없이 주어진다.

## 출력

입력으로 주어진 숫자 $$N$$개의 합을 출력한다.

### 예제 입력 1

```shell
1
1
```

### 예제 출력 1

```shell
1
```

### 예제 입력 2

```shell
5
54321
```

### 예제 출력 2

```shell
15
```

### 예제 입력 3

```shell
25
7000000000000000000000000
```

### 예제 출력 3

```shell
7
```

### 예제 입력 4

```shell
11
10987654321
```

### 예제 출력 4

```shell
46
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int n;
    int result = 0;
    char i[100];

    cin>>n;

    for(int k=0; k<n; k++)
        cin>>i[k];

    for(int k=0; k<n; k++)
        result += (i[k] - 48);

    cout<<result;

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/11720)