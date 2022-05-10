---
layout: single
title: "Linux - Hosts"
categories: Linux
tag: [Linux, Command, Centos, Window, method, Host, Domain]
---

# 간단 정의

## HOSTS?

Domian Name Server를 사용하기 전에 IP와 Domain Name를 내부적으로 맵핑

## Domian [ Name ] ?

- IP주소를 대체할 수 있는 URL 주소 ( 호스트명 )라고 보면 된다
- E.g.
  - IP주소 : 223.130.200.107
  - Domain Name : www.google.com

## Domian Name Server \<Server Name >?

- IP -> Domain Name , Domain Name -> IP로 치환해주는 Server
- 위치는 사용하는 인터넷 통신사 서버 등에 주로 존재한다

# 간단 DNS 예시

![DNS 로직](https://user-images.githubusercontent.com/53324492/167662015-85e47864-84bd-4c60-9e22-7b264559d8fa.png)

# CentOS 7 / window Hosts 설정

> CentOs , Window 모두 경로만 잘 작성하면 간편하게 만들 수 있다.
>
> 해당 파일에 원하는 Hosts를 위한 값들을 작성하면 된다.

## CnetOS 7

- Hosts 파일경로

  - /etc/hosts

- 삽입 데이터 형식

  - [IP] [HOSTNAEM] [Alias1] [Alias2] …

- E.g

  - 192.168.10.1 bapa1.com bapa1 b1

## Window

- Hosts 파일경로 **`< 변경시 관리자 권한으로 해야 저장 가능하다 >`**

  - C:\Windows\System32\drivers\etc\hosts

- 삽입 데이터 형식

  - [IP] [HOSTNAEM] [Alias1] [Alias2] …

- E.g

  - 192.168.10.1 bapa1.com bapa1 b1
