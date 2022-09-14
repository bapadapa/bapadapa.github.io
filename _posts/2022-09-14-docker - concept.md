---
layout: single
title: "Docker - Concept"
categories: Docker
tag: [docker, concept, 도커]
---

# 도커 ?

컨테이너를 생성해주는 것을 도와주는 툴

# 컨테이너 Container?

- 특정 프레임워크 특정버전을 코드로 패키징하여 언제든지 다시 사용할 수있게 만들둔 것

- 동일한 환경을 재구축하기 편리하다
  - 재설치 등이 편리함
- 여러 버전을 구축하고 필요할 때 마다 사용할 수 있다.
  - `spark`, `kafka`, `nodeJS` 등을 사용하는데, `1.x 버전`, `2.x 버전` 과 같이 필요한 버전을 컨테이너로 들고 있다가 필요할 때 마다 해당 컨테이너를 사용하여 여러 버전을 편리하게 바꿔가며 사용할 수 있다.

# 컨테이너 와 VM의 차이?

## VM

- Hypervisor아래 여러 서버가 존재하고 각 서버에는 Guest OS가 존재한다.
- 즉 여러개의 kernel이 존재한다.

![vm white](https://user-images.githubusercontent.com/53324492/190177201-a6fa6065-a2f9-4234-a9e6-17b2e5d384a3.png)

## Container

- 하나의 Docker Engine / Daemon 아래에 여러 서버(컨테이너)가 존재한다.
- 일반적으로 각각의 컨테이에 하나의 App를 구축한다고 알고 있다.
- 서버라 볼 수 있지만, 각각을 App관점으로 보는 것이 편할 것 같다.

![docker White](https://user-images.githubusercontent.com/53324492/190177163-3ece7d2b-6848-489e-a47c-9a9fa288e4d1.png)
