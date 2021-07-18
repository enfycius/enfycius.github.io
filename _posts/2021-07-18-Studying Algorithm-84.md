---
title: "BOJ: 15439 Vera and Outfits"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

Vera owns $$N$$ tops and $$N$$ pants. The $$i$$-th top and $$i$$-th pants have colour $$i$$, for $$1 \leq i \leq N$$, where all $$N$$ colours are different from each other.

An outfit consists of one top and one pants. Vera likes outfits where the top and pants are not the same colour.

How many different outfits does she like?

## 입력

The input will be in the format:

```shell
N
```

Constraints:

* $$1 \leq N \leq 2017$$
* $$N$$ is integer

## 출력

Output one line with the number of different outfits Vera likes.

### 예제 입력 1

```shell
1
```

### 예제 출력 1

```shell
0
```

### 예제 입력 2

```shell
2
```

### 예제 출력 2

```shell
2
```

### 예제 입력 3

```shell
5
```

### 예제 출력 3

```shell
20
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

int main(void) {
    int n;
    
    cin>>n;
    
    cout<<n*(n-1);
    
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/15439)