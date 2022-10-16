---
layout: single
title: "docker - 설치"
categories: docker
tag: [docker, install, 도커, 설치]
---

필자는 Mac이없기 때문에 Window기준으로 설치한다.

현재 사용중인 PC의 사양은
Intel(R) Core(TM) i7-6700 CPU @ 3.40GHz 3.40 GHz
Windows 10 Pro 이다.

Home Edition은 추가로 설청해야 할 것이 있다던데, 추후 `Window 11 Home` 으로 다시 설치할 예정이니
그때 추가하겠다.

- window 11 로 설치해본 결과 아래 과정을 동일하게 수행하면 된다.

# 도커 설치

## Docker*Desktop_Install*설치

[Dokcer Doc](https://docs.docker.com/desktop/install/windows-install/) 이 URL로 들어가서 설치파일을 다운로드 받는다. - 바로 들어가기 싫다면, Docker Desktop 혹은 Docker를 검색해서 docker페이지에 들어간다음 document를 들어가서 설치하면된다. 2. 다운로드만 받고, 가상화 환경, Hyper-V를 활성화 시켜줘야한다.

- 기본 조건은 아래와 같다
  1.  Windows 10 Enterprise, Pro, or Education
  1.  64-bit Processor with Second Level Address Translation (SLAT).
  1.  CPU support for VM Monitor Mode Extension (VT-c on Intel CPUs).
  1.  Minimum of 4 GB memory.

## Hyper-V 활성화

[Hyper-V Document](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)로 들어가서 설치하거나 `window 10 enable hyper v`를 검색하여 윈도우 페이지를 들어가준다.

2.  그러면 아래와 같은 Enable 명령어를 제공한다. 이것을 Powershell을 관리자 권한으로 실행 후 실행시켜주면 된다.

```powershell
  Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

- 위 명령어를 실행시키면 컴퓨터를 재시작하라고 할 것이다. 추가로 1개의 명령어를 실행시켜야하니 N을 눌러주고 다음 명령어를 실행시킨다.

```powershell
  Enable-WindowsOptionalFeature -Online -FeatureName containers -Al
```

## WSL 2 업데이트

WSL 2 업데이트 아래 순서대로 실행시켜주면 된다.

- window 10 Home 은 [이전 버전 WSL의 수동 설치 단계](https://learn.microsoft.com/ko-kr/windows/wsl/install-manual)를 참고하여 설치하면 될 것 같다.

  - 그런데 필자는 Pro인데 왜 하라고 하는지 모르겠다...
  - Linux는 Ubunto 20.04를 설치했다.
  - 아래 명령어들과 MSI파일들을 설치해주면 된다.

  ```powershell
      dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

      dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
  ```

  [x64 머신용 최신 WSL2 Linux 커널 업데이트 패키지](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi) 다운로드 후 설치

  ```powershell
      wsl --set-default-version 2
  ```

  [Ubuntu 20.04 LTS](https://www.microsoft.com/store/apps/9n6svws3rx71)

## 최종 설치

활성화를 마쳤으면 `Docker_Desktop_Install_설치`에서 설치한 Docker Desktop Installer를 실행시켜준다.

- 이 때 모두 체크하고 설치를 하는 것을 권장한다.
- 설치가 완료되며 재시작하면 된다.
- 캡쳐를 저장 못 해서 올리지 못 했지만, 만약 문제가 있다고 하면 초기화 할꺼냐고 물을 것 인데, 초기화 후 재부팅을 하면 잘 설치가 될 것 이다.

![Docker Install](https://user-images.githubusercontent.com/53324492/195377485-f1b61126-445b-42bb-98bf-e9db8b3c004a.png)

- 위와 같이 왼쪽 아래에 녹색으로 되어있으면 성공이다.
