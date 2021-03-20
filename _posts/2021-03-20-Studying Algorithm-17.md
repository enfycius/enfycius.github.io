---
title: "BOJ: 10816 숫자 카드 2"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

숫자 카드는 정수 하나가 적혀져 있는 카드이다. 상근이는 숫자 카드 $$N$$개를 가지고 있다. 정수 $$M$$개가 주어졌을 때, 이 수가 적혀있는 숫자 카드를 상근이가 몇 개 가지고 있는지 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 상근이가 가지고 있는 숫자 카드의 개수 $$N(1 \leq N \leq 500,000)$$이 주어진다. 둘째 줄에는 숫자 카드에 적혀있는 정수가 주어진다. 숫자 카드에 적혀있는 수는 $$-10,000,000$$보다 크거나 같고, $$10,000,000$$보다 작거나 같다.

셋째 줄에는 $$M(1 \leq M \leq 500,000)$$이 주어진다. 넷째 줄에는 상근이가 몇 개 가지고 있는 숫자 카드인지 구해야 할 $$M$$개의 정수가 주어지며, 이 수는 공백으로 구분되어져 있다. 이 수도 $$-10,000,000$$보다 크거나 같고, $$10,000,000$$보다 작거나 같다.

## 출력

첫째 줄에 입력으로 주어진 $$M$$개의 수에 대해서, 각 수가 적힌 숫자 카드를 상근이가 몇 개 가지고 있는지를 공백으로 구분해 출력한다.

### 예제 입력 1

```shell
10
6 3 2 10 10 10 -10 -10 7 3
8
10 9 -5 2 3 4 5 -10
```

### 예제 출력 1

```shell
3 0 0 1 2 0 0 2
```

<br/>

# 코드

```cpp
#include <iostream>
#include <algorithm>

#define MAX 500001

using namespace std;

int main(void) {
    ios_base::sync_with_stdio(0);
    cin.tie(0);

    int arr_n[MAX];
    int arr_m[MAX];

    int n, m;

    cin>>n;
    
    for(int i=0; i<n; i++)
        cin>>arr_n[i];

    sort(arr_n, arr_n+n);

    cin>>m;

    for(int i=0; i<m; i++) 
        cin>>arr_m[i];

    for(int i=0; i<m; i++) {
        int count = 0;

        int* a = upper_bound(arr_n, arr_n+n, arr_m[i]-1);
        int* b = upper_bound(arr_n, arr_n+n, arr_m[i]);

        for(; a<b; a++)
            count++;

        cout<<count<<' ';
    }
        
    return 0;
}

```

# Reference

[BOJ](https://www.acmicpc.net/problem/10816)