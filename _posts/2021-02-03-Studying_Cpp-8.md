---
title: "C++ 함수 템플릿의 정의, 두 번째"

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

다음은 int형 배열에 저장된 값을 모두 더해서 그 결과를 반환하는 기능의 함수이다.

```cpp
int SumArray(int arr[], int len)
{
    int sum=0;

    for(int i=0; i<len; i++)
        sum+=arr[i];

    return sum;
}
```

이 함수를 템플릿으로 정의하여, 다양한 자료형의 배열을 대상으로 합을 계산하는 예제를 작성해보자.

# 해결

## 코드

```cpp
#include <iostream>
 
using namespace std;
 
template <typename T>
 
T SumArray(T arr[], int len)
{
    T sum = 0;
 
    for (int i = 0; i < len; i++)
        sum += arr[i];
 
    return sum;
}
 
int main(void)
{
    int arr[5] = { 1, 2, 3, 4, 5 };
    double arr2[5] = { 1.1, 2.2, 3.3, 4.4, 5.5 };
 
    cout<<"int Value: "<<SumArray(arr, 5)<<endl;
    cout << "double Value: " << SumArray(arr2, 5) << endl;
 
    return 0;
}
```