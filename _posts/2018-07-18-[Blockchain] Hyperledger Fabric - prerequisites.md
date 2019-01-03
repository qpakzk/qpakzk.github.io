---
layout: post
title: "[Blockchain] Hyperledger Fabric - prerequisites"
description: ""
tags: [Blockchain]
redirect_from:
  - /2018/07/18/
---

# Hyperledger Fabric - prerequisites

Hyperledger Fabric을 이용하여 블록체인 애플리케이션을 개발하고 운영하기 위해서는 Hyperledger Fabric을 사용할 환경에 다음과 같은 프로그램이 설치되어 있어야 한다.

* cURL
* python
* docker
* docker-compose
* go language
* node.js

본 포스트는 Ubuntu 18.04 LTS 환경에서 Hyperledger Fabric v1.2에 맞춰 실습을 진행할 예정이다.

## 패키지 설치

cURL, python 및 기타 필요한 패키지를 설치한다.

```sh
$ sudo apt-get install curl libtool build-essential vim git python
```

python은 2.7 버전이 필요하다.

```sh
$ python --version
Python 2.7.15rc1
```

## docker 설치

```sh
$ curl -fsSL https://get.docker.com/ | sudo sh
```

root 권한 없이 docker 명령을 실행시키기 위해서는 docker 그룹에 계정을 추가해야 하다. 본 포스트에서는 계정으로 실습에서 사용하는 Ubuntu 18.04 LTS 환경의 계정인 frodo를 사용한다.

```sh
$ sudo usermod -aG docker frodo
```

docker service를 재시작한다.

```sh
$ sudo service docker restart
```

docker service가 시작되었는지 확인한다.

```sh
$ docker info
```

## docker-compose 설치

 > 1.21.2 – compatible with v1.2

```sh
$ sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```

docker-compose에 실행 권한을 설정한다.

```sh
$ sudo chmod +x /usr/local/bin/docker-compose
```

docker-compose이 제대로 설치되었는지 확인하기 위해 버전을 확인해본다.

```sh
$ docker-compose -v
```

## go 언어 설치

go 언어 압축 파일을 다운로드 받는다.

```sh
$ wget https://dl.google.com/go/go1.9.6.linux-amd64.tar.gz
```

/usr/local 디렉토리 경로에 go 언어 압축 파일을 풀어 놓는다.

```sh
$ sudo tar -C /usr/local -xzf go1.9.6.linux-amd64.tar.gz
```

~/.bashrc에 환경 변수를 정의하고 경로를 설정한다.

```sh
$ vi ~/.bashrc
...
export USER_LOCAL=/usr/local
export GOROOT=$USER_LOCAL/go
export GOPATH=~/project/go_workspace
export PATH=$PATH:$GOROOT/bin
```
## node.js 설치

node.js는 8.9.x 버전이 필요하다.

```sh
$ wget https://nodejs.org/dist/v8.9.4/node-v8.9.4-linux-x64.tar.gz
$ sudo tar -C /usr/local -xzf node-v8.9.4-linux-x64.tar.gz
```

~/.bashrc에 환경 변수를 정의하고 경로를 설정한다.

```sh
$ vi ~/.bashrc
...
export PATH=$PATH:$USER_LOCAL/node-v8.9.4-linux-x64/bin
```

## 참고문헌

* https://hyperledger-fabric.readthedocs.io/en/release-1.2/prereqs.html
