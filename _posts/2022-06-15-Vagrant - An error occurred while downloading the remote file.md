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
```

> 위 글을 보면 CA 즉 *자격검증*을 실패했다는 의미이다.
>
> 간단하게 해결하고 싶다면, 가장 마지막 문구, --insecure 옵션을 추가해서 설치해면 된다.

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
