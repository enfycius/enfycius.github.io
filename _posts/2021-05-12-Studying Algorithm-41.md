---
title: "BOJ: 11279 최대 힙"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

널리 잘 알려진 자료구조 중 최대 힙이 있다. 최대 힙을 이용하여 다음과 같은 연산을 지원하는 프로그램을 작성하시오.

1. 배열에 자연수 $$x$$를 넣는다.
2. 배열에서 가장 큰 값을 출력하고, 그 값을 배열에서 제거한다.

프로그램은 처음에 비어있는 배열에서 시작하게 된다.

## 입력

첫째 줄에 연산의 개수 $$N(1 \leq N \leq 100,000)$$이 주어진다. 다음 $$N$$개의 줄에는 연산에 대한 정보를 나타내는 정수 $$x$$가 주어진다. 만약 $$x$$가 자연수라면 배열에 $$x$$라는 값을 넣는(추가하는) 연산이고, $$x$$가 0이라면 배열에서 가장 큰 값을 출력하고 그 값을 배열에서 제거하는 경우이다. 입력되는 자연수는 $$2^{31}$$보다 작다.

## 출력

입력에서 0이 주어진 회수만큼 답을 출력한다. 만약 배열이 비어 있는 경우인데 가장 큰 값을 출력하라고 한 경우에는 0을 출력하면 된다.

### 예제 입력 1

```shell
13
0
1
2
0
0
3
2
1
0
0
0
0
0
```

### 예제 출력 1

```shell
0
2
1
3
2
1
0
0
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

void small(priority_queue<int> *v) {
    if(v->size() == 0)
        printf("0\n");
    else {
        printf("%d\n", v->top());
        v->pop();
    }
}

int main(void) {
    priority_queue<int> v;
    int n;

    scanf("%d", &n);

    for(int i=0; i<n; i++) {
        int k;

        scanf("%d", &k);

        if(k > 0)
            v.push(k);
        else
            small(&v);
    }

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/11279)
