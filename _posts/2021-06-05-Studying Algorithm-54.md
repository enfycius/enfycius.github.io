---
title: "BOJ: 11653 소인수분해"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

정수 $$N$$이 주어졌을 때, 소인수분해하는 프로그램을 작성하시오.

## 입력

첫째 줄에 정수 $$N(1 \leq N \leq 10,000,000)$$이 주어진다.

## 출력

$$N$$의 소인수분해 결과를 한 줄에 하나씩 오름차순으로 출력한다. $$N$$이 1인 경우 아무것도 출력하지 않는다.

### 예제 입력 1

```shell
72
```

### 예제 출력 1

```shell
2
2
2
3
3
```

### 예제 입력 2

```shell
3
```

### 예제 출력 2

```shell
3
```

### 예제 입력 3

```shell
6
```

### 예제 출력 3

```shell
2
3
```

### 예제 입력 4

```shell
2
```

### 예제 출력 4

```shell
2
```

### 예제 입력 5

```shell
9991
```

### 예제 출력 5

```shell
97
103
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

bool is_prime(int n) {
    int count = 0;

    for(int i=1; i<=n; i++) n % i == 0 ? count++ : false;

    return count == 2 ? true : false;
}

int main(void) {
    int n, i=1, val=0, exa=0;

    cin>>n;

    while(n != 1) { while(n % i == 0 && is_prime(i)) { cout<<i<<'\n'; n /= i; } i++; }

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/11653)
