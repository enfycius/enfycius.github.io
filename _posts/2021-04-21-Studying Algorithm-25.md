---
title: "BOJ: 10951 A+B - 4"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

두 정수 A와 B를 입력받은 다음, A+B를 출력하는 프로그램을 작성하시오.

## 입력

입력은 여러 개의 테스트 케이스로 이루어져 있다.

각 테스트 케이스는 한 줄로 이루어져 있으며, 각 줄에 A와 B가 주어진다. $$(0 < A, B < 10)$$

## 출력

각 테스트 케이스마다 A+B를 출력한다.

### 예제 입력 1

```shell
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
    int a, b;

    while(1) {
        cin>>a>>b;

        if(cin.eof() == true) {
            break;
        }
        
        if(a <= 0 || b >= 10)
            continue;
        
        cout<<a+b<<endl;
    }
    
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/10951)
