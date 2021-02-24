---
title: "BOJ: 12755 수면 장애"

classes: wide

categories:
  - Algorithm
tags:
  - BOJ

toc: true
---

# 문제

수면 장애를 가진 강민이는 잠이 오지 않아 적잖은 고통을 느끼고 있다. 강민이는 잠이 오지 않을 때마다 속으로 양을 세고 있었는데, 오늘따라 백만 마리까지 세었는데도 잠이 오지 않았다.

한계를 느낀 강민이는 새로운 방법으로 수를 세기로 했다.

1부터 숫자를 쭉 이어 붙이면 다음과 같은 숫자열이 생성된다.

12345678910111213...

강민이는 이 숫자열을 한 숫자씩 떼어서 읽기 시작했다. 수면에 성공한 강민이는 다음날 일어나자마자 "$$N$$번째 숫자까지 읽었어!" 라고 기분 좋게 외쳤다.

과연 $$N$$번째 숫자는 무엇일까?

## 입력

첫째 줄에 $$N$$번째 숫자를 나타내는 $$N$$이 주어진다. $$(1\leq{N}\leq{100,000,000})$$

## 출력

첫째 줄에 $$N$$번째 숫자에 해당하는 0~9 중 한 숫자를 출력하시오.

### 예제 입력 1

```shell
15
```

### 예제 출력 1

```shell
2
```

<br/>

# 코드

```cpp
#include <iostream>
#include <stack>

using namespace std;

int main(void) {
    stack<int> s;
    int n, k;
    int mod;
    int count = 0;
    int pos = 1;
    int chk;
    int con = 0;

    cin>>n;

    for(int i=1; i<=n; i++) {
        k = i;
        count = 0;

        while(1) {
            if(k == 0) 
                break;
            
            mod = k % 10;
            s.push(mod);
            k /= 10;
            count++;
        }

        while(count != 0) {
            chk = s.top();
            s.pop();
            
            if(pos == n) {
                con = 1;
                break;
            }
                
            pos++;
            count--;
        }

        if(con == 1)
            break;

    }

    cout<<chk;

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/12755)
