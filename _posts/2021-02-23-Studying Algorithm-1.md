---
title: "BOJ: 17254 키보드 이벤트"

classes: wide

categories:
  - Algorithm
tags:
  - BOJ

toc: true
---

# 문제

키보드에서 어떤 키를 누르면 어떤 키가 눌러졌는지 컴퓨터에 전송되고, 컴퓨터에서는 키가 눌러진 순서대로 화면에 출력된다.

승지는 팀 과제로 보고서 100장을 작성해야 하는 데, 마감 시간이 얼마 남지 않아서 팀원에게 도움을 요청하였다. 하지만 컴퓨터가 하나뿐이라 보고서를 동시에 작성할 수 없었다.

주변을 둘러보니 쓰지 않는 키보드가 여러 개가 바닥에서 굴러다니는 것을 보았다. 급한 대로 컴퓨터에 키보드 여러 개를 연결해서 타자 속도를 올리기로 했다.

문제는 원하는 문장을 작성하기 위해서는 서로 호흡을 잘 맞춰야 하는데, 키보드의 동작 원리를 아직 알지 못했던 승지는 어떤 결과가 출력될지 알 수 없었다.

승지는 팀원 N명에게 N개의 키보드를 나눠주고 전부 컴퓨터에 연결했다. 각자 어느 시간에 어떤 키를 누를지를 미리 정한다면, 어떤 결과가 화면에 출력될 것인지를 알아내고자 한다.

키보드의 번호는 컴퓨터에 연결된 순서대로 1번 키보드, 2번 키보드, ... N번 키보드이다. 동시에 여러 키보드에서 키를 누른다면 번호가 작은 키보드에서 누른 키가 먼저 출력되지만, 하나의 키보드에서 여러 개의 키를 동시에 누를 수는 없다. 즉, 하나의 키보드에서 각 키를 누른 시간은 모두 다르다.

## 입력

첫째 줄에 연결된 키보드의 개수 N과, 키보드를 누르게 될 횟수 M이 주어진다. $$(1\leq{a}\leq{N}, 0\leq{b}\leq{1,000,000})$$

다음 M개의 줄에 정수 a, b와 문자 c가 주어진다. 이는 a번 키보드로, b초에 문자 c가 적힌 키를 누를 것이라는 의미이다. $$(1\leq{a}\leq{N}, 0\leq{b}\leq{1,000,000})$$

키보드에는 알파벳 대문자와 숫자키만 존재한다.

## 출력

모든 입력이 끝난 후에 화면에 출력될 결과를 출력한다.

### 예제 입력 1

```shell
3 5
1 0 A
2 1 P
1 2 L
2 4 E
3 0 P
```

### 예제 출력 1

```shell
APPLE
```

### 예제 입력 2

```shell
2 7
1 6 B
1 1 A
1 0 L
1 3 D
2 8 G
2 6 U
2 3 Y
```

### 예제 출력 2

```shell
LADYBUG
```

<br/>

# 코드

```cpp
#include <iostream>

#define MAX 1000

#define OPERATOR_MAX(max, var) (max < var) ? max = var : 0

using namespace std;

void sorting(int * index, int * a, int m) {
    int temp;

    int arr[MAX] = {0,};

    for(int i=0; i<m; i++)
        arr[i] = a[i];

    for(int i=0; i<m; i++) {
        for(int j=i; j<m; j++) {

            if(arr[j] < arr[i]) {
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;

                temp = index[i];
                index[i] = index[j];
                index[j] = temp;
            }
        }
    }
}

int get_max(int * b, int m) {
    int max = b[0];

    for(int i=1; i<m; i++)
        OPERATOR_MAX(max, b[i]);

    return max;
}

void get_string(int * index, int * a, int * b, char * c, int m) {

    int max = get_max(b, m);
    
    for(int j=0; j<=max; j++)
        for(int k=0; k<m; k++)
            if(b[index[k]] == j)
                cout<<c[index[k]];            
        
}

int main(void) {
    int n, m;
    int a[MAX] = {0,};
    int b[MAX] = {0,};
    char c[MAX] = {0,};
    int index[MAX] = {0,};

    cin>>n>>m;

    for(int i=0; i<m; i++) {
        cin>>a[i]>>b[i]>>c[i];

        if(a[i]>n || a[i]<1) {
            i--;
            continue;
        }
            
        if((c[i] < 48 || c[i] > 57) && (c[i] < 65 || c[i] > 90)) {
            i--;
            continue;
        }

        index[i] = i;
    }

    sorting(index, a, m);
    get_string(index, a, b, c, m);

    return 0;
}
```

# Reference

[BOJ](https://www.acmicpc.net/problem/17254)
