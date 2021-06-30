---
title: "BOJ: 16430 제리와 톰"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

톰은 마트에서 치즈 $$1kg$$을 사서 집으로 돌아왔습니다.

그런데 톰이 한눈을 판 사이 제리가 와서 $$A/B kg$$만큼 훔쳐갔습니다.

제리가 치즈를 훔쳐 간 후 톰이 가지고 있는 치즈의 무게는 얼마인가요?


## 입력

첫 번째 줄에 두 정수 $$A, B (1 \leq A < B \leq 9)$$ 가 주어집니다.

$$A$$와 $$B$$는 서로소임이 보장됩니다.

## 출력

정답을 기약분수로 표현했을 때 $$P/Q kg$$이라면 첫 번째 줄에 $$P$$와 $$Q$$를 공백을 사이에 두고 출력합니다.

### 예제 입력 1

```shell
2 7
```

### 예제 출력 1

```shell
5 7
```

### 예제 입력 2

```shell
5 8
```

### 예제 출력 2

```shell
3 8
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

int main(void) {
    int a, b;

    cin>>a>>b;

    cout<<b-a<<' '<<b;

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/16430)