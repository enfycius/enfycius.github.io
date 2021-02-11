---
title: "Reversing: String Patching"

classes: wide

categories:
  - Reversing
tags:
  - Reversing
  - Programming
  - Coding

toc: true
---

# Contents

## Prerequisite

이번 포스팅에서는 Radare2를 이용하여 String Patching을 진행해보고자 한다.

이를 위해 필자는 Linux x64 System에서 x64 Executable File을 Target으로 삼았으며,

또한, Example Code로서 이전에 업로드한 포스팅의 예제를 활용하였다.

[참고](https://enfycius.github.io/c++/Assign-Cpp-1/)

독자 여러분들은 필자와 동일한 환경을 구성하진 않더라도 비슷한 환경을 구성해주길 바란다.

## Purpose

필자는 Compiled Example Code로부터 다음의 기존 출력결과를

```shell
1. student
2. salesman
3. housewife
select:
```

다음과 같이 변경하려 한다.

```shell
1. test
2. salesman
3. housewife
select:
```

## String Patching

먼저 터미널을 실행한다.

![terminal-01](/assets/images/reversing/studying/reversing-01-01.png)

Example Code가 있는 곳으로 이동하여,

![terminal-02](/assets/images/reversing/studying/reversing-01-02.png)

해당 파일을 컴파일하자.
(필자는 Example Code의 Filename을 virtual1.cpp로 작성하였다.)

![terminal-03](/assets/images/reversing/studying/reversing-01-03.png)

수정하기 전 실행 결과는 다음과 같다.

![terminal-04](/assets/images/reversing/studying/reversing-01-04.png)

Radare2를 본격적으로 사용해보자.

```shell
radare2 main
```
![terminal-05](/assets/images/reversing/studying/reversing-01-05.png)

문자열 student이 있는 메모리 상의 위치를 검색해보자.

```shell
/ student
```

![terminal-06](/assets/images/reversing/studying/reversing-01-06.png)

다음과 같이 메모리 주소 0x00002033가 도출되었으므로, 

![terminal-07](/assets/images/reversing/studying/reversing-01-07.png)

해당 메모리 주소로 커서를 이동시키자.

```shell
s 0x00002033
```

![terminal-08](/assets/images/reversing/studying/reversing-01-08.png)

해당 메모리 주소가 우리가 변경하기를 원하는 문자열이 있는 위치인지를 명확히 하기 위해 다음의 명령어를 입력하여 이를 확인해보자.

```shell
px
```

![terminal-09](/assets/images/reversing/studying/reversing-01-09.png)

문자열 student가 있는 위치로 커서가 이동했음을 확인할 수 있다.

이제 해당 내용을 변경하기 위해 읽기-쓰기 모드로 전환하자.

```shell
oo+
```

![terminal-10](/assets/images/reversing/studying/reversing-01-10.png)

이제 진짜 문자열을 변경해보자.

필자는 위에서 student를 test로 변경한다하였으므로 다음과 같이 입력해주었다.

```shell
w test\x00
```

![terminal-11](/assets/images/reversing/studying/reversing-01-11.png)


> C/C++에서는 문자열의 끝을 NULL 문자로 인식하므로 \x00 삽입을 잊어서는 안된다.

마지막으로 Radare2를 종료한 후,

```shell
q
```

컴파일한 파일을 다시 실행시켜보자.

```shell
./main
```

![terminal-12](/assets/images/reversing/studying/reversing-01-12.png)

기존 문자열 student가 test로 변경된 것을 확인할 수 있다.




