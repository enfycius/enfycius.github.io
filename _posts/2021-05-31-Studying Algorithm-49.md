---
title: "BOJ: 14681 사분면 고르기"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

흔한 수학 문제 중 하나는 주어진 점이 어느 사분면에 속하는지 알아내는 것이다. 사분면은 아래 그림처럼 1부터 4까지 번호를 갖는다. "Quadrant n"은 "제n사분면"이라는 뜻이다.

![Figure](/assets/images/algorithm/14681-figure.png)

예를 들어, 좌표가 $$(12,5)$$인 점 $$A$$는 $$x$$좌표와 $$y$$좌표가 모두 양수이므로 제1사분면에 속한다. 점 $$B$$는 $$x$$좌표가 음수이고 $$y$$좌표가 양수이므로 제2사분면에 속한다.

점의 좌표를 입력받아 그 점이 어느 사분면에 속하는지 알아내는 프로그램을 작성하시오. 단, $$x$$좌표와 $$y$$좌표는 모두 양수나 음수라고 가정한다.

## 입력

첫 줄에는 정수 $$x$$가 주어진다. $$(-1000 \leq x \leq 1000; x \neq 0)$$ 다음 줄에는 정수 $$y$$가 주어진다. $$(-1000 \leq y \leq 1000; y \neq 0)$$

## 출력

점 $$(x, y)$$의 사분면 번호(1, 2, 3, 4 중 하나)를 출력한다.

### 예제 입력 1

```shell
12
5
```

### 예제 출력 1

```shell
1
```

### 예제 입력 2

```shell
9
-13
```

### 예제 출력 2

```shell
4
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int x;
    int y;

    cin>>x;
    cin>>y;

    if(x > 0 && y > 0)
        cout<<1;
    else if(x > 0 && y < 0)
        cout<<4;
    else if(x < 0 && y > 0)
        cout<<2;
    else if(x < 0 && y < 0)
        cout<<3;
    
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/14681)