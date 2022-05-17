---
layout: single
title: "Linux - staticIP"
categories: Linux
tag: [Linux, Command, Centos, static IP, VM, VirtualBox]
---

# 간단 정의

## static IP?

IP는 크게 Dynamic , Static이 존재한다

**`Dynamic`**은 IP를 매번 할당하여, 항상 동일한 IP를 사용 하는 것이 아니다.

**`Static`**은 IP를 고정되게 할당하여, 항상 동일한 IP를 사용 한다

# VM VirtualBox 설정

1.  VM VirtualBox

    1. ![설정](https://user-images.githubusercontent.com/53324492/168844386-e6f4b045-1ac7-4dbb-b9c4-12984d3e514f.png)

       1. 파일 - 호스트 네트워크 관리자 클릭
       1. 혹은 ctrl + H 를 눌러 호스트 네트워크 관리자를 킨다.

    1. ![호스트 네트워크 관리자](https://user-images.githubusercontent.com/53324492/168843878-8cd3462a-ab5d-4e06-ac4e-dbe70c1f7a78.png)

       1. 만들기를 누른다 ( 사실 기존에 있는 것으로 사용해도 된다 )
       1. DHCP (Dynamic Host Configuration Protocol) 를 체크

    1. ![VM 네트워크 설정](https://user-images.githubusercontent.com/53324492/168843893-250ae8c4-ae97-43c6-82b0-8a4fd160f578.png)

       1. 생성한 접속 정보에 할당시켜준다 .
          - 이름에 본인이 생성한 Adapter를 삽입해 주면 된다.

    1. ![ifconfig - 검정](https://user-images.githubusercontent.com/53324492/168843898-84447d2a-04fc-4b6a-a69c-06bdd8281ffb.png)
       1. ifconfig 명령어를 이용하여 정보확인
          - 일반적으로 enp0s8이 새로 생성한 연결 정보일 것이다.

# 설정 방법

## /etc/sysconfig/network-scripts/ifcfg-enp0s8 수정

아래와 같이 수정하면 끝난다.

```sh
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp0s8
UUID=28dd1e08-177c-4270-a79d-a7444e84f553
DEVICE=enp0s8
IPV6_PRIVACY=no
ONBOOT=yes
IPADDR=192.168.100.103
PREFIX=24
GATEWAY=192.168.100.254

# 위에것들 간단 설명
# BOOTPROTO : 유동 IP 여부. (dhcp,static,none)
# ONBOOT : 부팅 시 어탭터 활성화 여부
# IPADDR : 고정 IP주소
# PREFIX : Netmask ( 255.255.255.0 , C-Class)
# NETMASK : PREFIX를 추가 시 필요 없음
# GATEWAY : Gateway주소
```
