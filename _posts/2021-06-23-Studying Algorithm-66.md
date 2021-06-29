---
title: "BOJ: 5337 웰컴"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

Welcome을 예제 출력처럼 출력하는 프로그램을 작성하시오.

## 출력

Welcome을 아래 예제 출력처럼 출력한다.

### 예제 입력 1

```shell

```

### 예제 출력 1

```shell
.  .   .
|  | _ | _. _ ._ _  _
|/\|(/.|(_.(_)[ | )(/.
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    cout<<".  .   ."<<endl;
    cout<<"|  | _ | _. _ ._ _  _"<<endl;
    cout<<"|/\\|(/.|(_.(_)[ | )(/.";

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/5337)