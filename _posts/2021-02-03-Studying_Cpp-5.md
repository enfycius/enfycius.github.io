---
title: "C++ 상속과 생성자의 호출"

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

다음 클래스에 적절한 생성자를 삽입해보자.

그리고 이의 확인을 위한 main 함수를 적절히 정의해 보자.

```cpp
#include <iostream>
 
using namespace std;
 
class Car
{
private:
    int gasolineGauge;
 
public:
    int GetGasGauge()
    {
        return gasolineGauge;
    }
};
 
class HybridCar : public Car
{
private:
    int electricGauge;
 
public:
    int GetElecGauge()
    {
        return electricGauge;
    }
};
 
class HybridWaterCar : public HybridCar
{
private:
    int waterGauge;
 
public:
    void ShowCurrentGauge()
    {
        cout<<"잔여 가솔린: "<<GetGasGauge()<<endl;
        cout<<"잔여 전기량: "<<GetElecGauge()<<endl;
        cout<<"잔여 워터량: "<<waterGauge<<endl;
    }
};
```

# 해결

## 코드

```cpp
#include <iostream>
 
using namespace std;
 
class Car
{
private:
    int gasolineGauge;
 
public:
    Car(int gasoline) : gasolineGauge(gasoline) {}
    int GetGasGauge()
    {
        return gasolineGauge;
    }
};
 
class HybridCar : public Car
{
private:
    int electricGauge;
 
public:
    HybridCar(int elec, int gasoline) : Car(gasoline), electricGauge(elec) {}
 
    int GetElecGauge()
    {
        return electricGauge;
    }
};
 
class HybridWaterCar : public HybridCar
{
private:
    int waterGauge;
 
public:
    HybridWaterCar(int gasoline, int elec, int water) : HybridCar(elec, gasoline), waterGauge(water) {}
 
    void ShowCurrentGauge()
    {
        cout<<"잔여 가솔린: "<<GetGasGauge()<<endl;
        cout<<"잔여 전기량: "<<GetElecGauge()<<endl;
        cout<<"잔여 워터량: "<<waterGauge<<endl;
    }
};
 
int main(void)
{
    HybridWaterCar ts(100, 100, 100);
 
    ts.ShowCurrentGauge();
 
    return 0;
}
```