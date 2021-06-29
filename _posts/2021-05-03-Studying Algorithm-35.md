---
title: "BOJ: 10818 최소, 최대"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

$$N$$개의 정수가 주어진다. 이때, 최솟값과 최댓값을 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 정수의 개수 $$N(1 \leq N \leq 1,000,000)$$이 주어진다. 둘째 줄에는 $$N$$개의 정수를 공백으로 구분해서 주어진다. 모든 정수는 $$-1,000,000$$보다 크거나 같고, $$1,000,000$$보다 작거나 같은 정수이다.

## 출력

첫째 줄에 주어진 정수 $$N$$개의 최솟값과 최댓값을 공백으로 구분해 출력한다.

### 예제 입력 1

```shell
5
20 10 35 30 7
```

### 예제 출력 1

```shell
7 35
```

<br/>

# 코드

```cpp
#include <iostream>
#define MAX 1000000

using namespace std;

int main(void) {
    int i, j;
    int min, max;
    int arr[MAX];

    cin>>i;

    for(int j=0; j<i; j++) {
        cin>>arr[j];
    }

    min = arr[0];
    max = arr[0];

    for(int j=1; j<i; j++) {
        if(min > arr[j])
            min = arr[j];
        
        if(max < arr[j])
            max = arr[j];
    }

    cout<<min<<' '<<max;
        
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/10818)
