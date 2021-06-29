---
title: "BOJ: 1330 두 수 비교하기"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

두 정수 $$A$$와 $$B$$가 주어졌을 때, $$A$$와 $$B$$를 비교하는 프로그램을 작성하시오.

## 입력

첫째 줄에 $$A$$와 $$B$$가 주어진다. $$A$$와 $$B$$는 공백 한 칸으로 구분되어져 있다.

## 출력

첫째 줄에 다음 세 가지 중 하나를 출력한다.

* $$A$$가 $$B$$보다 큰 경우에는 '>'를 출력한다.
* $$A$$가 $$B$$보다 작은 경우에는 '<'를 출력한다.
* $$A$$와 $$B$$가 같은 경우에는 '=='를 출력한다.

## 제한

* $$-10,000 \leq A, B \leq 10,000$$

### 예제 입력 1

```shell
1 2
```

### 예제 출력 1

```shell
<
```

### 예제 입력 2

```shell
10 2
```

### 예제 출력 2

```shell
>
```

### 예제 입력 3

```shell
5 5
```

### 예제 출력 3

```shell
==
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int a, b;

    cin>>a>>b;

    if(a > b) {
        cout<<">"<<endl;
    }else if(a < b) {
        cout<<"<"<<endl;
    }else{
        cout<<"=="<<endl;
    }

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/1330)