---
title: "C++ & Assembly : Settings for Visual Studio 2017"

classes: wide

categories:
  - Cpp
  - Assembly
tags:
  - Programming
  - Tool

toc: true
---

# 내용

Dropper Lab 연구 활동 중 개인적으로 Visual Studio 2017에서 C++ 내에 Assembly 코드를 작성하는 방식(inline) 대신, 외부 참조 방식으로 코드를 작성할 일이 생겨, 이번 포스팅에서는 이와 관련하여 몇 가지 설정법에 대해 알아보고자 한다.

## 프로젝트 생성

먼저 프로젝트를 생성하자.

프로젝트 Type은 Console Application이다.

![Creating](/assets/images/assembly/studying/assembly-settings-1.png)

## 프로젝트 설정

### 사용자 지정 빌드

일단 솔루션 탐색기에서 프로젝트를 선택한 상태로, 메뉴에서 **프로젝트 > 사용자 지정 빌드**를 선택하자.

![Settings](/assets/images/assembly/studying/assembly-settings-2.png)

다음과 같이 나오는 창에서 **masm**을 체크하고 확인을 누르자.

![Settings](/assets/images/assembly/studying/assembly-settings-3.png)

### 구성 관리자

메뉴에서 **빌드 > 구성 관리자**를 선택하자.

그 후 다음의 노출되는 창에서

![Settings](/assets/images/assembly/studying/assembly-settings-4.png)

**활성 솔루션 플랫폼** 아래의 x86이 적혀있는 콤보박스를 내려서 **x64**로 변경하자.

![Settings](/assets/images/assembly/studying/assembly-settings-5.png)

## 어셈블리 파일 생성 및 설정

### 어셈블리 파일 생성

이제 어셈블리 파일을 생성할 차례이다.

솔루션 탐색기의 프로젝트 아래에 있는 소스 파일 directory에 오른쪽 마우스를 눌러서 나오는 드롭다운 메뉴에서 **추가 > 새 항목**을 누르자.

![Creating](/assets/images/assembly/studying/assembly-settings-6.png)

파일의 Type은 **C++ 파일(.cpp)**을 선택하고, 아래의 이름 적는 란에는 파일의 확장자를 기존 .cpp에서 .asm으로 변경하자.

(참고로 기존 .cpp 파일과 동일 이름으로 파일명을 작성하진 말자.)

![Creating](/assets/images/assembly/studying/assembly-settings-7.png)

그리고 추가 버튼을 눌러주면 된다.

### 어셈블리 파일 설정

솔루션 탐색기 아래의 소스 파일 directory 내부에 생성된 .asm 파일을 선택한 후, 노출되는 드롭다운 메뉴에서 **속성**을 누르자.

![Settings](/assets/images/assembly/studying/assembly-settings-8.png)

노출되는 창에서 항목 형식이 **Microsoft Macro Assembler**인지 확인하자.

(만약 이것이 아니라면, 드롭다운 메뉴를 내려서 이것으로 설정해주자.)

![Settings](/assets/images/assembly/studying/assembly-settings-9.png)

설정이 되었다면, 왼쪽에 Microsoft Macro Assembler를 내려보면 **Command Line**이라는 항목이 존재하는 데 이를 눌러보자.

모든 옵션 아래에 있는 내용이 ml64.exe로 시작하는지 확인하자.

![Settings](/assets/images/assembly/studying/assembly-settings-10.png)

여기까지 완료했다면, 확인 버튼을 누르자.

## 코드 작성

단순히 동작 여부만을 확인하기 위해서 두 개의 정수 값을 인자로 받아서 이것의 덧셈을 반환하는 함수(IntegerAdd)를 어셈블리로 작성해보자.

필자는 .cpp 파일명을 main으로 .asm 파일명을 main2로 작성했다.

### main.cpp

```cpp
#include <iostream>

using namespace std;

extern "C" int IntegerAdd(int a, int b);

int main() {
    int result = IntegerAdd(3, 5);

    cout<<result<<endl;

    return 0;
}
```

### main2.asm

```nasm
.code
IntegerAdd proc

mov eax, ecx
add eax, edx

ret

IntegerAdd endp
end
```

아래에 실행 결과를 보이면서 이번 포스팅을 마무리 짓겠다.

### 실행 결과

![Result](/assets/images/assembly/studying/assembly-settings-11.png)





















# Reference

[Reference](https://stackoverflow.com/questions/33751509/external-assembly-file-in-visual-studio)