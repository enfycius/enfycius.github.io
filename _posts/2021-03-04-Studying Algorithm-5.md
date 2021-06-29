---
title: "BOJ: 1152 단어의 개수"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

영어 대소문자와 띄어쓰기만으로 이루어진 문자열이 주어진다. 이 문자열에는 몇 개의 단어가 있을까? 이를 구하는 프로그램을 작성하시오. 단, 한 단어가 여러 번 등장하면 등장한 횟수만큼 모두 세어야 한다.

## 입력

첫 줄에 영어 대소문자와 띄어쓰기로 이루어진 문자열이 주어진다. 이 문자열의 길이는 1,000,000을 넘지 않는다. 단어는 띄어쓰기 한 개로 구분되며, 공백이 연속해서 나오는 경우는 없다. 또한 문자열의 앞과 뒤에는 공백이 있을 수도 있다.

## 출력

첫째 줄에 단어의 개수를 출력한다.

### 예제 입력 1

```shell
The Curious Case of Benjamin Button
```

### 예제 출력 1

```shell
6
```

### 예제 입력 2

```shell
 Mazatneunde Wae Teullyeoyo
```

### 예제 출력 2

```shell
3
```

### 예제 입력 3

```shell
Teullinika Teullyeotzi
```

### 예제 출력 3

```shell
2
```

<br/>

# 코드

```cpp
#include <iostream>

#define MAX 1000000

using namespace std;

int main(void) {
    char str[MAX] = {0,};
    int i=0;
    int count = 0;

    cin.getline(str, sizeof(str));

    while(str[i] != 0) {

        if(i == 0) 
            if((str[i] >= 65 && str[i] <= 90) || (str[i] >= 97 && str[i] <= 122))
                count++;  
        
        if(i < MAX - 1) 
            if(str[i] == ' ' && ((str[i+1] >= 65 && str[i+1] <= 90) || (str[i+1] >= 97 && str[i+1] <= 122))
                count++;          
        
        i++;
    }

    cout<<count;

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/1152)