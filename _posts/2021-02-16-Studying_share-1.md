---
title: "ShareLaTeX: Installing & Settings"

classes: wide

categories:
  - ShareLaTeX
  - Linux
tags:
  - Mathematics
  - LaTex
  - ShareLaTeX
  - Tool

toc: true
---

이번 포스팅에서는 ShareLaTeX를 서버에 설치하고 설정하는 방법에 대해서 알아보고자 한다.

# Prerequisites

## OS

### Version

* Ubuntu 20.04.1 (LTS)

### Architecture

* x86-64

<br/>

# Installing

## Docker-CE

먼저 Docker-CE를 설치하자.

```shell
$ sudo apt-get update

$ sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$ sudo apt-key fingerprint 0EBFCD88

$ sudo add-apt-repository \
 "deb [arch=amd64] https://download.docker.com/linux/ubuntu \ 
 $(lsb_release -cs) \ 
 stable"

$ sudo apt-get update

$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## pip3

docker-compose를 설치하기 위해 pip3도 설치해주자.

```shell
sudo apt-get install python3-pip
```

## Docker-Compose

docker-compose를 설치하자.

```shell
pip3 install docker-compose
```

## Configuring ShareLaTeX

ShareLaTeX를 설정하자.

디렉토리 생성 및 파일 다운받기

```shell
mkdir /etc/sharelatex
cd /etc/sharelatex
wget https://raw.githubusercontent.com/sharelatex/sharelatex/master/docker-compose.yml
```

디렉토리 생성

```shell
mkdir /var/lib/sharelatex
mkdir /var/lib/sharelatex/data
mkdir /var/lib/sharelatex/mongodb
mkdir /var/lib/sharelatex/redis
```

### Editing a docker-compose.yml

```shell
vim docker-compose.yml
```

From

```shell
volumes:
    - ~/sharelatex_data:/var/lib/sharelatex
```

To

```shell
volumes:
    - /var/lib/sharelatex/data:/var/lib/sharelatex
```

From

```shell
volumes:
    - ~/mongo_data:/data/db
```

To

```shell
volumes:
    - /var/lib/sharelatex/mongodb:/data/db
```

From

```shell
volumes:
    - ~/redis_data:/data
```

To

```shell
volumes:
    - /var/lib/sharelatex/redis:/data
```

From

```shell
ports:
    - 80:80
```

To

```shell
ports:
    - 0.0.0.0:x:80  # x : Listening Port
```

From

```shell
environment:

            SHARELATEX_APP_NAME: Overleaf Community Edition

            SHARELATEX_MONGO_URL: mongodb://mongo/sharelatex

            # Same property, unfortunately with different names in
            # different locations
            SHARELATEX_REDIS_HOST: redis
            REDIS_HOST: redis

            ENABLED_LINKED_FILE_TYPES: 'url,project_file'

            # Enables Thumbnail generation using ImageMagick
            ENABLE_CONVERSIONS: 'true'

            # Disables email confirmation requirement
            EMAIL_CONFIRMATION_DISABLED: 'true'

            # temporary fix for LuaLaTex compiles
            # see https://github.com/overleaf/overleaf/issues/695
            TEXMFVAR: /var/lib/sharelatex/tmp/texmf-var

            ## Set for SSL via nginx-proxy
            #VIRTUAL_HOST: 103.112.212.22

            # SHARELATEX_SITE_URL: http://sharelatex.mydomain.com
            # SHARELATEX_NAV_TITLE: Our ShareLaTeX Instance
            # SHARELATEX_HEADER_IMAGE_URL: http://somewhere.com/mylogo.png
            # SHARELATEX_ADMIN_EMAIL: support@it.com

            # SHARELATEX_LEFT_FOOTER: '[{"text": "Powered by <a href=\"https://www.sharelatex.com\">ShareLaTeX</a> 2016"},{"text": "Another page I want to link to can be found <a href=\"here\">here</a>"} ]'
            # SHARELATEX_RIGHT_FOOTER: '[{"text": "Hello I am on the Right"} ]'

            # SHARELATEX_EMAIL_FROM_ADDRESS: "team@sharelatex.com"

            # SHARELATEX_EMAIL_AWS_SES_ACCESS_KEY_ID:
            # SHARELATEX_EMAIL_AWS_SES_SECRET_KEY:

            # SHARELATEX_EMAIL_SMTP_HOST: smtp.mydomain.com
            # SHARELATEX_EMAIL_SMTP_PORT: 587
            # SHARELATEX_EMAIL_SMTP_SECURE: false
            # SHARELATEX_EMAIL_SMTP_USER:
            # SHARELATEX_EMAIL_SMTP_PASS:
            # SHARELATEX_EMAIL_SMTP_TLS_REJECT_UNAUTH: true
            # SHARELATEX_EMAIL_SMTP_IGNORE_TLS: false
            # SHARELATEX_CUSTOM_EMAIL_FOOTER: "This system is run by department x"

