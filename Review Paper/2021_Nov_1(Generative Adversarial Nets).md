# 11월 논문 리뷰 3주차 GAN 수식, 알고리즘 더 자세히 살펴보기
# Generative Adversarial Nets

## 0. Abstract

우리는 대립적인 과정을 통해 생성 모델을 추정하기 위한 새로운 프레임워크를 제안한다. 데이터 분포를 포작하는 생성모델 G와 샘플이 훈련 데이터에서 나왔을 확률을 추정하는 차별 모델 D의 두가지 모델을 동시에 훈련한다. G의 훈련은 D가 실수할 확률을 최대로 높이는 것이다. 임의의 함수 G와 D의 공간에는 G가 훈련 데이터 분포를 복구하고 D가 모든 곳에서 1/2가 되는 특별한 솔루션이 존재한다. G와 D가 다중 퍼셉트론으로 정의되는 경우, 역전파를 통해 시스템 전체를 훈련시킬 수 있다. 실험은 생성된 샘플의 정성적, 정량적 평가를 통해 프레임워크의 잠재력을 입증한다.

## 1. Introduction

딥러닝은 자연이미지, 음성과 같은 인공지능 애플리케이션에서 접하는 데이터의 종류에 대한 확률 분포를 나타내는 풍부하고 계층적인 모델을 발견하는 것이다. 지금까지의 딥러닝은 대개 클래스 레이블에 고차원적이고 풍부한 감각 입력에 매핑하는 모델과 관련있다. 이러한 모델들은 주로 역전달 및 중도하차알고리즘에 바탕을 두고 있으며, 선형 단위들 사용한다. 심층 생성 모델은 다음과 같은 많은 난해한 확률적 계산을 근사하는 어려움 때문에 영향을 덜 받았다. 우리는 이러한 어려움을 비켜가는 새로운 생성 모델 추정 절차를 제안한다.

제안된 적대적 네트 프레임워크에서 생성 모델은 상대에 대하여 배치된다. 즉, 표본이 모델 분포에서 추출되었는지 데이터 분포에서 추출된 것인지 결정하는 방법을 배우는 차별적 모델이다. 생성 모델은 위조 화폐를 만드는 팀과 유사하고, 차별 모델은 위조 화폐를 탐지하려는 경찰과 유사하다고 볼 수 있다. 이는 두 팀 모두 위조품이 진짜와 구별될 수 없을 때까지 그들의 수행 능력을 개선하도록 유도한다.

이 프레임워크는 많은 종류의 모델 및 최적화 알고리즘에 대한 특정 훈련 알고리즘을 산출할 수 있다. 이 논문에서는 생성 모델이 샘플을 생성하는 특별한 경우를 살펴본다.



## 2. 이론 설명

### 2-1. 이산확률분포 vs 연속확률분포

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_2-1.png?raw=true'>

이산확률분포는 x확률 분포가 정해져 있을 때, 연속확률분포는 x 확률 변수가 정해져 있지 않을 때 사용한다. 즉, 실제 세계 데이터는 정규분포로 표현할 수 있다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_2-2.png?raw=true'>

현실과 가장 가까운 데이터인 이미지 데이터는 다차원 특징 공간의 한 점으로 표현되므로 통계적인 평균치가 존재한다.



### 2-2. 생성 모델

실존하지 않지만 있을 법한 이미지를 생성할 수 있는 모델 ⇒ 통계적, 새로운 데이터 생성

목표: 이미지 데이터의 분포를 근사하는 모델  G를 만드는 것.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_2-3.png?raw=true'>

시간이 지나면서 원본 데이터를 학습한다. 학습이 잘 되었다면 d처럼 통계적으로 평균적인 특징을 가지는 데이터를 생성할 수 있다.



### 2-3. GAN(Generative Adversarial Networks)

생성자와 판별자 두 개의 네트워크를 활용한 생성 모델.

목적 함수를 통해 생성자는 이미지 분포를 학습할 수 있다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_2-4.png?raw=true'>

판별자 D는 진짜 이미지를 1. 가짜를 0으로 도출할 수 있도록 하며, 생성자 G는 가짜 이미지가 판별자에 의해 1을 도출할 수 있도록 학습한다. 이 과정을 반복하여 G가 그럴듯한 이미지를 생성할 수 있도록 한다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_2-5.png?raw=true'>



## 3. 결과

GAN은 실제로 학습과정을 거치면서 실제로 있을 법한 이미지를 생성할 수 있었고 GAN 등장 기준으로 이전의 모델 보다 성능도 좋았다.