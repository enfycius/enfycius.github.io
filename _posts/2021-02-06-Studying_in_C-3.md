---
title: "C/C++ main 함수의 크기"

classes: wide

categories:
  - C
  - C++
tags:
  - C
  - C++
  - Programming
  - Coding

toc: true
---

# 내용

이번 포스팅에서는 의미가 있을까 싶지만, 한번쯤 궁금해 할 것 같은 내용을 다뤄보고자 한다.

바로 **"main 함수의 크기"**이다.

main 함수의 크기는 얼마일까?

## 코드(C)

```c
#include <stdio.h>

int main(void) {

    printf("%lu\n", sizeof(main()));

    return 0;
}
```

## 실행결과

![C](/assets/images/c/studying/c_studying_1.png)

C에서는 4Byte,

## 코드(C++)

```cpp
#include <iostream>

using namespace std;

int main(void) {

    cout<<sizeof(main())<<endl;

    return 0;
}
```

## 실행결과

![C++](/assets/images/c++/studying/cpp_studying_3.png)

C++에서도 4Byte이다.


