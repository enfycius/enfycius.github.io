---
title: "BOJ: 1934 최소공배수"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

두 자연수 A와 B에 대해서, A의 배수이면서 B의 배수인 자연수를 A와 B의 공배수라고 한다. 이런 공배수 중에서 가장 작은 수를 최소공배수라고 한다. 예를 들어, 6과 15의 공배수는 30, 60, 90등이 있으며, 최소 공배수는 30이다.

두 자연수 A와 B가 주어졌을 때, A와 B의 최소공배수를 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 테스트 케이스의 개수 $$T(1\leq{T}\leq{1,000})$$가 주어진다. 둘째 줄부터 T개의 줄에 걸쳐서 A와 B가 주어진다. $$(1\leq{A, B}\leq{45,000})$$

## 출력

첫째 줄부터 T개의 줄에 A와 B의 최소공배수를 입력받은 순서대로 한 줄에 하나씩 출력한다.

### 예제 입력 1

```shell
3
1 45000
6 10
13 17
```

### 예제 출력 1

```shell
45000
30
221
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int get_least(int * a, int * b) {
    int i=1, j=1;

    if(a < b) {
        while(1) {
            if(*a*i == *b*j)
                break;

            if(*a*i < *b*j)
                i++;
            else
                j++;
        }
    }else{
        while(1) {
            if(*a*i == *b*j)
                break;

            if(*a*i > *b*j)
                j++;
            else
                i++;
        }
    }

    return *a*i;
}

int main(void) {
    int a, b;
    int t;
    int least;

    cin>>t;

    for(int i=0; i<t; i++) {
        cin>>a>>b;

        least = get_least(&a, &b);

        cout<<least<<endl;
    }

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/1934)