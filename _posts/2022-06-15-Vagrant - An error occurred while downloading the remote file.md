---
layout: single
title: "Vagrant - An error occurred while downloading the remote file"
categories: Vagrant
tag: [Vagrant, Centos, Concept, VM, Error, VirtualBox]
---

# Error?

```shell
$ vagrant box add https://app.vagrantup.com/centos/boxes/7 --name centos/7
==> box: Box file was not detected as metadata. Adding it directly...
==> box: Adding box 'centos/7' (v0) for provider:
    box: Downloading: https://app.vagrantup.com/centos/boxes/7
    box:
An error occurred while downloading the remote file. The error message, if any, is reproduced below. Please fix this error and try again.

SSL certificate problem: certificate has expired
More details here: http://curl.haxx.se/docs/sslcerts.html

curl performs SSL certificate verification by default, using a "bundle" of Certificate Authority (CA) public keys (CA certs). If the default bundle file isn't adequate, you can specify an alternate file using the --cacert option.
If this HTTPS server uses a certificate signed by a CA represented in the bundle, the certificate verification probably failed due to a problem with the ertificate (it might be expired, or the name might not match the domain name in the URL).
If you'd like to turn off curl's verification of the certificate, us the -k (or --insecure) option.

혹은

schannel: next InitializeSecurityContext failed: Unknown error (0x80092013) - 해지 서버가 오프라인이므로 해지를 확인하지 못했습니다.

```

> 처음 위와 같은 에러를 발견했을때 해지서버가 뭔지 몰랐었는데, 간단했다.
>
> 위 글을 보면 _CA(Certificate Authority)_ 즉 *자격검증*을 실패<해지 서버(revocation server
> )를 확인 못함>했다는 의미이다.

## 해지(폐기) 서버?

> 통신 시 Client는 Server에게 받은 *SSL인증서 (CA)*의 유효성을 검사하는 메커니즘이 있다.
>
> 이때 CRL (Certificate Revocation Lists)이라는 인증서가 정상이 아니라고 판단된 인증서 폐기(해지) 목록이 있다.
>
> 위 에러는 CRL에 접근을 제대로 하지 못하여, 현재 사용하는 인증서가 *정상여부 판단을 못하는 것*이다.

# Simple Solutition

```shell
$ vagrant box add https://app.vagrantup.com/centos/boxes/7 --insecure --name centos/7
==> box: Loading metadata for box 'https://app.vagrantup.com/centos/boxes/7'
This box can work with multiple providers! The providers that it can work with are listed below. Please review the list and choose the provider you will be working with.

1) hyperv
2) libvirt
3) virtualbox
4) vmware_desktop

Enter your choice: 3
==> box: Adding box 'centos/7' (v2004.01) for provider: virtualbox
    box: Downloading: https://vagrantcloud.com/centos/boxes/7/versions/2004.01/providers/virtualbox.box
==> box: Box download is resuming from prior download progress
    box:
    box: Calculating and comparing box checksum...
==> box: Successfully added box 'centos/7' (v2004.01) for 'virtualbox'!

```

> 위와 같이 `vagrant box add https://app.vagrantup.com/centos/boxes/7 --insecure --name centos/7` 를 삽입해서 진행하면 된다.
>
> 필자는 _guest additions_ 에러가 발생하여 최종적으로는 _centoy/7_ 박스가 아닌, vbguest가 설치된 _bento/centos-7.9_ 를 설치했다.

# Other Solution?

```shell
Vagrant.configure("2") do |config|

  # 보안 포기
  config.vm.box_download_insecure=true

  config.vm.box = "bento/centos-7.9"
  .
  .
  .
```

> vagrantFile에 위 `config.vm.box_download_insecure=true` 를 상단에 추가해주면 `config.vm.box = "bento/centos-7.9"` 로인하여 `bento/centos-7.9`를 설치할 때 _--insecure_ 를 삽입해 준 것과 같은 효과를 낸다.
