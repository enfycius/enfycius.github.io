---
title: "BOJ: 10546 배부른 마라토너"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

마라토너라면 국적과 나이를 불문하고 누구나 참가하고 싶어하는 백준 마라톤 대회가 열린다. $$42.195km$$를 달리는 이 마라톤은 모두가 참가하고 싶어했던 만큼 매년 모두가 완주해왔다. 단, 한 명만 빼고!

모두가 참가하고 싶어서 안달인데 이런 백준 마라톤 대회에 참가해 놓고 완주하지 못한 배부른 참가자 한 명은 누굴까?

## 입력

첫째 줄에는 참가자 수 $$N$$이 주어진다. $$(1 \leq N \leq 10^{5})$$

$$N$$개의 줄에는 참가자의 이름이 주어진다.

추가적으로 주어지는 $$N-1$$개의 줄에는 완주한 참가자의 이름이 쓰여져 있다.

참가자들의 이름은 길이가 1보다 크거나 같고, 20보다 작거나 같은 문자열이고, 알파벳 소문자로만 이루어져 있다.

참가자들 중엔 동명이인이 있을 수도 있다.

## 출력

마라톤을 완주하지 못한 참가자의 이름을 출력한다.

### 예제 입력 1

```shell
3
leo
kiki
eden
eden
kiki
```

### 예제 출력 1

```shell
leo
```

### 예제 입력 2

```shell
5
marina
josipa
nikola
vinko
filipa
josipa
filipa
marina
nikola
```

### 예제 출력 2

```shell
vinko
```

### 예제 입력 3

```shell
4
mislav
stanko
mislav
ana
stanko
ana
mislav
```

### 예제 출력 3

```shell
mislav
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>
#include <unordered_map>

using namespace std;

int main(void) {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL); cout.tie(NULL);
    
    unordered_map<string, int> player;
    unordered_map<string, int>:: iterator itr;

    string name;
    int n;

    cin>>n;

    for(int i=0; i<n; i++) {
        cin>>name;

        if(player.find(name) != player.end())
            player[name]++;
        else
            player.insert(make_pair(name, 1));
    }

    for(int i=0; i<n-1; i++) {
        cin>>name;

        if(player.find(name) != player.end())
            player[name]--;
    }

    for(itr=player.begin(); itr != player.end(); itr++)
        if(itr->second != 0)
            cout<<itr->first<<'\n';

    return 0;
}

```

# Reference

[BOJ](https://www.acmicpc.net/problem/10546)
