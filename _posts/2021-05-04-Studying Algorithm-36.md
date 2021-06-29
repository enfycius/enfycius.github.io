---
title: "BOJ: 2739 구구단"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

$$N$$을 입력받은 뒤, 구구단 $$N$$단을 출력하는 프로그램을 작성하시오. 출력 형식에 맞춰서 출력하면 된다.

## 입력

첫째 줄에 $$N$$이 주어진다. $$N$$은 1보다 크거나 같고, 9보다 작거나 같다.

## 출력

출력형식과 같게 $$N*1$$부터 $$N*9$$까지 출력한다.

### 예제 입력 1

```shell
2
```

### 예제 출력 1

```shell
2 * 1 = 2
2 * 2 = 4
2 * 3 = 6
2 * 4 = 8
2 * 5 = 10
2 * 6 = 12
2 * 7 = 14
2 * 8 = 16
2 * 9 = 18
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int n;

    cin>>n;

    if(n >= 1 && n <= 9) 
        for(int i=1; i<10; i++)
            cout<<n<<' '<<'*'<<' '<<i<<' '<<'='<<' '<<n*i<<endl;

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/2739)
