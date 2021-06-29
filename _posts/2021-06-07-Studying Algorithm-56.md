---
title: "BOJ: 1978 소수 찾기"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

주어진 수 $$N$$개 중에서 소수가 몇 개인지 찾아서 출력하는 프로그램을 작성하시오.

## 입력

첫 줄에 수의 개수 $$N$$이 주어진다. $$N$$은 100이하이다. 다음으로 $$N$$개의 수가 주어지는데 수는 $$1,000$$ 이하의 자연수이다.

## 출력

주어진 수들 중 소수의 개수를 출력한다.

### 예제 입력 1

```shell
4
1 3 5 7
```

### 예제 출력 1

```shell
3
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int n;
    int arr[100] = {0,};
    int count = 0;
    int chk = 0;

    cin>>n;

    for(int i=0; i<n; i++)
        cin>>arr[i];

    for(int i=0; i<n; i++) {
        chk = 0;
        
        for(int j=1; j<=arr[i]; j++)
            if(arr[i] % j == 0)
                chk++;

        if(chk == 2)
            count++;
    }

    cout<<count;

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/1978)