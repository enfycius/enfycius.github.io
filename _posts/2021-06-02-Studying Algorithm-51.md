---
title: "BOJ: 10940 BASE16 인코딩"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

문자열 $$S$$가 주어졌을 때, $$S$$를 BASE16 인코딩해 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 문자열 $$S$$가 주어진다. $$S$$는 알파벳 대문자와 소문자, 그리고 숫자로만 이루어져 있으며, 길이는 최대 50이다.

## 출력

첫째 줄에 $$S$$를 BASE16으로 인코딩한 값을 출력한다.

### 예제 입력 1

```shell
Baekjoon
```

### 예제 출력 1

```shell
4261656B6A6F6F6E
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

int main(void) {
    ios_base::sync_with_stdio(false); cin.tie(NULL); cout.tie(NULL);
    char base16[16] = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F'};
    char str[51];
    int i=0;

    cin>>str;

    while(str[i] != '\0') {
        cout<<base16[(int(str[i])/16)%16];
        cout<<base16[int(str[i])%16];
        i++;
    }

    return 0;
}

```

# Reference

[BOJ](https://www.acmicpc.net/problem/10940)
