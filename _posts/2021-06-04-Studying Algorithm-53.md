---
title: "BOJ: 17352 여러분의 다리가 되어 드리겠습니다!"

classes: wide

categories:
  - Algorithms
tags:
  - BOJ

toc: true
---

# 문제

선린월드에는 $$N$$개의 섬이 있다. 섬에는 $$1, 2, ..., N$$의 번호가 하나씩 붙어 있다. 그 섬들을 $$N-1$$개의 다리가 잇고 있으며, 어떤 두 섬 사이든 다리로 왕복할 수 있다.

* 어제까지는 그랬다.

"왜 다리가 $$N-1$$개밖에 없냐, 통행하기 불편하다"며 선린월드에 불만을 갖던 욱제가 다리 하나를 무너뜨렸다! 안 그래도 불편한 통행이 더 불편해졌다. 서로 왕복할 수 없는 섬들이 생겼기 때문이다. 일단 급한 대로 정부는 선린월드의 건축가를 고용해, 서로 다른 두 섬을 다리로 이어서 다시 어떤 두 섬 사이든 왕복할 수 있게 하라는 지시를 내렸다.

그런데 그 건축가가 당신이다! 안 그래도 천하제일 코딩대회에 참가하느라 바쁜데...


## 입력

첫 줄에 정수 $$N$$이 주어진다. $$(2 \leq N \leq 300,000)$$

그 다음 $$N-2$$개의 줄에는 욱제가 무너뜨리지 않은 다리들이 잇는 두 섬의 번호가 주어진다.

## 출력

다리로 이을 두 섬의 번호를 출력한다. 여러 가지 방법이 있을 경우 그 중 아무거나 한 방법만 출력한다.

### 예제 입력 1

```shell
4
1 2
1 3
```

### 예제 출력 1

```shell
1 4
```

"4 1"이나 "2 4", "4 3" 등 가능한 정답은 많이 있지만, 아무거나 하나만 출력해야 한다.

### 예제 입력 2

```shell
2
```

### 예제 출력 2

```shell
1 2
```

### 예제 입력 3

```shell
5
1 2
2 3
4 5
```

### 예제 출력 3

```shell
3 4
```

<br/>

# 코드

```cpp
#include <bits/stdc++.h>

using namespace std;

class Djs {
    int* rank;
    int* parent;
    int n;

    public:
    void init(int n) {
        rank = new int[n];
        parent = new int[n];
        this->n = n;
        makeSet();
    }

    void makeSet() {
        for(int i=0; i<n; i++) parent[i] = i+1;
    }

    int find(int x) {
        if(parent[x-1] != x) parent[x-1] = find(parent[x-1]);

        return parent[x-1];
    }

    void Union(int x, int y) {
        int xset = find(x);
        int yset = find(y);

        if(xset == yset) return;

        if(rank[xset-1] < rank[yset-1]) parent[xset-1] = yset;
        else if(rank[xset-1] > rank[yset-1]) parent[yset-1] = xset;
        else { parent[yset-1] = xset; rank[xset-1] = rank[xset-1] + 1;}
    }

    ~Djs() {
        delete[] rank; delete[] parent;
    }
};

int main(void) {
    Djs d;
    int n, k, t;
    int flag=0;

    cin>>n;

    d.init(n);

    for(int i=0; i<n-2; i++) { cin>>k>>t; d.Union(k, t); } 

    for(int i=0; i<n; i++) { 
        for(int j=0; j<n; j++) if(d.find(i+1) != d.find(j+1)) { cout<<i+1<<' '<<j+1; flag=1; break;}
        
        if(flag == 1) break;
    }
    
    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/17352)
