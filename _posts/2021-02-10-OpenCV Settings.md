---
title: "OpenCV Installing & Settings for Mac"

classes: wide

categories:
  - OpenCV
tags:
  - OpenCV
  - Settings
  - Programming
  - Coding

toc: true
---

# 내용

Mac에서 OpenCV 설치와 Xcode 설정법을 찾아보던 중 이에 대해 정리가 잘 되어있는 블로그를 발견하였다.
(아래 링크 참고)

[바로 가기](https://dgrld.tistory.com/34 "Xcode OpenCV Install & Settings")

다만 설정을 다루는 내용에서 몇 가지 아쉬운 점이 있어 이번 포스팅에서는 그에 대한 보충을 해보고자 한다.

##  링커 플래그(Linker Flag) 추출할 때

위 블로그 포스팅에서는 링커 플래그(Linker Flag)를 추출하기 위해 다음의 명령어를 입력하였는데,

```shell
pkg-config --cflags --libs opencv
```

그러면 다음과 같은 에러 메시지가 뜬다.

![OpenCV-Settings](/assets/images/opencv/studying/opencv-settings-1.png "OpenCV-Settings")

그러므로 명령어를 다음으로 변경하여 입력하자.

```shell
pkg-config --cflags --libs opencv4
```

그러면 다음처럼 정상적으로 링커 플래그(Linker Flag)가 추출되는 것을 확인할 수 있다.

![OpenCV-Settings](/assets/images/opencv/studying/opencv-settings-2.png "OpenCV-Settings")

## Xcode Header Search Paths 설정할 때

또한 위 블로그 포스팅에서는 다음의 경로만 추가해주었다.

```shell
/usr/local/include
```

이렇게 할 경우 헤더파일 선언문을 다음과 같이 작성해주어야 하는데,

```cpp
#include <opencv4/opencv2/opencv.hpp>
```

이것 역시 컴파일 시 관련된 파일들을 찾을 수 없다는 에러(Not Found)로 이어지므로 다음 경로도 추가로 입력해주자.

```shell
/usr/local/include/opencv4
```

여기까지 하면 정상적으로 컴파일 되는 것을 확인할 수 있다.





