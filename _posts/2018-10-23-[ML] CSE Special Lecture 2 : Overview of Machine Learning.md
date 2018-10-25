---
layout: post
title: "[ML] CSE Special Lecture 2 : Overview of Machine Learning (KR)"
description: ""
tags: [ML]
redirect_from:
  - /2018/10/23/
---

# CSE Special Lecture 2 : Overview of Machine Learning

숭실대학교 컴퓨터학부 2018-2학기에 개설된 《컴퓨터공학특강 2》 강의 내용을 요약하였다. 강의와 관련된 소스코드는 [여기](https://github.com/qpakzk/ssu-cse-computer-science-special-lecture2)에서 확인할 수 있다.

## 머신러닝의 종류

* Supervised Learning (지도학습)
  * Regression (회귀)
  * Classification (분류)
* Unsupervised Learning (비지도학습)
  * Clustering (군집화)
* Reinforcement Learning (강화학습)

## Supervised Learning

* 입력값과 정답(label)을 포함하는 training data를 이용하여 학습(learning)하고, 학습된 결과를 바탕으로 미지의 데이터(test data)에 대한 미래 결과값을 예측(predict)하는 기법
* 공부 시간(입력)과 시험 결과(정답)의 상관관계 학습을 통해 합격-불합격 여부 예측
* 평수(입력)와 집값(정답)의 상관관계 학습을 통해 어떤 평수에 대한 집값 예측

### Regression

* training data를 이용하여 연속적인 숫자값을 예측하는 것
* 공부 시간과 시험 성적의 상관관계 학습을 통해 어떤 공부 시간에 대한 시험 성적 예측
* 평수와 집값의 상관관계 학습을 통해 어떤 평수에 대한 집값 예측

### Classification

* training data를 이용하여 입력값의 종류를 구별하는 것
* 공부 시간과 시험 결과의 상관관계 학습을 통해 합격-불합격 여부 예측

## Unsupervised Learning

* training data에 정답은 없고 입력값만 존재할 때 입력값을 통해 정답을 찾는 것이 아니라 입력값의 특성, 패턴을 학습을 통해 발견하는 기법
* 군집화(clustering) 알고리즘을 뉴스 그룹핑, 백화점의 상품 추천 시스템에 활용

## Reinforcement Learning

* 소프트웨어 에이전트(agent)가 환경(environment)에서 보상(reword)을 최대화하는 방향으로 행동(action)을 수행하도록 학습하는 기법
