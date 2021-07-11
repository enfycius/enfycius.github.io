---
title: "BOJ: 5339 콜센터"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

스타워즈에 등장하는 로봇인 C3PO는 요즘 콜센터에 근무하고 있다. 콜센터에 앉아있는 C3PO를 그리는 프로그램을 작성하시오.

## 출력

예제 출력처럼 콜센터에 앉아있는 C3PO를 출력한다. 마지막 세 줄의 두 '|' 사이에는 공백이 10개 있다.

### 예제 입력 1

```shell

```

### 예제 출력 1

```shell
     /~\
    ( oo|
    _\=/_
   /  _  \
  //|/.\|\\
 ||  \ /  ||
============
|          |
|          |
|          |
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

int main(void) {
    cout<<"     /~\\\n";
    cout<<"    ( oo|\n";
    cout<<"    _\\=/_\n";
    cout<<"   /  _  \\\n";
    cout<<"  //|/.\\|\\\\\n";
    cout<<" ||  \\ /  ||\n";
    cout<<"============\n";
    cout<<"|          |\n";
    cout<<"|          |\n";
    cout<<"|          |";
    
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/5339)