---
title: "BOJ: 10950 A + B - 3"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

두 정수 $$A$$와 $$B$$를 입력받은 다음, $$A+B$$를 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 테스트 케이스의 개수 $$T$$가 주어진다.

각 테스트 케이스는 한 줄로 이루어져 있으며, 각 줄에 $$A$$와 $$B$$가 주어진다. $$(0 < A, B < 10)$$

## 출력

각 테스트 케이스마다 $$A+B$$를 출력한다.

### 예제 입력 1

```shell
5
1 1
2 3
3 4
9 8
5 2
```

### 예제 출력 1

```shell
2
5
7
17
7
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int a, b, t;

    cin>>t;

    for(int i=0; i<t; i++) {
        cin>>a>>b;
        
        cout<<a+b<<endl;
    }

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/10950)