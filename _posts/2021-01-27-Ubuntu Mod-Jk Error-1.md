---
title: "Ubuntu mod_jk Error"

classes: wide

categories:
  - Linux
tags:
  - Linux
  - Ubuntu
  - Apache
  - Server
  - Tomcat

toc: true
---

# Ubuntu mod_jk Error

Tomcat과 Apache를 연결시켜주는 다리 역할을 하는 mod_jk에서 계속된 오류가 발생하여,

결국 포기하고 Tomcat만을 돌리다가 주소에서 :8080을 떼어내고 싶어 /var/log/apache2/mod_jk.log 파일을 분석하던 중 다음의 에러를 발견할 수 있었다.

![mod_jk.log](/assets/images/linux/error/mod_jk/error-1.png)

에러는 다음과 같았으며,

> Could not find worker with name 'ajp13_worker' in uri map post processing.

이에 대해 인터넷에 검색하던 중 다음의 게시글을 찾을 수 있었다.

[Stack Overflow](https://stackoverflow.com/questions/59035732/could-not-find-worker-with-name-ajp13-worker "Stack Overflow")

해결방법은 /etc/apache2/mods-available 내에 있는 httpd-jk.conf 파일을 jk.conf 파일로 변경한 후, 원본 파일인 /etc/apache2/mods-available/jk.conf를 대상 파일인 /etc/libapache2-mod-jk/httpd-jk.conf에 대해 심볼릭 링크 파일을 생성해주면 된다.

예전에는 이러한 과정을 거치지 않았던 것 같은데...
