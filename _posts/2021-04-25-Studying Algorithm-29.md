---
title: "BOJ: 11022 A+B - 8"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

두 정수 $$A$$와 $$B$$를 입력받은 다음, $$A + B$$를 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 테스트 케이스의 개수 $$T$$가 주어진다.

각 테스트 케이스는 한 줄로 이루어져 있으며, 각 줄에 $$A$$와 $$B$$가 주어진다. $$(0 < A, B < 10)$$

## 출력

각 테스트 케이스마다 "Case #x: $$A + B = C$$" 형식으로 출력한다.

x는 테스트 케이스 번호이고 1부터 시작하며, $$C$$는 $$A + B$$이다.

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
Case #1: 1 + 1 = 2
Case #2: 2 + 3 = 5
Case #3: 3 + 4 = 7
Case #4: 9 + 8 = 17
Case #5: 5 + 2 = 7
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int n;
    int a, b;

    cin>>n;

    for(int i=0; i<n; i++) {
        cin>>a>>b;

        if(a <= 0 || b >= 10) {
            i--;
            continue;
        }
        
        cout<<"Case #"<<i+1<<':'<<' '<<a<<' '<<'+'<<' '<<b<<' '<<'='<<' '<<a+b<<endl;
    }

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/11022)