```

To

```shell
environment:
          SHARELATEX_MONGO_URL: mongodb://mongo/sharelatex
          SHARELATEX_REDIS_HOST: redis
          SHARELATEX_APP_NAME: ShareLaTeX

          # Put here the information about your ShareLaTeX site:
          SHARELATEX_SITE_URL: https://my.sharelatex.tld
          SHARELATEX_NAV_TITLE: ShareLaTeX - My beautiful ShareLaTeX Installation
          # Uncomment the following line if you want to display a logo (i.e., of your school or university)
          # SHARELATEX_HEADER_IMAGE_URL: http://somewhere.com/mylogo.png
          # Put your email address here:
          SHARELATEX_ADMIN_EMAIL: my@email.com

          SHARELATEX_LEFT_FOOTER: '[{"text": "Powered by <a href=\"https://github.com/sharelatex/sharelatex\">ShareLaTeX</a>"}]'
          SHARELATEX_RIGHT_FOOTER: '[{"text": "Run your own instance on <a href=\"https://scaleway.com\">Scaleway</a>"} ]'

          # Configure the email address that will be displayed in emails sent by ShareLaTeX
          SHARELATEX_EMAIL_FROM_ADDRESS: "my@email.com"

          # Enable the installation behind a proxy
          SHARELATEX_BEHIND_PROXY: 'true'
          SHARELATEX_SECURE_COOKIE: 'true'

          # Set the language of the installation. For example 'en' English, 'de' German, 'fr' French ...
          SHARELATEX_SITE_LANGUAGE: 'en'

          # Configure the settings for outgoing mails
          SHARELATEX_EMAIL_SMTP_HOST: 'localhost'
          SHARELATEX_EMAIL_SMTP_PORT: '465'
          SHARELATEX_EMAIL_SMTP_SECURE: 'true'
          SHARELATEX_EMAIL_SMTP_USER: 'sharelatex'
          SHARELATEX_EMAIL_SMTP_PASS: 'YOUR_PASSWORD'
          # SHARELATEX_EMAIL_SMTP_TLS_REJECT_UNAUTH: 'true'
          # SHARELATEX_EMAIL_SMTP_IGNORE_TLS: 'false'
          # Set a footer for outgoing mails:
          SHARELATEX_CUSTOM_EMAIL_FOOTER: "<div>Powered by ShareLaTeX</div>"
```

## Docker-Compose up

```shell
sudo docker-compose up
```

## Check

웹 주소창에 아래의 형식으로 주소를 입력하여 접속한다.

```shell
http://IP:PORT
```

아래처럼 나오면 성공이다.

![Check](/assets/images/sharelatex/install/sharelatex-check-01.png)

## Configuring Systemd

먼저 ctrl+c 조합을 이용하여 실행중인 프로세스를 종료시키자.

```shell
/etc/systemd/system/
```

위 경로에 sharelatex.service 파일을 생성하자.

```shell
vim /etc/systemd/system/sharelatex.service
```

그러고 나서 다음을 입력해주자.

```shell
[Unit]
    Description=ShareLaTeX Service
    After=docker.service

    [Service]
    Type=simple
    WorkingDirectory=/etc/sharelatex
    ExecStart=/usr/local/bin/docker-compose -f /etc/sharelatex/docker-compose.yml up
    ExecStop=/usr/local/bin/docker-compose -f /etc/sharelatex/docker-compose.yml down

    [Install]
    WantedBy=multi-user.target
```

파일 저장 후 다음의 명령어들을 순차적으로 터미널에 입력하자.

```shell
$ systemctl enable sharelatex

$ systemctl daemon-reload

$ systemctl start sharelatex
```

## Register

Admin 계정을 등록하기 위해 웹 주소창에 아래의 형식으로 주소를 입력하여 접속한 뒤, 계정을 생성해주면 끝이다.

```shell
http://IP:PORT/launchpad
```

# References

[Docker](https://docs.docker.com/engine/install/ubuntu/)

[ShareLaTeX](https://www.scaleway.com/en/docs/installing-sharelatex-ubuntu/)



