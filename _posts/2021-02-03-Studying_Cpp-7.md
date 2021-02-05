---
title: "C++ 함수 템플릿의 정의"

classes: wide

categories:
  - C++
tags:
  - C++
  - Programming
  - Coding

toc: true
---

# 문제

인자로 전달되는 두 변수에 저장된 값을 서로 교환하는 SwapData라는 이름의 함수를 템플릿으로 정의해보자.

그리고 다음 Point 클래스를 대상으로 값의 교환이 이뤄짐을 확인할 수 있도록 main 함수를 구성해보자.


```cpp
class Point
{
private:
    int xpos, ypos;

public:
    Point(int x=0, int y=0) : xpos(x), ypos(y) { }

    void ShowPosition() const
    {
        cout<<'['<<xpos<<", "<<ypos<<']'<<endl;
    }
};
```

# 해결

## 코드

```cpp
#include <iostream>
 
using namespace std;
 
template <typename T>
 
void SwapData(T num1, T num2)
{
    int temp = *num1;
    *num1 = *num2;
    *num2 = temp;
}
 
class Point
{
private:
    int xpos, ypos;
 
public:
    Point(int x=0, int y=0) : xpos(x), ypos(y) { }
 
    void ShowPosition() const
    {
        cout << '[' << xpos << ", " << ypos << ']' << endl;
    }
 
    int* GetX()
    {
        return &xpos;
    }
 
    int* GetY()
    {
        return &ypos;
    }
};
 
int main(void)
{
    Point pos(1, 2);
    
    SwapData(pos.GetX(), pos.GetY());
 
    pos.ShowPosition();
 
    return 0;
}
```