---
title: "BOJ: 2588 곱셈"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

(세 자리 수) $$\times$$ (세 자리 수)는 다음과 같은 과정을 통하여 이루어진다.

![Figure](https://www.acmicpc.net/upload/images/f5NhGHVLM4Ix74DtJrwfC97KepPl27s%20(1).png)

(1)과 (2) 위치에 들어갈 세 자리 자연수가 주어질 때 (3), (4), (5), (6) 위치에 들어갈 값을 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 (1)의 위치에 들어갈 세 자리 자연수가, 둘째 줄에 (2)의 위치에 들어갈 세자리 자연수가 주어진다.

## 출력

첫째 줄부터 넷째 줄까지 차례대로 (3), (4), (5), (6)에 들어갈 값을 출력한다.

### 예제 입력 1

```shell
472
385
```

### 예제 출력 1

```shell
2360
3776
1416
181720
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int a, b, t;

    cin>>a>>b;
    
    t = b;

    while(1) {
        if(t == 0)
            break;

        cout<<a * (t % 10)<<'\n';

        t /= 10;
    }

    cout<<a*b;
        
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/2588)