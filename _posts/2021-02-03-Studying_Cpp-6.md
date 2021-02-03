---
title: "C++ 다형성"

classes: wide

categories:
  - C++
tags:
  - C++
  - Programming
  - Coding
---

# 개념

**'다형성'** 이란 **'동질이상'** 을 의미한다.

즉, **"모습은 같은데 형태는 다르다."**

이를 C++에 적용하면, **"문장은 같은데 결과는 다르다."**는 것이다.

# 코드

```cpp
#include <iostream>
 
using namespace std;
 
class First
{
public:
    virtual void SimpleFunc() { cout << "First" << endl; }
};
 
class Second : public First
{
public:
    virtual void SimpleFunc() { cout << "Second" << endl; }
};
 
int main(void)
{
    First* ptr = new First();
    ptr->SimpleFunc();
    delete ptr;
 
    ptr = new Second();
    ptr->SimpleFunc();
    delete ptr;
 
    return 0;
}
```

상속관계에 놓여있는 First와 Second 클래스를 보면,

![Figure](/assets/images/c++/studying/cpp_studying_2.png)

위와 같은 관계인데,

main 함수 내부를 잘 살펴보면,

동적 할당의 형태로 First 객체를 하나 생성시키고,

SimpleFunc() 이라는 함수를 호출 및 객체를 소멸시키는 것을 확인할 수 있다.

또한 First형에 Second 객체를 생성시키고 있는데,

이는 First가 기초(기반, Base) 클래스이므로 가능한 연산이다.

그리고 이것 역시 SimpleFunc() 이라는 함수를 호출 및 객체 소멸을 진행하고 있다.

만약에 virtual로 함수를 선언하지 않았다면,

First형으로 선언된 포인터 변수에 First 객체를 담든, Second 객체를 담든 (상속 관계에 놓여있는 기초 클래스 외에 어떤 유도(파생, Derived) 클래스의 객체를 담더라도) First 클래스 내부에 있는 SimpleFunc() 함수만 호출될 것이다.

그런데 virtual 선언을 해줌으로써 First형의 포인터 변수에 Second 객체를 담게 되면 Second 클래스 내부에 있는 동일한 이름의 SimpleFunc 함수가 호출이 된다.

이것이 바로 C++에서의 **'다형성'**의 예시이다.


