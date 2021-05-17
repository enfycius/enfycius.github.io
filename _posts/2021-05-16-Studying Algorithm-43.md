---
title: "BOJ: 11654 아스키 코드"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

알파벳 소문자, 대문자, 숫자 0-9중 하나가 주어졌을 때, 주어진 글자의 아스키 코드값을 출력하는 프로그램을 작성하시오.

## 입력

알파벳 소문자, 대문자, 숫자 0-9 중 하나가 첫째 줄에 주어진다.

## 출력

입력으로 주어진 글자의 아스키 코드 값을 출력한다.

### 예제 입력 1

```shell
A
```

### 예제 출력 1

```shell
65
```

### 예제 입력 2

```shell
C
```

### 예제 출력 2

```shell
67
```

### 예제 입력 3

```shell
0
```

### 예제 출력 3

```shell
48
```

### 예제 입력 4

```shell
9
```

### 예제 출력 4

```shell
57
```

### 예제 입력 5

```shell
a
```

### 예제 출력 5

```shell
97
```

### 예제 입력 6

```shell
z
```

### 예제 출력 6

```shell
122
```

<br/>

# 코드

```cpp
#include <iostream>
using namespace std;
int main(void) {
    char i;
    cin>>i;
    cout<<static_cast<int>(i);
    return 0;
}
```

<br/>

# Reference

[BOJ](https://www.acmicpc.net/problem/11654)
