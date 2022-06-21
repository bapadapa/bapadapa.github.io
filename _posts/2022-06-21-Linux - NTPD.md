---
layout: single
title: "Linux - ntpd"
categories: Linux
tag: [Linux, Command, Centos, ntpd]
---

# NTP ?

Network Time Protocol

서버간 시간을 동기화 시켜주는 프로토콜

그림으로 간단히 표현하면 아래와 같다

![ntpd](https://user-images.githubusercontent.com/53324492/174816073-fd8f5e9a-aea4-4026-9987-eeb4f118fe82.png)

# 시간 동기화 이유 ?

서버간 시간이 맞지 않아 예기치 못한 에러 발생 가능

데이터 삽입시간과 실제 시간과 차이가 날 수 있다.

그런데 그 시간이 차이나는 것을 나중에 알아차리면 데이터가 엉켜있을 수 있고, 프로세스간 시간값이 달라 문제가 발생할 수 있다.

그냥 재앙이다.

# 사용방법 ?

간단하게 사용하는 방법은 NTPD를 설치하여 사용하면 된다.

```shell
# 옛날 버전인 chrony 사용 중지
systemctl disable chronyd

# 설치 및 시작
Yum install –y ntpd
systemctl start ntpd
systemctl enable ntpd

# vim /etc/ntp.config
# 기존의 Server정보를 주석 혹은 제거 후 아래  서버 추가
# 원하는 것을 아무거나 넣으면 된다.

server kr.pool.ntp.org iburst # 코리아 NTP Pool Time Server
server time.bora.net iburst # LGU+
server ntp1.epidc.co.kr iburst # Enterprise IDC 타임서버
```

사람들 말로는 시간을 맞추는데 시간이 조금 걸릴 수 있다고 한다. ( 말하는 것은 5분~30분정도 걸릴 수 있다함)

만약 위와 같이 진행을 했는데, 시간이 안 맞으면 , Date 명령어 수행시 KST와 같이 한국 시간으로 맞춰져 있는지 확인을 해보자.

![UTC to KST](https://user-images.githubusercontent.com/53324492/174817155-91257a25-4ede-45c0-bff1-21a5a7927577.png)

```shell
rm -rf /etc/localtime
ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime
date
```
