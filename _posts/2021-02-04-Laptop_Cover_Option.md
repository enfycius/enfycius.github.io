---
title: "노트북 덮개 설정 - Ubuntu"

classes: wide

categories:
  - Linux
tags:
  - Linux
  - Ubuntu
  - Apache
  - Server
  - Tomcat
---

# 내용

이번 포스팅에서는 노트북 덮개를 덮은 상태에서 노트북을 사용할 수 있는 방법에 대해 알아보고자 한다.

먼저 우분투에서 터미널 실행 후 다음 명령어를 입력하자.

```shell
sudo vi /etc/systemd/logind.conf
```

i를 눌러 입력 모드(Insert mode)로 전환 후,

아래의 기본 설정을

```shell
#HandleLidSwitch=suspend
```

다음과 같이 변경한다.

```shell
#HandleLidSwitch=ignore
```

:wq 입력 후 엔터를 눌러 변경한 설정을 저장한 후, 우분투를 재부팅해주면 된다.