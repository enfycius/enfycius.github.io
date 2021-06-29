---
title: "BOJ: 1920 수 찾기"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

$$N$$개의 정수 $$A[1], A[2], \cdots, A[N]$$이 주어져 있을 때, 이 안에 $$X$$라는 정수가 존재하는지 알아내는 프로그램을 작성하시오.

## 입력

첫째 줄에 자연수 $$N(1 \leq N \leq 100,000)$$이 주어진다. 다음 줄에는 $$N$$개의 정수 $$A[1], A[2], \cdots, A[N]$$이 주어진다. 다음 줄에는 $$M(1 \leq M \leq 100,000)$$이 주어진다. 다음 줄에는 $$M$$개의 수들이 주어지는데, 이 수들이 $$A$$안에 존재하는지 알아내면 된다. 모든 정수의 범위는 $$-2^{31}$$보다 크거나 같고 $$2^{31}$$보다 작다.

## 출력

$$M$$개의 줄에 답을 출력한다. 존재하면 1을, 존재하지 않으면 0을 출력한다.

### 예제 입력 1

```shell
5
4 1 5 2 3
5
1 3 7 9 5
```

### 예제 출력 1

```shell
1
1
0
0
1
```

<br/>

# 코드

```cpp
#include <iostream>

#define EXCHANGE(x, y, temp) temp = x; x = y; y = temp;
#define MAX 100001

using namespace std;

int partition(int* arr_n, int low, int high) {
    int first = low;
    int pivot = arr_n[first];
    int temp;

    while(low <= high) {
        while(arr_n[low] <= pivot && low < high)
            ++low;
        while(arr_n[high] >= pivot && low <= high)
            --high;
        
        if(low < high) {
            EXCHANGE(arr_n[low], arr_n[high], temp);
        }else {
            break;
        }
            
    }

    EXCHANGE(arr_n[first], arr_n[high], temp);

    return high;
}

void quick_sort(int* arr_n, int low, int high) {

    if(high > low) {
        int index = partition(arr_n, low, high);
        quick_sort(arr_n, low, index - 1);
        quick_sort(arr_n, index + 1, high);
    }
}

int binary_search(const int* arr_n, int n, int x) {
    int low = 0, mid, high = n;

    while(low <= high) {
        mid = (low+high)/2;

        if(x == arr_n[mid])
            return 1;
        else if(x < arr_n[mid])
            high = mid - 1;
        else
            low = mid + 1;
    }
    
    return 0;
}


int main(void) {
    int arr_n[MAX];
    int arr_m[MAX];
    int arr_t[MAX];

    int n, m;

    cin>>n;

    for(int i=0; i<n; i++)
        cin>>arr_n[i];

    quick_sort(arr_n, 0, n-1);

    cin>>m;

    for(int i=0; i<m; i++)
        cin>>arr_m[i];

    for(int i=0; i<m; i++) {
        if(binary_search(arr_n, n-1, arr_m[i]))
            arr_t[i] = 1;
        else
            arr_t[i] = 0;
    }

    for(int i=0; i<m; i++)
        cout<<arr_t[i]<<'\n';
        
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/1920)