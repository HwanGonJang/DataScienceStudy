# 12월 논문 리뷰 1주차 Conditional GAN
# Conditional Generative Adversarial Nets

## 개요

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_6-1.png?raw=true'>

미리 만들어 놓은 맵을 바탕으로 실제 사진처럼 합성하는 과정. 여러가지 자동차에 대한 UI를 넣어서 자동차의 모양, 색 등을 바꿀 수 있다. ← Conditional(조건)

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_6-2.png?raw=true'>


Conditional GAN은 일반 GAN을 바탕으로 condition(조건)을 설정하여 생성자가 그 조건에 맞게 이미지를 생성하는 모델이다.



## 수식

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_6-3.png?raw=true'>


GAN에서 각 생성자에 condition y가 들어간다. 나머지는 GAN과 동일.

↔**GAN 수식**

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_6-4.png?raw=true'>




## 기본적인 과정

### 1. Label

label은 딥러닝에서 예측하고자 하는 대상의 항목을 의미한다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_6-5.png?raw=true'>


기본적으로 GAN과 동일하나 생성자와 판별자 모두 랜덤한 latent 벡터에 condition 레이블을 붙여준다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_6-6.png?raw=true'>


1. 판별자에 이미지 5와 이 이미지가 5임을 명시하는 condition 레이블을 넣어준다.
2. 생성자에도 같은 condition 레이블을 주고 생성한 이미지를 condition을 받은 판별자가 판별. 처음은 0
3. 학습이 충분히 되면 생성자가 매우 그럴듯한 이미지를 생성해 판별자의 출력이 1이 나온다.



### 2. Data From Other Modalities

condition으로 레이블이 아닌 입력한 소스와 다른 형식의 데이터를 넣어주는 방법.

### Tag Generator

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_6-7.png?raw=true'>


1. 생성자에 입력으로 랜덤 노이즈를 주고 생성자는 태그를 생성한다. 
2. 판별자의 입력(정답)으로 사용자가 생성한 태그를 준다.
3. condition으로는 이미지를 준다.(x, z와 y가 다른 형식의 데이터)
4. 결국 판별자는 데이터 x와 y의 pair가 생성자의 태그와 데이터 y의 pair 와 matching이 되는지를 판단한다.



이와 같은 Conditional GAN이 발전하여 만들어진 모델들

1. Image2Image Translation

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_6-8.png?raw=true'>


2. Speech Enhancement

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_6-9.png?raw=true'>