---
title: "C++ mutable 키워드, 그리고 그 외의 이야기들"

classes: wide

categories:
  - C++
tags:
  - C++
  - Programming
  - Coding

toc: true
---

# 내용

Keyword mutable은 const 함수 내에서의 값의 변경을 예외적으로 허용해준다.

## 예제

### 코드

```cpp
#include <iostream>
 
using namespace std;
 
class SoSimple
{
    private:
    int num1;
    mutable int num2;
 
    public:
    SoSimple(int n1, int n2) : num1(n1), num2(n2)
    {}
 
    void ShowSimpleData() const
    {
        cout<<num1<<", "<<num2<<endl;
    }
 
    void CopyToNum2() const
    {
        num2 = num1;
    }
};
 
int main(void)
{
    SoSimple sm(1, 2);
    sm.ShowSimpleData();
    sm.CopyToNum2();
    sm.ShowSimpleData();
 
    return 0;
}
```

## 설명

9행을 보면 num2라는 변수 선언 앞에 mutable이라는 keyword가 붙은것을 볼 수 있다.

```cpp
mutable int num2;
```

이 keyword가 붙는 순간 const로 선언된 함수 내부에서 num2의 값을 변경시키는 것이 가능해진다.

그러므로 20행에 정의된 CopyToNum2 이라는 const로 정의된 함수 내부에서 num2의 값을 num1의 값으로 변경시키는 것을 볼 수 있다.
(그리고 이러한 변경은 컴파일러가 허용한다.)

```cpp
void CopyToNum2() const
{
        num2 = num1;
}
```

특히, C에서 전역변수를 많이 사용하게 될 경우 스파게티 코드가 되듯이, C++에서도 전역변수 외에 mutable keyword 과다 사용 시 스파게티 코드가 되므로 이것 역시 조심히 사용해야 한다.
