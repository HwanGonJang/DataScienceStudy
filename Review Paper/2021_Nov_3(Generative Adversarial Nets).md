# 11월 논문 리뷰 3주차 GAN 수식, 알고리즘 더 자세히 살펴보기
# Generative Adversarial Nets

## 개요

GDSC Soongsil (Google Development Student Club), 숭실대학교의 GDSC 에서 제가 참여한 AI 파트는 매월 하나의 논문을 매주 리뷰하기로 했습니다. 11월 논문 리뷰는 Generative Adversarial Nets 라는 논문입니다. 

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_1-0.png?raw=true'>

11월 부터는 위의 머신러닝 논문의 발전 방향에 맞게 논문을 리뷰합니다.



## GAN에서 사용된 식과 알고리즘 더 자세히 살펴보기

### 1. 목적함수 V
- 생성자 Generator는 min, 판별자 Dicriminator는 max 가 되도록 함.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_4-1.jpg?raw=true'>



### 2. Global Optimality 증명
- 판별자와 생성자의 Global Optimality(최적(max,min)이 되는 값) 증명.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_4-2.jpg?raw=true'>



### 3. 실제 구현을 위한 알고리즘

- 상승(max) 방식을 통한 판별자 학습과 하강(min) 방식을 통한 생성자 학습 알고리즘.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_4-3.png?raw=true'>



### 4. . Pg가 Pdata로 잘 수렴할 수 있는가에 대한 증명(Convex 하기 때문에 가능하다)

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_4-4.png?raw=true'>

 V 함수에서 생성자의 분포인 Pg로 미분하면 앞 항은 상수처럼 취급되고 뒷 항의 영향만 받기 때문에 함수 V는 Pg의 도메인에서 convex 로 불 수 있고 뒷 항도 Pg에 대해서 상수 이기 때문에 V는 Pg의 도메인에서 선형 함수로 볼 수 있어 Generator 입장에서 적은 업데이트로도 충분히 수렴할 수 있다.



### 5. 한계

 현실적으로 딥러닝 아키텍처는 임계점이 여러개일 수 밖에 없다. 딥러닝에서 파라미터 공간에서는 임계점이 여러개 존재 할 수 밖에 없기 때문에 이론과 다르게 실제 구현 상에서는 딥러닝을 구현할 때의 패널티가 존재한다. 



### 6. 결론

 GAN을 통한 여러개의 데이터셋에 대한 가짜 이미지를 생성하였으나 완전히 동일한 결과물을 도출하지 못했다. 즉, GAN은 현실에 있을 법한 이미지를 생성하는 모델이다. 

 GAN은 논문 발표 당시를 기준으로 기존의 다른 여러가지 모델들과 비교하여 충분히 경쟁적인 성능을 보여준다.