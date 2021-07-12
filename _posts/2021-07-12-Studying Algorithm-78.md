---
title: "BOJ: 6749 Next in line"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

You know a family with three children. Their ages form an arithmetic sequence: the difference in ages between the middle child and youngest child is the same as the difference in ages between the oldest child and the middle child. For example, their ages could be 5, 10 and 15, since both adjacent pairs have a difference of 5 years.

Given the ages of the youngest and middle children, what is the age of the oldest child?

## 입력

The input consists of two integers, each on a separate line. The first line is the age $$Y$$ of the youngest child $$(0 \leq Y \leq 50)$$. The second line is the age $$M$$ of the middle child $$(Y \leq M \leq 50)$$.

## 출력

The output will be the age of the oldest child.

### 예제 입력 1

```shell
12
15
```

### 예제 출력 1

```shell
18
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

int main(void) {
    int i, j;
    
    cin>>i>>j;
    
    cout<<j+(j-i);
    
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/6749)