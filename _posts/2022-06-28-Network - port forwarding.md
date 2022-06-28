---
layout: single
title: "Network - port forwarding"
categories: Network
tag: [Network, port forwarding, 포트포워딩, IPTIME]
---

# 포트포워딩 (port forwarding) ?

포트를 열어주는 것이다.

![포트포워딩 과정 흰색](https://user-images.githubusercontent.com/53324492/176208511-56c2a7a3-a6d3-48f1-991c-6fb44edf8307.png)

위와 같이 닫힌 문 ( 포트 ) **`잠긴 문을 열어주는 행위`** (포트포워딩) 라고 생각하면 된다.

# 간단 과정

본인은 아래와 같은 과정에서 진행을 할 것이다.

![포워딩 순서 흰색](https://user-images.githubusercontent.com/53324492/176209453-5a17ffb3-8274-4206-a768-05dbeca673ed.png)

## IPTIME

IPTIME에서 우선 PortFoward를 해준다.

고급설정 – NAT/라우터 관리 – 포트포워드 설정

![IPTIME 설정](https://user-images.githubusercontent.com/53324492/176210019-1bc35767-1a53-4e48-9a9c-229b2ff3fee6.png)

## 인바운드 설정 ( Window 방화벽 설정 )

> 인바운드 ( Inbound ) 는 클라이언트에서 서버로 연결할 떄 사용할 규칙이라고 생각하면 된다.
>
> 아웃바운드( Outbound ) 는 반대 개념이다.

**`Win + R`** 을 눌러 실행창에 **`wf.msc`** 를 검색하여 실행하거나

**`Win`** 을 눌러 **`고급 보안이 포함된 Windows Defender 방화벽`** 을 검색하여

고급 방화벽을 실행시킨다.

![image](https://user-images.githubusercontent.com/53324492/176210328-f6854368-ea8c-463e-b19e-a87aeeead7e8.png)

실행시키면 다음과 같은 것이 나오는데 아래 그림과 같이

인바운드 --> 새 규칙 --> 포트를 클릭하고 진행해준다.

![image](https://user-images.githubusercontent.com/53324492/176210755-ecd05373-5b45-49b0-8886-a7fb5b027287.png)

본인이 TCP 혹은 UDP를 선택하고, 원하는 Port번호를 설정하여 진행한다.

이것 이후는 본인이 원하는 보안 규칙에 맞게 설정해주면 된다.

![인바운드 03](https://user-images.githubusercontent.com/53324492/176211848-0fb88d16-c779-4bdd-aa99-38c6f0fad94b.png)

## Virtual Box

원하는 VM에서 마우스 우클릭 + 설정을 누른 다음 네트워크에서 아래와 같이 순서대로 진행하면 된다.

호스트 Port에 위에서 열어준 Port를 작성하면되고, 게스트 포트에 VM내부에서 사용할 Port를 작성하면된다.

VM입장에서보면 Host Port 는 외부 포트고, Guest Port는 내부 포트다

내부 / 외부 포트를 모르겠으면 위로 올라가 다시 읽고오면 된다.

![Virutal Box](https://user-images.githubusercontent.com/53324492/176213427-97f51ecb-96bc-476d-aa78-1375014df647.png)

## Centos 07 Firewalld

이제 마지막으로 VM내부 즉 Linux에서 방화벽을 열어주면 된다.

방법은 2가지다.

1. 방화벽을 꺼버린다

```shell
# centos07 기준

# 방화벽 중지 (  서버를 재시작하면 다시 실행됨 )
systemctl stop firewalld
# 방화벽 완전 사용 중지 ( 서버를 재시작해도 실행 안됨 )
systemctl disable firewalld
```

> 보안을 생각하면 권장하지 않는다.

2. 해당 포트를 열어준다

```shell
# centos07 기준

# 포트 열기
# --permanent : 1회성이 아니고 계속 열림
# --zone=public : zone 설정은 Public 즉 모든 서비스에 대하여 열것
#  --add-port=12345/tcp : 포트번호는 12345 , 방식은 tcp인 포트를 추가할 것이다.
firewall-cmd --permanent --zone=public --add-port=12345/tcp

# 방화벽 리스트 다시 가져오기
firewall-cmd --reload

# 방화벽 리스트 및 열린 포트 확인
firewall-cmd --list-ports
```

# 결론

1. 공유기 : IPTIME
1. 서버 ( 원격지 ) : Window
1. 가상머신 : Virtual box
1. 가상머신 OS : Centos07

위와 같이 4가지 조건이면, 왠만하면 포트가 성공적으로 열릴 것 이다.

성공여부는 Ping을 보내서 확인해보면 된다.

Port까지 사용하여 확인하는 방법은 여러개지만

본인은 윈도우에서는 [TCPING](https://www.elifulkerson.com/projects/tcping.php)(TCP Ping의 약자인듯)을 사용하고, Linux에서는 telnet을 이용하여 포트가 잘 열렸는지 확인한다.
