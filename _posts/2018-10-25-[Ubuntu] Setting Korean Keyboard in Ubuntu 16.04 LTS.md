---
layout: post
title: "[Ubuntu] Setting Korean Keyboard in Ubuntu 16.04 LTS (KR)"
description: ""
tags: [Ubuntu]
redirect_from:
  - /2018/10/25/
---

# Setting Korean Keyboard in Ubuntu 16.04 LTS

본 포스트에서는 우분투 16.04 LTS에서 한글 입력기(ibus-hangul)를 설치하고 오른쪽 Alt 키로 한영변환이 가능하도록 설정한다.

## Install ibus-hangul

터미널을 열고 다음 명령들을 차례로 실행시킨다.

```sh
$ sudo add-apt-repository ppa:createsc/3beol
$ sudo apt-get update
$ sudo apt-get install ibus ibus-hangul -y
```

## Language Support

* System Settings을 열고 Language Support를 클릭한다.

![]({{ site.baseurl }}/assets/images/ubuntu-ibus-hangul/system-settings1.png)

* Language Support를 들어갔을 때 설치를 요구할 수 있다.
* Keyboard input method system을 IBus로 선택한다.

![]({{ site.baseurl }}/assets/images/ubuntu-ibus-hangul/language-support.png)

* Install/Remove Languages...를 클릭하고 Korean을 체크한다.

![]({{ site.baseurl }}/assets/images/ubuntu-ibus-hangul/installed-languages.png)

## Text Entry

* System Settings을 열고 Text Entry를 클릭한다.

![]({{ site.baseurl }}/assets/images/ubuntu-ibus-hangul/system-settings2.png)

* Input sources to use에 Korean(Hangul)(IBus), English(US)가 담겨져 있어야 한다. +를 클릭하여 추가한다.
* 참고로 +를 클릭한 뒤 Korean을 검색하면 여러 개가 나오는데 반드시 Korean(Hangul)(IBus)로 선택해야 한다. 만약 Korean(Hangul)(IBus)가 없다면 리부팅한다.
* 오른쪽 Alt 키로 한영변환을 하기 위해서는 Switch to next sources using을 클릭하고 오른쪽 Alt를 입력한다.

![]({{ site.baseurl }}/assets/images/ubuntu-ibus-hangul/text-entry.png)

* 오른쪽 Alt를 입력했을 때 Multikey가 입력되지 않고 RAlt 키가 입력된다면 다음 Keyboard 파트를 진행한다.

## Keyboard

* System Settings을 열고 Keyboard를 클릭한다.

![]({{ site.baseurl }}/assets/images/ubuntu-ibus-hangul/system-settings3.png)

* Keyboard > Shortcuts > Typing을 들어가서 Compose Key를 Right Key로 바꾸고 Switch to next source를 클릭한 후 오른쪽 Alt를 입력한다. 그러면 Multikey가 입력된다.

![]({{ site.baseurl }}/assets/images/ubuntu-ibus-hangul/keyboard.png)

## Hangul Mode

* 이제 오른쪽 Alt를 누리면 오른쪽 상단의 한영변환 이미지가 태극문양과 En이 토글될 것이다. 그러나 태극문양일 때에도 한글이 아닌 알파벳이 입력될 수도 있다. 이는 Hangul Mode가 설정되지 않았기 때문이다.
* 태극 문양을 클릭하면 drop down menu가 열리고 Setup을 클릭한다.

![]({{ site.baseurl }}/assets/images/ubuntu-ibus-hangul/hangul-mode-setup.png)

* Hangul 탭에서 Start in hangul mode를 체크한다.

![]({{ site.baseurl }}/assets/images/ubuntu-ibus-hangul/ibus-hangul-setup.png)

* 재부팅하면 한글 문양일 때 한글이 입력될 것이다.
