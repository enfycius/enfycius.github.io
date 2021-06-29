---
title: "BOJ: 2577 숫자의 개수"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

세 개의 자연수 $$A, B, C$$가 주어질 때 $$A \times B \times C$$를 계산한 결과에 0부터 9까지 각각의 숫자가 몇 번씩 쓰였는지를 구하는 프로그램을 작성하시오.

예를 들어 $$A = 150, B = 266, C = 427$$ 이라면 $$A \times B \times C = 150 \times 266 \times 427 = 17037300$$ 이 되고, 계산한 결과 17037300 에는 0이 3번, 1이 1번, 3이 2번, 7이 2번 쓰였다.

## 입력

첫째 줄에 $$A$$, 둘째 줄에 $$B$$, 셋째 줄에 $$C$$가 주어진다. $$A, B, C$$는 모두 100보다 같거나 크고, $$1,000$$보다 작은 자연수이다.

## 출력

첫째 줄에는 $$A \times B \times C$$의 결과에 0이 몇 번 쓰였는지 출력한다. 마찬가지로 둘째 줄부터 열 번째 줄까지 $$A \times B \times C$$의 결과에 1부터 9까지의 숫자가 각각 몇 번 쓰였는지 차례로 한 줄에 하나씩 출력한다.


### 예제 입력 1

```shell
150
266
427
```

### 예제 출력 1

```shell
3
1
0
2
0
0
0
2
0
0
```

<br/>

# 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
  int num[10] = {0, };
  int a, b, c;
  int t;

  cin>>a>>b>>c;

  t = a*b*c;

  while(1) {
    if(t == 0)
      break;
    
    num[t%10]++;

    t /= 10;
  }

  for(int i=0; i<10; i++)
    cout<<num[i]<<endl;

  return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/2577)