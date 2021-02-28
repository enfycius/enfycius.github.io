---
title: "BOJ: 2581 소수"

classes: wide

categories:
  - Algorithm
tags:
  - BOJ

toc: true
---

# 문제

자연수 $$M$$과 $$N$$이 주어질 때 $$M$$이상 $$N$$이하의 자연수 중 소수인 것을 모두 골라 이들 소수의 합과 최솟값을 찾는 프로그램을 작성하시오.

예를 들어 $$M=60, N=100$$인 경우 60이상 100이하의 자연수 중 소수는 61, 67, 71, 73, 79, 83, 89, 97 총 8개가 있으므로, 이들 소수의 합은 620이고, 최솟값은 61이 된다.

## 입력

입력의 첫째 줄에 $$M$$이, 둘째 줄에 $$N$$이 주어진다.

$$M$$과 $$N$$은 10,000이하의 자연수이며, $$M$$은 $$N$$보다 작거나 같다.

## 출력

$$M$$이상 $$N$$이하의 자연수 중 소수인 것을 모두 찾아 첫째 줄에 그 합을, 둘째 줄에 그 중 최솟값을 출력한다.

단, $$M$$이상 $$N$$이하의 자연수 중 소수가 없을 경우는 첫째 줄에 -1을 출력한다.

### 예제 입력 1

```shell
60
100
```

### 예제 출력 1

```shell
620
61
```

### 예제 입력 2

```shell
64
65
```

### 예제 출력 2

```shell
-1
```

<br/>

# 코드

```cpp
#include <iostream>

#define OPERATOR_MIN(min, var) (min > var) ? min = var : 0

using namespace std;

int prime_chk(int n) {
    int count = 0;

    for(int i=1; i<=n; i++)
        if(n%i == 0)
            count++;

    if(count != 2)
        return 0;
    else
        return 1;
}

void get_prime(int i, int j, int * arr) {

    for(int k=i; k<=j; k++) {
        if(prime_chk(k)) {
                if(arr[2] == 0)
                    arr[1] = k;
                else
                    OPERATOR_MIN(arr[1], k);

                arr[0] += k;
                arr[2]++;
        }
    }
}

int main(void) {
    int i, j;
    int arr[3] = {0,};

    cin>>i>>j;

    if(i>=j)
        get_prime(j, i, arr);
    else
        get_prime(i, j, arr);


    if(arr[2] == 0)
        cout<<-1;
    else
        cout<<arr[0]<<endl<<arr[1];
    
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/2581)