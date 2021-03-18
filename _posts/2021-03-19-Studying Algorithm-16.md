---
title: "BOJ: 1003 피보나치 함수"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

다음 소스는 $$N$$번째 피보나치 수를 구하는 C++ 함수이다.

```cpp
int fibonacci(int n) {
    if (n == 0) {
        printf("0");
        return 0;
    } else if (n == 1) {
        printf("1");
        return 1;
    } else {
        return fibonacci(n-1) + fibonacci(n-2);
    }
}
```

fibonacci(3)을 호출하면 다음과 같은 일이 일어난다.

* fibonacci(3)은 fibonacci(2)와 fibonacci(1) (첫 번째 호출)을 호출한다.
* fibonacci(2)는 fibonacci(1) (두 번째 호출)과 fibonacci(0)을 호출한다. 
* 두 번째 호출한 fibonacci(1)은 1을 출력하고 1을 리턴한다.
* fibonacci(0)은 0을 출력하고, 0을 리턴한다.
* fibonacci(2)는 fibonacci(1)과 fibonacci(0)의 결과를 얻고, 1을 리턴한다.
* 첫 번째 호출한 fibonacci(1)은 1을 출력하고, 1을 리턴한다.
* fibonacci(3)은 fibonacci(2)와 fibonacci(1)의 결과를 얻고, 2를 리턴한다.

1은 2번 출력되고, 0은 1번 출력된다. $$N$$이 주어졌을 때, fibonacci(N) 을 호출했을 때, 0과 1이 각각 몇 번 출력되는지 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 테스트 케이스의 개수 $$T$$가 주어진다.

각 테스트 케이스는 한 줄로 이루어져 있고, $$N$$이 주어진다. $$N$$은 40보다 작거나 같은 자연수 또는 0이다.

## 출력

각 테스트 케이스마다 0이 출력되는 횟수와 1이 출력되는 횟수를 공백으로 구분해서 출력한다.

### 예제 입력 1

```shell
3
0
1
3
```

### 예제 출력 1

```shell
1 0
0 1
1 2
```

<br/>

# 코드

```cpp
#include <iostream>

#define MAX 41

using namespace std;

int fibonacci(int* value, int* zero, int* one, int* check, int n, int t, int k) {
    if(n == 0) { 
        if(check[k] == 0) {
            zero[t]++;
        }
        return 0;
    } else if(n == 1) {
        if(check[k] == 0) {
            one[t]++;
        }
        return 1;
    }
    
    if(value[n] == 0) {
        value[n] = fibonacci(value, zero, one, check, n-2, n, k) + fibonacci(value, zero, one, check, n-1, n, k);

        if(n != k) {
            zero[t] += zero[n];
            one[t] += one[n];
        }
        check[n] = 1;
    } else {
        if(check[k] == 0) {
            zero[t] += zero[n];
            one[t] += one[n];
        }
    }

    return value[n];
}


int main(void) {
    int value[MAX]={0,};
    int zero[MAX]={0,};
    int one[MAX]={0,};
    int check[MAX]={0, };
    int t;
    int n;

    cin>>t;

    for(int i=0; i<t; i++) {
        cin>>n;
        fibonacci(value, zero, one, check, n, n, n);
        cout<<zero[n]<<' '<<one[n]<<'\n';
    }

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/1003)