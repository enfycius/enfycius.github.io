---
title: "BOJ: 2741 N 찍기"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

자연수 $$N$$이 주어졌을 때, 1부터 $$N$$까지 한 줄에 하나씩 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 $$100,000$$보다 작거나 같은 자연수 $$N$$이 주어진다.

## 출력

첫째 줄부터 $$N$$번째 줄까지 차례대로 출력한다.

### 예제 입력 1

```shell
5
```

### 예제 출력 1

```shell
1
2
3
4
5
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int n;

    cin>>n;

    for(int i=1; i<=n; i++)
        cout<<i<<'\n';

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/2741)