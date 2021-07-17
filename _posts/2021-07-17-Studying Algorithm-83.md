---
title: "BOJ: 8370 Plane"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

Byteland Airlines recently extended their aircraft fleet with a new model of a plane. The new acquistion has $$n_{1}$$ rowos of seats in the business class and $$n_{2}$$ rows in the economic class. In the business class each row contains $$k_{1}$$ seats, while each row in the economic class has $$k_{2}$$ seats.

Write a program which:

* reads information about available seats in the plane,
* calculates the sum of all seats available in that plane,
* writes the result.

## 입력

In the first and only line of the standard input there are four integers $$n_{1}, k_{1}, n_{2}$$ and $$k_{2} (1 \leq n_{1}, k_{1}, n_{2}, k_{2} \leq 1000)$$, separated by single spaces.

## 출력

The first and only line of the standard output should contain one integer - the total number of seats available in the plane.

### 예제 입력 1

```shell
2 5 3 20
```

### 예제 출력 1

```shell
70
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

int main(void) {
    int n1, k1, n2, k2;
    
    cin>>n1>>k1>>n2>>k2;
    
    cout<<(n1*k1)+(n2*k2);
    
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/8370)