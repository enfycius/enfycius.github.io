---
title: "BOJ: 2742 기찍 N"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

자연수 $$N$$이 주어졌을 때, $$N$$부터 1까지 한 줄에 하나씩 출력하는 프로그램을 작성하시오.

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
5
4
3
2
1
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int n;

    cin>>n;

    for(int i=n; i>0; i--)
        cout<<i<<'\n';
        
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/2742)