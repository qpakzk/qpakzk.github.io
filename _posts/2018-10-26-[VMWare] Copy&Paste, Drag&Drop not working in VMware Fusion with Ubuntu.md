---
layout: post
title: "[VMWare] Copy&Paste, Drag&Drop not working in VMware with Ubuntu (KR)"
description: ""
tags: [VMWare]
redirect_from:
  - /2018/10/26/
---

# Copy&Paste, Drag&Drop not working in VMware Fusion with Ubuntu

본 포스트 내용은 아래 환경에서 진행되었다.

> * VMWare Fusion 10
> * Host OS : macOS Mojave
> * Guest OS : Ubuntu 16.04

VMWare Fusion에서 Host OS인 macOS와 Guest OS인 Ubuntu 간에 Copy&Paste, Drag&Drop이 잘 되다가 갑자기 안되는 경우가 종종 발생한다. 이때 다음과 같은 과정을 거쳐 문제를 해결하였다.

## Delete VMWare Tools

VMWare Tools을 제거한다.

```sh
$ sudo apt-get autoremove open-vm-tools
```

리부팅을 진행한다.

```sh
$ systemctl reboot -i
```

## Reinstall VMWare Tools

다시 VMWare Tools를 설치한다.

```sh
$ sudo apt-get install open-vm-tools open-vm-tools-desktop -y
```

리부팅을 진행한다.

```sh
$ systemctl reboot -i
```

리부팅 후 macOS와 Ubuntu 사이의 Copy&Paste, Drag&Drop가 다시 정상적으로 작동한다.
