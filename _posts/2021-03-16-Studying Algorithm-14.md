---
title: "BOJ: 2164 카드2"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

$$N$$장의 카드가 있다. 각각의 카드는 차례로 1부터 $$N$$까지의 번호가 붙어 있으며, 1번 카드가 제일 위에, $$N$$번 카드가 제일 아래인 상태로 순서대로 카드가 놓여 있다.

이제 다음과 같은 동작을 카드가 한 장 남을 때까지 반복하게 된다. 우선, 제일 위에 있는 카드를 바닥에 버린다. 그 다음, 제일 위에 있는 카드를 제일 아래에 있는 카드 밑으로 옮긴다.

예를 들어 $$N=4$$인 경우를 생각해 보자. 카드는 제일 위에서부터 1234 의 순서로 놓여있다. 1을 버리면 234가 남는다. 여기서 2를 제일 아래로 옮기면 342가 된다. 3을 버리면 42가 되고, 4를 밑으로 옮기면 24가 된다. 마지막으로 2를 버리고 나며, 남는 카드는 4가 된다.

$$N$$이 주어졌을 때, 제일 마지막에 남게 되는 카드를 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 정수 $$N(1 \leq N \leq 500,000)$$이 주어진다.

## 출력

첫째 줄에 남게 되는 카드의 번호를 출력한다.

### 예제 입력 1

```shell
6
```

### 예제 출력 1

```shell
4
```

<br/>

# 코드

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main(void) {
    queue<int> q;

    int n;

    cin>>n;

    for(int i=0; i<n; i++)
        q.push(i+1);

    while(q.size() != 1) {
        q.pop();
        int temp = q.front();
        q.pop();
        q.push(temp);
    }

    cout<<q.front();

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/2164)