---
title: "C++ Early Binding(Static Binding) & Late Binding(Dynamic Binding)"

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

이번 포스팅에서는 Early Binding(Static Binding)과 Late Binding(Dynamic Binding)에 대해서 알아보고자 한다.

바인딩(Binding)이 생소할 수 있으니 먼저 이에 대해서 알아보자.

## 바인딩(Binding)

위키피디아에서는 바인딩을 다음과 같이 설명하고 있다.

프로그래밍 언어에서, 네임 바인딩(name binding)은 엔티티들(데이터 그리고/또는 코드)과 식별자들의 연관이다. 객체에 바운드되는 식별자는 객체를 참조한다고 불린다.  기계어는 식별자의 빌트인 개념을 갖진 않지만, 서비스로서 그리고 프로그래머를 위한 표기로서 네임-객체 바인딩을 가지며 이것은 프로그래밍 언어들에 의해서 구현된다. 바인딩은 스코핑(변수 영억)과 밀접하게 연결되는데, 스코핑은 어떤 네임들을 어떤 객체들에 바인드할 지를 결정한다 - 프로그램 코드의 어느 위치에서 그리고 가능한 실행 경로들 중 어느 곳에서. id를 위한 바인딩을 확립하는 문맥에서 식별자 id의 사용은 바인딩 발생이라고 불린다. 모든 다른 발생들(예를 들면 표현식들, 할당들 그리고 서브프로그램 호출들에서)에서 식별자는 무엇이 바운드되었는지를 나타낸다. 이러한 발생들은 적용된 발생이라고 불린다.

위의 정의만 읽고나서는 도통 무슨 말인지 이해할 수 없을 듯 하여 이에 대해 최대한 쉽게, 간략하게 설명을 해보고자 한다.

일반적으로 바인딩이란 하나의 것을 다른 것에(으로) 대입(대치)하는 것인데, 예를 들어 변수들에 값을 대입하는 것도 바인딩에 해당하고,

식별자들(예를 들면, 변수나 함수의 이름들)을 주소들로 변환하는 과정도 바인딩에 해당한다.

그리고 이러한 바인딩은 컴파일 시(at compile time)에 발생하는 바인딩과 런타임 시(at runtime)에 발생하는 바인딩으로 나눌 수 있다.

### Early Binding(Static Binding)

컴파일 시(at compile time)에 발생하는 바인딩을 가리켜 Early Binding(Static Binding)이라 한다.

이는 컴파일러(compiler)나 링커(linker)에 의해 직접적으로 주소와 함수 호출간에 연관 관계가 만들어지며,

함수 호출은 기계어 지시문들로 대체된다.

또한, C++에서 기본적으로 발생하는 바인딩은 Early Binding(Static Binding)이다.

코드와 실행결과를 보자.

#### Code

```cpp
#include <iostream>

using namespace std;

class Animal {
    public:
        void Eat() { cout<<"동물이 밥을 먹는다."<<endl; }
};

class Lion: public Animal {
    public:
        void Eat() { cout<<"사자가 밥을 먹는다."<<endl; }
};

int main(void) {
    Animal* ani = new Lion;

    ani->Eat();

    return 0;
}
```

#### Output

```shell
동물이 밥을 먹는다.
```

직관적으로 생각해보았을 때, 하위 클래스에 대한 객체를 생성한 후 해당 인스턴스를 상위 클래스 포인터 자료형에 대입하였으니 당연히 Eat()을 호출하였을 때, 하위 클래스의 Eat()이 실행될 것 같지만, 사실 상위 클래스인 Animal 내의 Eat()이 호출된다.

이는 Early Binding(Static Binding)의 경우에 컴파일러는 **포인터의 자료형**을 보기 때문에

Eat()을 호출하였을 때 해당 자료형 즉, 상위 클래스인 Animal 내의 Eat()이 호출되는 것이다.

그렇다면 필자의 직관적인 생각에 부합한 결과가 도출되기 위해서는 어떻게 해야할까?

아래에서 Late Binding(Dynamic Binding)에 대해 알아보자.

### Late Binding(Dynamic Binding)

Late Binding(Dynamic Binding)은 Early Binding(Static Binding)과는 달리 런타임 시(at runtime)에 발생하는 바인딩을 말한다.

이는 컴파일러가 런타임 시 객체의 자료형을 식별하는 코드를 추가한 후, 올바른 함수 정의와 그것의 호출을 일치시킨다.

이러한 Late Binding(Dynamic Binding)은 C++에서 **virtual keyword**에 의해 구현될 수 있다.

아래에서 코드와 실행결과를 살펴보자.

#### Code

```cpp
#include <iostream>

using namespace std;

class Animal {
    public:
        virtual void Eat() { cout<<"동물이 밥을 먹는다."<<endl; }
};

class Lion: public Animal {
    public:
        void Eat() { cout<<"사자가 밥을 먹는다."<<endl; }
};

int main(void) {
    Animal* ani = new Lion;

    ani->Eat();

    return 0;
}
```

#### Output

```shell
사자가 밥을 먹는다.
```

위의 실행결과는 필자의 직관적인 생각과 부합하는 결과임을 확인할 수 있다.

이렇듯 C++에서 Late Binding(Dynamic Binding)을 구현하기 위해 **virtual keyword** 붙이는 것을 잊지 말자.

또한, 아직 Early Binding(Static Binding)과 Late Binding(Dynamic Binding)에 대해 이해되지 않을 수 있다.

그래서 필자가 위 예제와 관련하여 여러분의 이해를 돕고자 다음의 필자의 생각을 준비해보았다.

> Early Binding(Static Binding)의 경우에는 컴파일러가 포인터의 자료형에 집중한다면, Late Binding(Dynamic Binding)의 경우에는 컴파일러가 포인터의 자료형이 아닌 그것이 가지고 있는 값에 집중한다.

이는 절대적인 진리는 아니며, 위의 예제와 같이 상속 관계에 놓여있는 클래스에 대해서 활용할 수 있는 생각임을 밝혀둔다.

# 참고문헌

[Wikipedia](https://ko.wikipedia.org/wiki/%EB%84%A4%EC%9E%84_%EB%B0%94%EC%9D%B8%EB%94%A9)

