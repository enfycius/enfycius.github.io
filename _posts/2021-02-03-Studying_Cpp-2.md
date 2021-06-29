---
title: "C++ 연산자 오버로딩"

classes: wide

categories:
  - Cpp
tags:
  - C++
  - Programming
  - Coding

toc: true
---

# 문제

## C++ 기반의 데이터 입출력 문제

이번에는 재미 삼아서(정말로 재미 삼아서) 2차원 배열접근에 대한 연산자 오버로딩을 진행하고자 한다.
실제로 이렇게까지 연산자를 직접 오버로딩 하는 경우는 거의 없다.
다만, 필자는 호기심을 유발 및 충족시킨다는 측면에서 이 문제를 제시하는 것이다.
그러니 여러분도 이 문제에 단순한 호기심과 즐거움을 느꼈으면 좋겠다.
그럼 문제를 제시하겠다.
다음의 이름으로 클래스를 정의하자.

```cpp
class BoundCheck2DIntArray { .... }
```

이 클래스는 BoundCheckIntArray 클래스의 2차원 배열 버전이다.
따라서 다음과 같이 객체를 생성하면,

```cpp
BoundCheck2DIntArray arr2d(3, 4);
```

세로와 가로의 길이가 각각 3과 4인, int형 2차원 배열처럼 동작하는 arr2d 객체가 생성되어, 다음의 형태로 데이터를 저장 및 참조할 수 있어야 한다.

```cpp
for(int n=0; n<3; n++)
    for(int m=0; m<4; m++)
        arr2d[n][m] = n+m;

for(int n=0; n<3; n++)
{
    for(int m=0; m<4; m++)
        cout<<arr2d[n][m]<<' ';
    cout<<endl;
}
```

참고로 두 개의 [] 연산자를 동시에 오버로딩 하는 것은 허용되지 않기 때문에, 위의 다음 문장은,

```cpp
arr2d[n][m];
```

두 번의 [] 연산자 호출을 동반하게끔 구현해야 한다.
즉, 첫 번째 [] 연산에 의해서 위의 문장은 다음과 같이 해석되어야 하며,

```cpp
(arr2d.operator[](n))[m];
```

그리고 arr2d.operator[](n) 연산의 반환 값을 이용해서 두 번째 [] 연산은 다음과 같이 해석되어야 한다.

```cpp
((반환 값).operator[])(m);
```

참고로 이는 호기심 유발 이상의 의미를 갖지는 않지만, 제법 수준이 높은 문제이니(본서의 검토 과정에서 제법 수준이 높은 게 아니고 많이 수준이 높다는 의견이 있었다), 풀지 못했다고 해서 실망할 필요는 없다.

# 풀이

## 코드

```cpp
#include <iostream>
#include <cstdlib>
 
using namespace std;
 
class BoundCheck2DIntArray
{
private:
    int *arr;
 
    int arrlen[2];
    int value[2];
    int p;
 
    BoundCheck2DIntArray(const BoundCheck2DIntArray& arr) {}
    BoundCheck2DIntArray& operator=(const BoundCheck2DIntArray& arr) {}
 
public:
    BoundCheck2DIntArray(int i, int j)
    {
        arr = new int[i*j];
        arrlen[0] = i;
        arrlen[1] = j;
        p = 0;
    }
 
    BoundCheck2DIntArray& operator[] (int idx)
    {
        if (p == 2)
            p = 0;
 
        if (idx < 0 || idx >= arrlen[p])
        {
            cout << "Array index out of bound exception" << endl;
            exit(1);
        }
 
        value[p++] = idx;
 
        return *this;
    }
 
    void operator=(int result)
    {
        if (p != 2)
        {
            cout << "not [][]" << endl;
            exit(1);
        }
 
        arr[arrlen[1] * value[0] + value[1]] = result;
    }
 
    int GetArr() const { return *arr; }
    ~BoundCheck2DIntArray() { delete[] arr; }
    friend ostream& operator<<(ostream& os, const BoundCheck2DIntArray& pos);
};
 
ostream& operator<<(ostream& os, const BoundCheck2DIntArray& pos)
{
    if (pos.p != 2)
    {
        cout << "not [][]" << endl;
        exit(1);
    }
 
    os << pos.arr[pos.arrlen[1] * pos.value[0] + pos.value[1]];
 
    return os;
}
 
int main(void)
{
    BoundCheck2DIntArray arr2d(3, 4);
    BoundCheck2DIntArray arr3d(9, 10);
 
    for (int n = 0; n < 3; n++)
        for (int m = 0; m < 4; m++)
            arr2d[n][m] = n + m;
 
    for (int n = 0; n < 3; n++)
    {
        for (int m = 0; m < 4; m++)
            cout << arr2d[n][m] << ' ';
        cout << endl;
    }
 
    cout << endl;
 
    for (int n = 0; n < 9; n++)
        for (int m = 0; m < 10; m++)
            arr3d[n][m] = n + m;
 
    for (int n = 0; n < 9; n++)
    {
        for (int m = 0; m < 10; m++)
            cout << arr3d[n][m] << ' ';
        cout << endl;
    }
 
    return 0;
}
 
```