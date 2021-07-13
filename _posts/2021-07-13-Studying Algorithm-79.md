---
title: "BOJ: 10170 NFC West vs North"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

동혁이를 위해 NFC 서부와 북부 디비전 순위를 출력하는 프로그램을 작성하시오.

## 입력

없음

## 출력

예제와 같이 NFC 서부와 북부 디비전 순위를 출력한다.

### 예제 입력 1

```shell

```

### 예제 출력 1

```shell
NFC West       W   L  T
-----------------------
Seattle        13  3  0
San Francisco  12  4  0
Arizona        10  6  0
St. Louis      7   9  0

NFC North      W   L  T
-----------------------
Green Bay      8   7  1
Chicago        8   8  0
Detroit        7   9  0
Minnesota      5  10  1
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

int main(void) {
    cout<<"NFC West       W   L  T\n";
    cout<<"-----------------------\n";
    cout<<"Seattle        13  3  0\n";
    cout<<"San Francisco  12  4  0\n";
    cout<<"Arizona        10  6  0\n";
    cout<<"St. Louis      7   9  0\n\n";
    cout<<"NFC North      W   L  T\n";
    cout<<"-----------------------\n";
    cout<<"Green Bay      8   7  1\n";
    cout<<"Chicago        8   8  0\n";
    cout<<"Detroit        7   9  0\n";
    cout<<"Minnesota      5  10  1";

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/10170)