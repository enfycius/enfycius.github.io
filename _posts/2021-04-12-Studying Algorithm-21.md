---
title: "BOJ: 10829 이진수 변환"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

자연수 $$N$$이 주어진다. $$N$$을 이진수로 바꿔서 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 자연수 $$N$$이 주어진다. $$(1 \leq N \leq 100,000,000,000,000)$$

## 출력

$$N$$을 이진수로 바꿔서 출력한다. 이진수는 0으로 시작하면 안 된다.

### 예제 입력 1

```shell
53
```

### 예제 출력 1

```shell
110101
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

void n_to_b(long long n) {
    if(n > 0 && n < 100000000000001) {
        n_to_b(n/2);
        cout<<n%2;
    }
}

int main(void) {
    long long n;

    cin>>n;
    n_to_b(n);

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/10829)
