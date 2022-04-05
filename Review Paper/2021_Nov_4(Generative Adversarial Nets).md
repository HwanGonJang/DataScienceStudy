# 11월 논문 리뷰 4주차 개념 탐구하기
## Generative Adversarial Nets 에서 사용된 개념 알아보기

## 개요

GDSC Soongsil (Google Development Student Club), 숭실대학교의 GDSC 에서 제가 참여한 AI 파트는 매월 하나의 논문을 매주 리뷰하기로 했습니다. 11월 논문 리뷰는 Generative Adversarial Nets 라는 논문입니다. 

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_1-0.png?raw=true'>

11월 부터는 위의 머신러닝 논문의 발전 방향에 맞게 논문을 리뷰합니다.



### 1. 경사 하강 알고리즘
비용 함수(Cost Function)의 비용값을 최소화 하는 파라미터 θ를 찾는 알고리즘입니다. 경사 하강 알고리즘은 비용 함수 J(θ(0),θ(1))를 최소화 하는 θ를 구하는 알고리즘으로 머신러닝에서 굉장히 폭넓게 쓰입니다.
* θ에 대해 임의의 초기값 즉 시작점을 잡습니다.
* 그리고 J가 최소가 될때까지 θ값 갱신을 반복하여 최솟값에 도달했을 때 해당하는 θ를 찾아냅니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_5-1.png?raw=true'>

* a 뒤에 곱해진 것은 비용함수 J의 미분값
* a = learnig rate : 갱신되는 θ 값의 속도를 결정합니다. 

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_5-2.png?raw=true'>

위와 같이 반복적인 갱신을 통해 최종적인 min 값에 도달하는 것이 최종 목표입니다.

#### 1-1. 미분 값
미분 값은 해당 지점에서의 기울기를 의미하므로 경사 하강 알고리즘에서는 초기값을 오른쪽에 두면 갱신마다 갱신 시 θ는 감소하고, 왼쪽에 두면 갱신 시 θ는 증가합니다. 따라서 초기값의 위치에 상과없이 결국 최소값으로 수렴합니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_5-3.png?raw=true'>



#### 1-2. Learning rate 학습 속도

 만약 Learning Rate가 지나치게 작다면 최솟값에 도달하기 위해 굉장히 많은 연산이 요구됩니다. 반대로 Learning Rate가 지나치게 크다면 θ가 반대쪽을 오가며 매우 큰 거리를 이동하게 되어 최솟값에서 점점 멀어지게 됩니다. 그렇기 때문에 적절한 Learning Rate를 설정하는 것은 매우 중요합니다. Learning Rate는 속도에도 영향을 주는데, 만약 Learning Rate없이 미분값으로만 갱신을 진행하게 되면 최솟값으로 도달하지 않고, 제자리에서 진동할 수도 있기 때문에 Learning Rate를 곱하여 갱신값에 변화를 주며 최솟값에 도달하게 해야합니다.



#### 1-3. θ의 수렴 조건

기울기가 0 인 점, 즉 미분값이 0인 시점에서 갱신을 멈춥니다. (갱신값의 변화가 없을 때)


### 2. KLD(쿨백-아리블러 발산),  JSD(젠슨-섀넌 발산)
Kullback-Leibler Divergence 와 Jensen-Shannon Divergence는 서로 다른 확률 분포의 차이를 즉정하는 척도입니다. 우리가 추정한 확률 분포와 실제 확률 분포 사이의 차이가 작다면 좋은 추정이라고 할 수 있습니다.

#### 2-1. Killback-Leibler Divergence
KLD는 두 모델이 얼마나 비슷하게 생겼는지를 알기 위한 척도인데, 제시한 모델이 실제 모델의 각 item들의 정보량을 얼마나 잘 보존하는지를 측정합니다. 즉, 원본 데이터가 가지고 있는 정보량을 잘 보존할 수록 원본 데이터와 비슷한 모델이라는 것입니다. item p(i)가 갖는 정보량은 다음과 같다면

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_5-4.png?raw=true'>

원본 확률 분포 p와 근사된 분포 q에 대하여 i번째 item이 가진 정보량의 차이는 다음과 같습니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_5-5.png?raw=true'>

p에 대하여 이러한 **근사시 상대적 정보 손실량의 기댓값**을 구한 것이 바로 Killback-Leibler Divergence입니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_5-6.png?raw=true'>



#### 2-2. Jensen-Shannon Divergence

KLD는 근사된 확률 분포가 얼마나 원본과 비슷한지를 측정하는 척도 이외에도, 단순히 두 대등한 확률 분포가 얼마나 닮았는지를 측정하는 척도로 쓰일 수 있습니다. 그러나 위의 식에 근거하여 KLD는 역의 관계가 성립하지(Symmetric) 않습니다. 즉, D(KL)(p||q) != D(KL)(q||p) 입니다. 따라서 이 KLD를 Symmetric 하게 개량한 Jensen-Shannon Divergence를 사용합니다.

<img src='https://github.com/HwanGonJang/HwanGonJang.github.io/blob/master/Pictures/ai_5-7.png?raw=true'>

위와 같이 KLD를 개량하면 JSD(p,q) = JSD(q,p) 가 되어 두 확률 분포의 차이(distance)로서의 역할을 수행합니다.





