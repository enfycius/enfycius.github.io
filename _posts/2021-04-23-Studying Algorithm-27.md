---
title: "BOJ: 10871 X보다 작은 수"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

정수 $$N$$개로 이루어진 수열 $$A$$와 정수 $$X$$가 주어진다. 이때, $$A$$에서 $$X$$보다 작은 수를 모두 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 $$N$$과 $$X$$가 주어진다. $$(1 \leq N, X \leq 10,000)$$

둘째 줄에 수열 $$A$$를 이루는 정수 $$N$$개가 주어진다. 주어지는 정수는 모두 1보다 크거나 같고, 10,000보다 작거나 같은 정수이다.

## 출력

$$X$$보다 작은 수를 입력받은 순서대로 공백으로 구분해 출력한다. $$X$$보다 작은 수는 적어도 하나 존재한다.

### 예제 입력 1

```shell
10 5
1 10 4 9 2 3 8 5 7 6
```

### 예제 출력 1

```shell
1 4 2 3
```

<br/>

# 코드

```cpp
#include <iostream>

#define MAX 10000

using namespace std;

int main(void) {
    int n, x;
    int arr[MAX] = {0,};

    cin>>n>>x;

    for(int i=0; i<n; i++)
        cin>>arr[i];
    
    for(int i=0; i<n; i++)
        if(arr[i] < x)
            cout<<arr[i]<<' ';

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/10871)
