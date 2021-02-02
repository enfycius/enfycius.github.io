---
title: "C++ 상속 관계의 확장과 추상 클래스"

classes: wide

categories:
  - C++
tags:
  - C++
  - Programming
  - Coding
---

# 문제 

예제 EmployeeManager4.cpp를 확장하여 다음 특성에 해당하는 ForeignSalesWorker 클래스를 추가로 정의해보자.

"영업직 직원 중 일부는 오지산간으로 시장개척을 진행하고 있다. 일부는 아마존에서, 또 일부는 테러의 위험이 있는 지역에서 영업활동을 진행 중에 있다. 따라서 이러한 직원들을 대상으로 별도의 위험수당을 지급하고자 한다."

위험수당의 지급방식은 '위험의 노출도' 에 따라서 다음과 같이 나뉘며, 한번 결정된 직원의 '위험 노출도' 는 변경되지 않는다고 가정한다(이는 const 멤버변수의 선언을 유도하는 것이다).

* 리스크 A: 영업직의 기본급여와 인센티브 합계 총액의 30%를 추가로 지급한다.
* 리스크 B: 영업직의 기본급여와 인센티브 합계 총액의 20%를 추가로 지급한다.
* 리스크 C: 영업직의 기본급여와 인센티브 합계 총액의 10%를 추가로 지급한다.

다음 main 함수와 함께 동작하도록 ForeignSalesWorker 클래스를 정의하기 바라며, Employee 클래스는 객체 생성이 불가능한 추상 클래스로 정의하기 바란다.

## main 함수

```cpp
int main(void)
{
    EmployeeHandler handler;

    ForeignSalesWorker* fseller1 = new ForeignSalesWorker("Hong", 1000, 0.1, RISK_LEVEL::RISK_A);

    fseller1 -> AddSalesResult(7000);

    handler.AddEmployee(fseller1);

    ForeignSalesWorker* fseller2 = new ForeignSalesWorker("Yoon", 1000, 0.1, RISK_LEVEL::RISK_B);

    fseller2->AddSalesResult(7000);

    handler.AddEmployee(fseller2);

    ForeignSalesWorker* fseller3 = new ForeignSalesWorker("Lee", 1000, 0.1, RISK_LEVEL::RISK_C);

    fseller3->AddSalesResult(7000);

    handler.AddEmployee(fseller3);
    handler.ShowAllSalaryInfo();

    return 0;
}
```

위의 main 함수에서 보이는 RISK_LEVEL 이름공간의 RISK_A, RISK_B, RISK_C는 enum형으로 선언된 상수이다. 그럼 이어서 실행결과를 보이겠다.

## 실행의 예

위의 실행결과에서 salary 내역은 일반 영업직 직원의 급여 계산결과이며(기본금에 상여금을 더한 결과), risk pay가 위험수당에 속한다.

### EmployeeManager4.cpp 코드

```cpp
#include <iostream>
#include <cstring>

using namespace std;

class Employee
{
private:
    char name[100];

public:
    Employee(char* name)
    {
        strcpy(this->name, name);
    }

    void ShowYourName() const
    {
        cout<<"name: "<<name<<endl;
    }

    virtual int GetPay() const
    {
        return 0;
    }

    virtual void ShowSalaryInfo() const {}
};

class TemporaryWorker : public Employee
{
private:
    int workTime;
    int payPerHour;

public:
    TemporaryWorker(char* name, int pay) : Employee(name), workTime(0), payPerHour(pay) {}

    void AddWorkTime(int time)
    {
        workTime += time;
    }

    int GetPay() const
    {
        return workTime*payPerHour;
    }

    void ShowSalaryInfo() const
    {
        ShowYourName();
        cout<<"salary: "<<GetPay()<<endl<<endl;
    }
};

class PermanentWorker: public Employee
{
private:
    int salary;

public:
    PermanentWorker(char* name, int money) : Employee(name), salary(money)
    {}

    int GetPay() const
    {
        return salary;
    }

    void ShowSalaryInfo() const
    {
        ShowYourName();
        cout<<"salary: "<<GetPay()<<endl<<endl;
    }
};

class SalesWorker: public PermanentWorker
{
private:
    int salesResult;
    double bonusRatio;

public:
    SalesWorker(char* name, int money, double ratio) : PermanentWorker(name, money), salesResult(0), bonusRatio(ratio) {}

    void AddSalesResult(int value)
    {
        salesResult += value;
    }

    int GetPay() const
    {
        return PermanentWorker::GetPay() + (int)(salesResult*bonusRatio);
    }

    void ShowSalaryInfo() const
    {
        ShowYourName();
        cout<<"salary: "<<GetPay()<<endl<<endl;
    }
};

class EmployeeHandler
{
private:
    Employee* empList[50];
    int empNum;

public:
    EmployeeHandler() : empNum(0)
    {}

    void AddEmployee(Employee* emp)
    {
        empList[empNum++]=emp;
    }

    void ShowAllSalaryInfo() const
    {
        for(int i=0; i<empNum; i++)
            empList[i]->ShowSalaryInfo();
    }

    void ShowTotalSalary() const
    {
        int sum=0;

        for(int i=0; i<empNum; i++)
            sum += empList[i]->GetPay();

        cout<<"salary sum: "<<sum<<endl;
    }

    ~EmployeeHandler()
    {
        for(int i=0; i<empNum; i++)
            delete empList[i];
    }
};

int main(void)
{
    EmployeeHandler handler;

    handler.AddEmployee(new PermanentWorker("KIM", 1000));
    handler.AddEmployee(new PermanentWorker("LEE", 1500));

    TemporaryWorker * alba = new TemporaryWorker("Jung", 700);

    alba->AddWorkTime(5);

    handler.AddEmployee(alba);

    SalesWorker * seller = new SalesWorker("Hong", 1000, 0.1);

    seller->AddSalesResult(7000);

    handler.AddEmployee(seller);
    handler.ShowAllSalaryInfo();
    handler.ShowTotalSalary();

    return 0;
}
```

