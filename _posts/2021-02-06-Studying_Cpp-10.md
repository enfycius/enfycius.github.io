---
title: "C++ Pointer, Reference 사용 시 주의할 점(Information Hiding)"

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

이번 포스팅에서는 C++에서 정보 은닉(Information Hiding)과 관련하여 Pointer, Reference Variable & Return Type 사용 시 주의해야 할 점에 대해서 알아보고자 한다.

먼저 아래의 코드를 보자.

## 코드

```cpp
#include <iostream>

using namespace std;

class Square {
private:
    double width;
    double height;

public:
    Square(double _width = 1.0, double _height = 1.0) {
        this->width = _width;
        this->height = _height;
    }

    double GetWidth() {
        return width;
    }

    double GetHeight() {
        return height;
    }

    void SetWidth(double _width) {
        this->width = _width;
    }

    void SetHeight(double _height) {
        this->height = _height;
    }

    double Area() {
        return this->width * this->height;
    }
};

int main(void) {
    
    Square obj(2.5);

    cout<<obj.Area();

    return 0;
}
```

위 코드는 **코드상** **정보 은닉의 원칙(Principle)**이 잘 반영된 코드이다. 

그런데 필자는 여기에 약간의 변형을 가해보려 한다.

다음의 코드는 어떠한가?

```cpp
#include <iostream>

using namespace std;

class Square {
private:
    double width;
    double height;

public:
    Square(double _width = 1.0, double _height = 1.0) {
        this->width = _width;
        this->height = _height;
    }

    double& GetWidth() {
        return width;
    }

    double& GetHeight() {
        return height;
    }

    void SetWidth(double _width) {
        this->width = _width;
    }

    void SetHeight(double _height) {
        this->height = _height;
    }

    double Area() {
        return this->width * this->height;
    }
};

int main(void) {
    Square obj(2.5);
    double& _height = obj.GetHeight();
    double& _width = obj.GetWidth();

    _height = 20.5;
    _width = 34.1;

    cout<<obj.Area();

    return 0;
}
```

> 위 코드는 **코드상** 정보은닉의 원칙(Principle)이 잘 반영된 코드라고 말할 수 있겠는가?

절대 아니다.

함수의 반환형이 참조형이므로 이를 받아 private 처리된 데이터를 수정할 수 있는 가능성이 존재하기 때문이다.

이는 정보은닉의 원칙(Principle)을 깨뜨리는(Break) 또는 타협하는(Compromising) 가능성(Possibility)을 지니고 있다. 

그럼 다음의 코드는 어떠한가?

```cpp
#include <iostream>

using namespace std;

class Square {
private:
    double width;
    double height;

public:
    Square(double _width = 1.0, double _height = 1.0) {
        this->width = _width;
        this->height = _height;
    }

    double* GetWidth() {
        return &width;
    }

    double* GetHeight() {
        return &height;
    }

    void SetWidth(double _width) {
        this->width = _width;
    }

    void SetHeight(double _height) {
        this->height = _height;
    }

    double Area() {
        return this->width * this->height;
    }
};

int main(void) {
    Square obj(2.5);
    double* _height = obj.GetHeight();
    double* _width = obj.GetWidth();

    *_height = 20.5;
    *_width = 34.1;

    cout<<obj.Area();

    return 0;
}
```

이 역시도 동일한 문제점을 내포하고 있다.

아마 눈치챈 독자도 있겠지만, 필자는 **"코드상"**이라는 말에 굵은 글씨로 강조 표시를 해놓았다.

다음 코드를 보자.

```cpp
#include <iostream>

using namespace std;

class Square {
private:
    double width;
    double height;

public:
    Square(double _width = 1.0, double _height = 1.0) {
        this->width = _width;
        this->height = _height;
    }

    double GetWidth() {
        return width;
    }

    double GetHeight() {
        return height;
    }

    void SetWidth(double _width) {
        this->width = _width;
    }

    void SetHeight(double _height) {
        this->height = _height;
    }

    double Area() {
        return this->width * this->height;
    }
};

int main(void) {
    
    Square obj(2.5);

    double* test = (double*)&obj;

    *test = 3.4;

    *(++test) = 4.5;

    cout<<obj.Area();

    return 0;
}
```

사실 이렇듯 **코드상** **정보 은닉의 원칙(Principle)**이 잘 지켜졌다고 하더라도 위의 경우에서처럼 private 데이터를 수정할 수 있다.

그렇다면 이것이 C++에서 캡슐화(Encapsulation)가 작동하지 않는다는 것을 의미하는 것일까?

아니다. **캡슐화를 통한 정보 은닉이 필요한 이유**를 생각해보자.

캡슐화를 통한 정보 은닉의 목적은 프로그래머에 의해 우발적으로(Accidentally) 발생할 수 있는 데이터의 손실이나 변경을 막기 위함이다.

즉, 위의 포인터 연산은 단순히 우발적으로(Accidentally) 일어난 일인가?

아니다. 이는 프로그래머가 의도적으로(Intentionally) 작성한 코드이다.

그러므로 캡슐화(Encapsulation)가 C++에서 작동하지 않는다는 말은 잘못된 주장이다.

하지만 위의 경우에서처럼 포인터를 이용하여 의도적으로(Intentionally) private 멤버에 접근하는 것은 권고 사항도 아닐 뿐더러 절대 사용하지 말아야 한다.

결론적으로 참조 변수와 포인터 변수 사용 시, 항상 신중하게 주의를 기울여 사용해야 함을 명심하자.
