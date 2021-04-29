---
title: "BOJ: 2750 수 정렬하기"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

$$N$$개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.

## 입력

첫째 줄에 수의 개수 $$N(1 \leq N \leq 1,000)$$이 주어진다. 둘째 줄부터 $$N$$개의 줄에는 숫자가 주어진다. 이 수는 절댓값이 $$1,000$$보다 작거나 같은 정수이다. 수는 중복되지 않는다.

## 출력

첫째 줄부터 $$N$$개의 줄에 오름차순으로 정렬한 결과를 한 줄에 하나씩 출력한다.

### 예제 입력 1

```shell
5
5
2
3
4
1
```

### 예제 출력 1

```shell
1
2
3
4
5
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int arr[1000];
    int n;
    int temp;

    cin>>n;

    for(int i=0; i<n; i++)
        cin>>arr[i];

    for(int i=0; i<n; i++) 
        for(int j=i; j<n; j++) 
            if(arr[i] > arr[j]) {
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }

    for(int i=0; i<n; i++)
        cout<<arr[i]<<endl;

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/2750)
