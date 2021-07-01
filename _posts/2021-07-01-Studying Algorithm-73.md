---
title: "BOJ: 2558 A + B - 2"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

두 정수 $$A$$와 $$B$$를 입력받은 다음, $$A+B$$를 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 $$A$$, 둘째 줄에 $$B$$가 주어진다. $$(0 < A, B < 10)$$

## 출력

첫째 줄에 $$A+B$$를 출력한다.

### 예제 입력 1

```shell
1
2
```

### 예제 출력 1

```shell
3
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

int main(void) {
    int i, j;
    
    cin>>i>>j;
    
    cout<<i+j;
    
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/2558)