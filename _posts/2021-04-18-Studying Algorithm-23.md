---
title: "BOJ: 10988 팰린드롬인지 확인하기"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

알파벳 소문자로만 이루어진 단어가 주어진다. 이때, 이 단어가 팰린드롬인지 아닌지 확인하는 프로그램을 작성하시오.

팰린드롬이란 앞으로 읽을 때와 거꾸로 읽을 때 똑같은 단어를 말한다.

level, noon은 팰린드롬이고, baekjoon, online, judge는 팰린드롬이 아니다.

## 입력

첫째 줄에 단어가 주어진다. 단어의 길이는 1보다 크거나 같고, 100보다 작거나 같으며, 알파벳 소문자로만 이루어져 있다.

## 출력

첫째 줄에 팰린드롬이면 1, 아니면 0을 출력한다.

### 예제 입력 1

```shell
level
```

### 예제 출력 1

```shell
1
```

### 예제 입력 2

```shell
baekjoon
```

### 예제 출력 2

```shell
0
```

<br/>

# 코드

```cpp
#include <iostream>
#include <cstring>

using namespace std;

int is_palin(char* s, int len) {
    int i=0, j=len-1;

    while(i<j && s[i] == s[j]) {
        i++;j--;
    }

    if((i == j) || (j < i))
        return 1;
    else
        return 0;
}


int main(void) {
    char s[101];
    int check;

    cin>>s;

    for(int i=0; i<strlen(s); i++)
        if(int(s[i]) < 97 || int(s[i]) > 122)
            return 0;
    
    check = is_palin(s, strlen(s));

    if(check == 1)
        cout<<"1";
    else
        cout<<"0";

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/10988)