### 풀이 코드

```cpp
#include <iostream>
#include <cstring>

using namespace std;

namespace RISK_LEVEL
{
    enum
    {
        RISK_A,
        RISK_B,
        RISK_C
    };
}

class Employee
{
private:
    char name[100];

public:
    Employee(char* name)
    {
        strcpy(this->name, name);
    }

    void ShowYourName() const
    {
        cout<<"name: "<<name<<endl;
    }

    virtual int GetPay() const = 0;
    virtual void ShowSalaryInfo() const = 0;
};

class TemporaryWorker : public Employee
{
private:
    int workTime;
    int payPerHour;

public:
    TemporaryWorker(char* name, int pay) : Employee(name), workTime(0), payPerHour(pay) {}

    void AddWorkTime(int time)
    {
        workTime += time;
    }

    int GetPay() const
    {
        return workTime*payPerHour;
    }

    void ShowSalaryInfo() const
    {
        ShowYourName();
        cout<<"salary: "<<GetPay()<<endl<<endl;
    }
};

class PermanentWorker: public Employee
{
private:
    int salary;

public:
    PermanentWorker(char* name, int money) : Employee(name), salary(money) {}

    int GetPay() const
    {
        return salary;
    }

    void ShowSalaryInfo() const
    {
        ShowYourName();
        cout<<"salary: "<<GetPay()<<endl<<endl;
    }
};

class SalesWorker: public PermanentWorker
{
private:
    int salesResult;
    double bonusRatio;

public:
    SalesWorker(char* name, int money, double ratio) : PermanentWorker(name, money), salesResult(0), bonusRatio(ratio) {}

    void AddSalesResult(int value)
    {
        salesResult += value;
    }

    int GetPay() const
    {
        return PermanentWorker::GetPay() + (int)(salesResult*bonusRatio);
    }

    void ShowSalaryInfo() const
    {
        ShowYourName();
        cout<<"salary: "<<GetPay()<<endl<<endl;
    }
};

class ForeignSalesWorker: public SalesWorker
{
private:
    const int risk;

public:
    ForeignSalesWorker(char* name, int money, double ratio, int risk) : SalesWorker(name, money, ratio), risk(risk) {}

    int GetPay() const
    {
        switch(risk)
        {
            case 0:
                return SalesWorker::GetPay() * 0.3;
                break;

            case 1:
                return SalesWorker::GetPay() * 0.2;
                break;
                
            case 2:
                return SalesWorker::GetPay() * 0.1;
                break;

            default:
                return 0;
        }
    }

    void ShowSalaryInfo() const
    {
        ShowYourName();

        cout<<"salary: "<<SalesWorker::GetPay()<<endl;
        cout<<"risk pay: "<<GetPay()<<endl;
        cout<<"sum: "<<SalesWorker::GetPay()+GetPay()<<endl<<endl;
    }                                
};

class EmployeeHandler
{
private:
    Employee* empList[50];
    int empNum;

public:
    EmployeeHandler() : empNum(0) {}

    void AddEmployee(Employee* emp)
    {
        empList[empNum++]=emp;
    }

    void ShowAllSalaryInfo() const
    {
        for(int i=0; i<empNum; i++)
            empList[i]->ShowSalaryInfo();
    }

    void ShowTotalSalary() const
    {
        int sum=0;

        for(int i=0; i<empNum; i++)
            sum += empList[i]->GetPay();

        cout<<"salary sum: "<<sum<<endl;
    }

    ~EmployeeHandler()
    {
        for(int i=0; i<empNum; i++)
            delete empList[i];
    }
};

int main(void)
{
    EmployeeHandler handler;

    ForeignSalesWorker* fseller1 = new ForeignSalesWorker("Hong", 1000, 0.1, RISK_LEVEL::RISK_A);

    fseller1 -> AddSalesResult(7000);

    handler.AddEmployee(fseller1);

    ForeignSalesWorker* fseller2 = new ForeignSalesWorker("Yoon", 1000, 0.1, RISK_LEVEL::RISK_B);

    fseller2->AddSalesResult(7000);

    handler.AddEmployee(fseller2);

    ForeignSalesWorker* fseller3 = new ForeignSalesWorker("Lee", 1000, 0.1, RISK_LEVEL::RISK_C);

    fseller3->AddSalesResult(7000);

    handler.AddEmployee(fseller3);
    handler.ShowAllSalaryInfo();

    return 0;
}
```