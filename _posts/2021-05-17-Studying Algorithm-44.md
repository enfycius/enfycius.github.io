---
title: "BOJ: 10430 나머지"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

$$(A+B)\%C$$는 $$((A\%C)+(B\%C))\%C$$와 같을까?

$$(A \times B)\%C$$는 $$((A\%C) \times (B\%C))\%C$$ 와 같을까?

세 수 $$A, B, C$$가 주어졌을 때, 위의 네 가지 값을 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 $$A, B, C$$가 순서대로 주어진다. $$(2 \leq A, B, C \leq 10000)$$

## 출력

첫째 줄에 $$(A+B)\%C$$, 둘째 줄에 $$((A\%C) + (B\%C))\%C$$, 셋째 줄에 $$(A \times B)\%C$$, 넷째 줄에 $$((A\%C) \times (B\%C))\%C$$를 출력한다.

### 예제 입력 1

```shell
5 8 4
```

### 예제 출력 1

```shell
1
1
0
0
```

<br/>

# 코드

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int a, b, c;
    cin>>a>>b>>c;
    cout<<(a+b)%c<<'\n';
    cout<<((a%c)+(b%c))%c<<'\n';
    cout<<(a*b)%c<<'\n';
    cout<<((a%c)*(b%c))%c;
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/10430)