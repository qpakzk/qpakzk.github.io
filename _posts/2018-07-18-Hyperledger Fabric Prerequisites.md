---
layout: post
title: "Hyperledger Fabric Prerequisites"
description: ""
tags: [Hyperledger Fabric]
redirect_from:
  - /2018/07/16/
---

# Hyperledger Fabric Prerequisites

## 패키지 설치

```sh
$ sudo apt-get install curl libtool build-essential vim git python
```

## docker 설치
> docker (18.05.0-ce, ubuntu 18.04 LTS) – compatible with v1.2


```sh
$ curl -fsSL https://get.docker.com/ | sudo sh
```

### docker 그룹에 계정 추가

* root 권한 없이 docker 명령을 사용하기 위해 필요
* 본 포스트에서는 계정을 frodo로 설정

```sh
$ sudo usermod -a -G docker frodo
```

### docker service restart

```
$ sudo service docker restart
```

### docker service 체크

```sh
$ docker info
```

## docker-compose 설치

 > 1.21.2 – compatible with v1.2

```sh
$ sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```

### 실행 권한 설정

```sh
$ sudo chmod +x /usr/local/bin/docker-compose
```

### docker-compose 버전 체크

```sh
$ docker-compose -v
```
