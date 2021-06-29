---
title: "C++ IS-A 관계의 상속, 두 번째"

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

정사각형을 의미하는 Square 클래스와 직사각형을 의미하는 Rectangle 클래스를 정의하고자 한다.

그런데 정사각형은 직사각형의 일종이므로, 다음의 형태로 클래스의 상속 관계를 구성하고자 한다.

```cpp
class Rectangle
{
    ...
};

class Square : public Rectangle
{
    ...
};

```

이에 다음 main 함수와 함께 실행이 가능하도록 위의 클래스를 완성해보자.
참고로 상속을 한다고 해서 유도 클래스에 무엇인가를 많이 담아야 한다는 생각을 버리자!

## main 함수

```cpp
int main(void)
{
    Rectangle rec(4, 3);
    rec.ShowAreaInfo();

    Square sqr(7);
    sqr.ShowAreaInfo();

    return 0;
}
```

## 실행의 예

면적: 12
면적: 49

# 해결

## 코드

```cpp
#include <iostream>
 
using namespace std;
 
class Rectangle
{
private:
    int hor;
    int ver;
    int area;
 
public:
    Rectangle(int my_hor, int my_ver) : hor(my_hor), ver(my_ver)
    {
        area = hor*ver;
    }
 
    void ShowAreaInfo()
    {
        cout << "면적: " << area << endl;
    }
};
 
class Square : public Rectangle
{
private:
    int line;
 
public:
    Square(int my_line) : Rectangle(my_line, my_line)
    {}
};
 
int main(void)
{
    Rectangle rec(4, 3);
    rec.ShowAreaInfo();
 
    Square sqr(7);
    sqr.ShowAreaInfo();
 
    return 0;
}

```