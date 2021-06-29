---
title: "BOJ: 9498 시험 성적"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

시험 점수를 입력받아 90 ~ 100점은 A, 80 ~ 89점은 B, 70 ~ 79점은 C, 60 ~ 69점은 D, 나머지 점수는 F를 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 시험 점수가 주어진다. 시험 점수는 0보다 크거나 같고, 100보다 작거나 같은 정수이다.

## 출력

시험 성적을 출력한다.

### 예제 입력 1

```shell
100
```

### 예제 출력 1

```shell
A
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int grade;

    cin>>grade;

    if(grade >= 90) {
        cout<<'A';
    }else if(grade >= 80) {
        cout<<'B';
    }else if(grade >= 70) {
        cout<<'C';
    }else if(grade >= 60) {
        cout<<'D';
    }else{
        cout<<'F';
    }

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/9498)