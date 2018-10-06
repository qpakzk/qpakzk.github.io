---
layout: post
title: "[PL] Static Typing vs Dynamic Typing"
description: ""
tags: [PL]
redirect_from:
  - /2018/10/06/
---

# Static Typing vs Dynamic Typing
Static typing은 runtime 이전(또는 compile-time)에 하는 type checking으로 static typing을 하는 프로그래밍 언어를 정적 타입 언어(Statically typed language)라고 한다. Dynamic typing은 runtime에 하는 type checking으로 dynamic typing을 하는 프로그래임 언어를 동적 타입 언어(Dynamically typed language)라고 한다.

## Advantages/Disadvantages of statically typed language
여기서 언급하는 정적 타입 언어의 장단점은 동적 타입 언어와 비교했을 때의 장단점을 의미한다.

### Advantages
* type checking을 runtime 전에 하기 때문에 실행 속도가 빠르다.
* 컴파일 최적화(compile optimization)가 가능하여 runtime 효율성을 향상시키고 메모리 사용을 절약할 수 있다.

### Disadvantages
* 엄격하다(rigid).
* development-time이 길다.
* 빠르게 변화하는 요구사항에 대처하기 어렵다.

## Advantages/Disadvantages of dynamically typed language
여기서 언급하는 동적 타입 언어의 장단점은 정적 타입 언어와 비교했을 때의 장단점을 의미한다.

### Advantages
* 유연하다(flexible).
* 프로그램과 상호작용(interactive)하게 개발할 수 있기 때문에 development-time이 짧다.
* 빠르게 변화하는 요구사항에 대처하기 쉽다.

### Disadvantages
* type checking을 runtime에 하기 때문에  실행 속도가 느리다.
* runtime error가 많이 발생한다.

## Runtime differenece

동적 타입 언어와 동적 타입 언어의 실행 시 차이점을 알아보자.

정적 타입 언어인 C와 동적 타입 언어 Python을 통해 예를 들어 보자. C와 Python 소스코드에서 if 문 안에 "3" + 1 문장이 존재한다고 가정하자.

```c
int var;
if(0) {
    var = "3" + 1;
}
```

```python
if 0:
    var = "3" + 1
```

if 문의 조건이 false라서 "3" + 1은 실행되지 않는다. C에서는 type checking을 runtime 전에 하기 때문에 타입 에러가 발생하지만 Python에서는 type checking을 runtime에 하기 때문에 실행되지 않는 문장이므로 정상적으로 동작한다.
