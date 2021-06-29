---
title: "BOJ: 15059 Hard choice"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

In long flights, airlines offer hot meals. Usually the flight attendants push carts containing the meals down along the aisles of the plane. When a cart reaches your row, you are asked right away: "Chicken, beef, or pasta?" You know your choices, but you have only a few seconds to choose and you don't know how your choice will look like because your neighbor hasn't opened his wrap yet. . .

The flight attendant in this flight decided to change the procedure. First she will ask all passengers what choice of meal they would prefer, and then she will check if the number of meals available in this flight for each choice are enough.

As an example, consider that the available number of meals for chicken, beef and pasta are respectively (80, 20, 40), while the number of passenger's choices for chicken, beef and pasta are respectively (45, 23, 48). In this case, eleven people will surely not receive their selection for a meal, since three passengers who wanted beef and eight passengers who wanted pasta cannot be pleased.

Given the quantity of meals available for each choice and the number of meals requested for each choice, could you please help the flight attendant to determine how many passengers will surely not receive their selection for a meal?

## 입력

The first line contains three integers $$C_{a}, B_{a}$$ and $$P_{a} (0 \leq C_{a}, B_{a}, P_{a} \leq 100)$$, representing respectively the number of meals available for chicken, beef and pasta. The second line contains three integers $$C_{r}, B_{r}$$ and $$P_{r} (0 \leq C_{r}, B_{r}, P_{r} \leq 100)$$, indicating respectively the number of meals requested for chicken, beef and pasta.

## 출력

Output a single line with an integer representing the number of passengers that will surely not receive their selection for a meal.

### 예제 입력 1

```shell
80 20 40
45 23 48
```

### 예제 출력 1

```shell
11
```

### 예제 입력 2

```shell
0 0 0
100 100 100
```

### 예제 출력 2

```shell
300
```

### 예제 입력 3

```shell
41 42 43
41 42 43
```

### 예제 출력 3

```shell
0
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

int main(void) {
    int i[3], j[3];
    int res=0;

    for(int k=0; k<3; k++) cin>>i[k];
    for(int k=0; k<3; k++) cin>>j[k];
    for(int k=0; k<3; k++) if(i[k] < j[k]) res += (j[k] - i[k]);

    cout<<res;

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/15059)