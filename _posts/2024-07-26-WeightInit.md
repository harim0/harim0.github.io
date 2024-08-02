---
title: "Weight Initialization 논문 정리"
categories:
  - nas
tags:
  - study
toc: true
toc_sticky: true
toc_label: "Paper Study"
date: 2024-07-26 17:30:00 +0900
author_profile: false
header:
  overlay_image: # assets/images/pages/2024-07-20.png
  overlay_filter: 0.5 
  teaser: # assets/images/pages/2024-07-20.png
use_math: true
---


## Xavier(2010)   
### Abstract   

Understanding the difficulty of training deep feedforward neural networks 논문에서는 "왜 랜덤 초기화에서의 standard GD가 deep nn에 약한가?" 라는 질문에 답하고, 더 나은 알고리즘을 제안한다.   
1. non-linear activations functions의 영향
  - logistic sigmoid activation이 랜덤 초기화된 deep nn에 부적합한 이유는 top hidden layer를 포화시킬 수 있는 mean value 때문이다.   
  - 포화된 units가 자체적으로 포화 상태를 벗어날 수 있고, 이는 nn training에서의 정체 상태를 설명할 수 있다.   
  - 포화 상태가 적은 새로운 non-linearity가 beneficial 할 수 있다.   
2. activations과 gradients가 training 중 layer에 따라 어떻게 변하는지      
  - 각 layer와 관련된 Jacobian이 1에서 멀어질 수록 훈련이 더 어려워진다.   

&rarr; 수렴 속도를 향상시키는 Xavier initialization 제안   

> **Sigmoid Non-Linearity의 학습 속도 저하 문제**   
*Hessian에서 singular values를 유도하는 non-zero mean 때문에 sigmoid의 non-linearity는 학습 속도를 저하시킨다.*   
$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$   
Sigmoid 함수의 포화 상태(기울기&rarr;0)에서는 2차 미분값은 0으로, Hessian 행렬의 대각 성분은 매우 작아져 학습 속도가 저하될 수 있다. non-linearity가 강할 경우에는 특정 방향으로의 곡률이 커지거나 작아져 Hessian의 singular value가 급격히 변동할 수 있어 학습 속도와 안정성에 직접적 영향을 미칠 수 있다.   
$$
\sigma'(x) = \sigma(x) \cdot (1 - \sigma(x))
$$   
$$
\sigma''(x) = \sigma(x) \cdot (1 - \sigma(x)) \cdot (1 - 2 \sigma(x))
$$   
$$
H_{ii} = \frac{\partial^2 L}{\partial w_i^2} = \sum_j \frac{\partial^2 L}{\partial a_j^2} \cdot \left(\frac{\partial^2 a_j}{\partial w_i^2}\right)
$$   
Hessian 행렬은 함수의 2차 미분을 나타내며, 함수의 곡률(함수의 기울기 벡터가 변화하는 속도)을 나타내어 1차 미분만을 사용하는 경사 하강법에서 나아가 Newton's Method, Quasi-Newton Methods 등의 더 정교한 업데이트가 가능하도록 한다.    
$$
\theta^{t+1} = \theta^t - \eta \nabla L(\theta^t)
$$   

### Xavier Initialization        

$i$번째 layer의 activation function($f$)의 입력(argument vector)은 $s^i = z^i W^i + b^i$ 이고, activation vector는 $z^{i+1} = f(s^i)$ 이다.    

$$
\frac{\partial \text{Cost}}{\partial s_k^i} = f'(s_k^i) W_{k, \cdot}^{i+1} \frac{\partial \text{Cost}}{\partial s^{i+1}} \tag{1}
$$    

$\text{Cost}i$에 대한 $s_k^i$의 기울기는 chain rule에 의해 $\frac{\partial \text{Cost}}{\partial z^{i+1}} = \frac{\partial \text{Cost}}{\partial s_k^i} \cdot \frac{\partial s_k^i}{\partial z^{i+1}}$ 이고, $z^{i+1} = f(s^i)$, $\frac{\partial z^{i+1}}{\partial s_k^i} = f'(s_k^i)$이다.   



$$
\frac{\partial \text{Cost}}{\partial w_{l,k}^i} = z_l^i \frac{\partial \text{Cost}}{\partial s_k^i} \tag{2}
$$    

$\text{Cost}i$에 대한 $W_{l,k}^i$의 기울기는 chain rule에 의해 $\frac{\partial W_{l,k}^i}{\partial \text{Cost}} = \frac{\partial s_{k}^i}{\partial \text{Cost}} \cdot \frac{\partial W_{l,k}^i}{\partial s_{k}^i}$ 이고, $\frac{\partial W_{l,k}^i}{\partial s_{k}^i} = z_{l}^i$이다.   


Initialization 때 linear 영역에 있고 weights가 독립적으로 초기화되어 inputs features 분산이 동일하다고 가정하면, activation function의 도함수는 $f'(s_k^i)\approx1$이고, $i$번째 layer의 크기 $n_i$와 network input x에 대해서 $\displaystyle \text{Var}[z^i] = \text{Var}[x] \prod_{i' = 0}^{i-1} n_{i'} \text{Var}[W^{i'}]$ 이다.    
원소들이 독립적이고 평균이 0일 때 Covariance를 사용하여 $\text{Var}[s^i] = W \text{Var}[z^i] W^T$를 일반화하여 activation variance가 위와 같이 표현된다. $\text{Var}[W^{i'}]$는 layer $i'$에서의 모든 weights의 shared scalar variance이다.   


$$
\text{Var}[ \frac{\partial \text{Cost}}{\partial s^i}] = \text{Var}\left( \frac{\partial \text{Cost}}{\partial s^d} \right) \prod_{i' = i}^{d} n_{i'}\text{Var}[W^{i'}] \tag{3}
$$   

$$
\text{Var}[\frac{\partial \text{Cost}}{\partial w^i} ] = \prod_{i' = 0}^{i-1} n_{i'}\text{Var}[W^{i'}]\prod_{i' = 0}^{d-1} n_{i'+1}\text{Var}[W^{i'}]\times \text{Var}[x]\text{Var}[x] \frac{\partial \text{Cost}}{\partial s^d} \tag{4} 
$$   

**Forward-propagation**    

$$
\forall (i, i'), \text{Var}[z^i] = \text{Var}[z^{i'}] \to \forall i, n_i\text{Var}[W^i] = 1 \tag{5}
$$     

network를 통과할 때 activation의 variance가 일정하면 information이 잘 유지되어 일관되게 전파될 수 있다.   

**Back-propagation**   

$$
\forall (i, i'), \text{Var}[ \frac{\partial \text{Cost}}{\partial s^i}] = \text{Var}[ \frac{\partial \text{Cost}}{\partial s^{i'}}]  \to \forall i, n_{i+1}\text{Var}[W^i] = 1 \tag{6}
$$     

vanishing gradient 문제를 방지하고 network가 안정적으로 학습되도록 하기 위하여 cost function의 gradient variance가 동일해야 한다.   

<p align="center">
*위의 두 제약 조건을 만족시키기 위해 아래와 같이 나타낼 수 있다. 모든 layer가 동일한 width를 가지면, 두 제약 조건을 만족한다.*    
</p>   

$$
\forall i, \text{Var}[W^i] = \frac{2}{n_i + n_{i+1}} \tag{7}
$$    

만약, weights에 대한 동일한 initialization을 가지면, 아래의 성질을 갖는다.    

$$\forall i, \; \text{Var} [ \frac{\partial \text{Cost}}{\partial s^i}] = [n\text{Var}[W]]^{d-i} \text{Var}[x] \tag{8}
$$   

$$
\forall i, \; \text{Var} [ \frac{\partial \text{Cost}}{\partial w^i}] = [n\text{Var}[W]]^d \text{Var}[x] \text{Var} [ \frac{\partial \text{Cost}}{\partial s^d}] \tag{9}
$$    

*weight에 대한 gradient의 variance는 모든 layer에서 동일하나, 더 깊은 network에서 back-propagate된 gradient의 variance는 vanish/explode될 수 있다.*   

$$
n\text{Var}[W] = \frac{1}{3} \text{ where } n \text{ is the layer size} \tag{10}
$$   

*이는 standard initialization에서의 variance로, back-propagated gradient의 variance가 layer에 따라 달라(감소)진다.(*n: layer의 size)*      

$$
W \sim U \left[ -\frac{\sqrt 6}{\sqrt {n_j + n_{j+1}}}, \frac{\sqrt 6}{\sqrt{n_j + n_{j+1}}} \right] \tag{11}
$$   

*layer를 통한 multiplicative effect로 인하여 deep network를 초기화할 때 normalization factor는 중요하다.   
본 논문에서는 network의 위 아래로 이동하며 activation variances와 back-propagated gradients variance를 대략적으로 유지하고자 다음의 normalized initialization을 제안한다.*     

### Conclusion    
- Normalized Initialization : 학습 중 activation과 gradient의 variance를 안정적으로 유지하여 성능 향상에 기여한다.    
- Sigmoid는 작은 random Weight으로 초기화 시, learning dynamics가 좋지 않고 top hidden layer에서의 초기 포화도가 높아진다.      
- activations과 gradients가 잘 흐르도록 layer 간 transformation을 잘 유지하면(Jacobian이 대략 1 정도) supervised deep networks와 pre-trained with unsupervised learning networks 간의 불일치를 상당 부분 제거할 수 있다.   


## He(2015)     

**문제**: 깊은 CNNs는 대부분 Gaussian 분포에서 추출한 random weights로 초기화되어, 고정된 표준 편차로 매우 깊은 모델(ex. 8개 이상의 Conv Layer)은 수렴에 어려움이 있다.   
**기존 방법의 문제**: Glorot와 Bengio(Xavier 초기화)는 적절히 조정된 균일 분포로 초기화하는 것을 제안했으나, 이는 linear activation란 가정에 기반하기에 ReLU나 PReLU에는 유효하지 않다.    

**찐 문제**: 하지만 Rectifier Network 또한 초기화가 잘못되면 Non-Linear System의 학습을 방해할 수 있다.   

### Abstract   
Delving Deep into Rectifiers: Surpassing Human-Level Performance on ImageNet Classification 논문에서는 2가지 방법을 제안하는데 여기서는 두번째 Initialization 방법만 살펴본다.   
1. 전통적인 Rectifier Unit을 일반화한 Parametric Rectifier Linear Unit(PReLU)를 제안한다.   
  - 모델 적합성을 개선하고, 추가적 계산 비용과 Overfitting의 위험 거의 없이 구현 가능함.   
2. Rectifier Non-linearities를 고려한 Initialization 방법을 제안한다.   
  - 매우 깊은 Rectifier 모델을 처음부터 직접 학습하고 더 깊고 넓은 아키텍처 탐색을 가능하도록 함.   

### Forward Propagtion Case    

Conv Layer에 대한 response는 $y_l = W_l x_l + b_l$ 이다.    

$$\text{Var}[y_l] = n_l \text{Var}[W_l x_l] \tag{1}$$     

$W_l$의 초기화된 요소들이 서로 독립적이며 같은 분포를 공유하고 $x_l$과 $W_l$이 서로 독립이라 가정하면 $\text{Var}[y_l]$은 위와 같다.       

$$\text{Var}[y_l] = n_l \text{Var}[W_l] E[x_l^2] \tag{2}$$    

또한, $w_l$이 zero-mean을 갖는다고 하여 독립 변수의 곱의 variance를 얻는다. ReLU activation function의 경우, $x_l = \max(0, y_{l-1})$이며, 따라서 평균이 0이 아니므로 $\mathbb{E}[x_l^2] \neq \text{Var}[x_l]$이다.      

$$
\text{Var}[y_l] =  \displaystyle \frac{1}{2} n_l \text{Var}[W_l] \text{Var}[y_{l-1}]   \tag{3} 
$$    

$w_{l-1}$이 zero-mean인 대칭 분포를 갖고 $b_{l-1}=0$인 경우, $y_{l-1}$은 zero-mean인 대칭 분포를 갖는다. 따라서, ReLU일 때 $E[x_l^2]=\frac{1}{2}Var[y_{l-1}]이므로 (3)과 같고, L개의 layer를 모두 합치면 (4)가 된다.   

$$\text{Var}[y_L] = \text{Var}[y_1] \left( \displaystyle \prod_{l=2}^L \frac{1}{2} n_l \text{Var}[W_l] \right) \tag{4}$$    

위의 곱이 적절한 scalar(ex. 1)를 취하여 입력 신호의 크기를 지수적으로 줄이거나 확대하지 않도록 하는 조건은 아래와 같다.   

$$\frac{1}{2} n_l \text{Var}[W_l] = 1, \forall l \tag{5}$$    

이는 zero-mean인 Gaussian 분포를 이끌어, std는 $\sqrt{\frac{2}{n_i}}$이며 $b=0$으로 초기화한다. 첫번째 layer는 ReLU가 입력 신호에 적용되지 않기 때문에 $n_1Var[w_1]=1$이어야 하나, $\frac{1}{2}$의 계수는 단일 layer에서만 존재하면 문제가 되지 않기 때문에 간단함을 위해 (5)를 적용한다.      



### Backward Propagtion Case   

$$
 \displaystyle \Delta x_l = \hat{W}_l \Delta y_l    \tag{6}
$$    

$$
 \displaystyle \text{Var}[\Delta x_l] = \hat{n}_l \text{Var}[\hat{W}_l] \text{Var}[\Delta y_l]\\    
= \displaystyle  \frac{1}{2} \hat{n}_l \text{Var}[\hat{W}_l] \text{Var}[\Delta x_{l+1}]    \tag{7}
$$    

$$
 \displaystyle \text{Var}[\Delta x_2] = \text{Var}[\Delta x_{L+1}] \left(\prod_{l=2}^L \frac{1}{2} \hat{n}_l \text{Var}[\hat{W}_l]\right)    \tag{8}
$$    

$$
 \displaystyle \frac{1}{2} \hat{n}_l \text{Var}[\hat{W}_l] = 1, \forall l    \tag{9}
$$    


### Conclusion
- Xavier와 비교하여 명확한 정확도 우위를 관찰하지 못하였으나, He의 경우 오류를 보다 더 빨리 줄이는 것을 확인하였다.   
  - Xavier은 Linear한 경우만 고려한 결과 $n_lVar[w_l]=1$로 std는 $\sqrt{\frac{1}{n_l}}$이다. 즉, L개의 layer가 있을 때의 std가 He std의 $\frac{1}{\sqrt{2^L}}$이므로 실제 사용된 모델의 수렴을 정지시키기에 충분히 작지 않다.   
- 매우 깊은 모델(30-layer)에서 비교 시, Xavier은 학습을 완전히 정지시키고 gradient는 감소한 반면, He는 모델의 수렴을 보여주었다.   
- 근데 또 ImageNet 실험에서 30-layer 모델의 경우 top-1/top-5 오류가 38.56/16.59로, 표 2의 14-레이어 모델(33.82/13.34)보다 나쁘고, 작은 모델, VGG의 대형 모델, 음성 인식 연구에서도 정확도 포화나 저하가 관찰되었다고 한다...    

...?   


## Orthogonal(2013)   

**문제**: input-output map의 Linearity에도 불구하고, 깊은 Linear NN은 새로운 hidden layer가 추가될 때 마다 weight에 대한 nonlinear gradient descent dynamics를 보인다.      

"Deep Learning의 시간 척도는 어떻게 결정되는가?"   
"깊이가 증가함에 따라 훈련 속도는 어떻게 느려지는가?"   
"Greedy Unsupervised Pretraining이 학습 속도를 어떻게 가속화 할 수 있는가?"   
"학습된 내부 표현은 훈련 데이터에 내재된 통계적 규칙성에 어떻게 의존하는가?"   

  
### Abstract
Exact solutions to the nonlinear dynamics of learning in deep linear neural networks 논문에서는 깊은 선형 신경망의 학습 역학을 분석하여, 네트워크의 깊이에 상관없이 유한한 학습 속도를 유지할 수 있는 initial condition을 제시하고, non-linear network에서도 신뢰할 수 있는 gradient 전파를 가능하게 하는 새로운 초기화 방법을 제안한다.    
- **학습의 비선형 현상**: 깊은 선형 네트워크는 비선형 네트워크에서 관찰되는 장기적인 정체 구간과 신속한 오류 감소를 포함하는 비선형 학습 현상을 보인다.   
  - 이러한 현상은 비선형 네트워크의 시뮬레이션에서 관찰되는 현상과 유사하며, 이는 깊은 선형 네트워크에서도 발생할 수 있음을 보임   
- **초기화의 중요성**: 이론적 분석은 초기 가중치의 특정 클래스가 깊이에 독립적인 학습 속도를 제공하며, 이는 무작위 Gaussian 초기화와는 다른 성질을 가진다.   
  - 또한, 이러한 초기 조건은 깊이와 상관없이 일정한 학습 속도를 보장하며, 이는 실제 비선형 네트워크에서도 gradient의 정확한 전파를 지원    
- **학습 속도의 유한성**: 네트워크의 깊이가 무한대에 가까워질 때, 특정 초기 조건 하에서 학습 속도가 여전히 유한하게 유지될 수 있음을 보여준다.   
  - 이러한 조건은 특히 unsupervised pretraining을 통해 발견될 수 있으며, 이는 깊은 네트워크에서도 효율적인 학습을 가능하게 함    

### Learning Dynamics on Weight Space

### Optimization of Layer-Wise Pretraining

### Random Orthogonal Initial Condition

### Conclusion


## Weight Uncertainty(2015)   

## ALL YOU NEED IS A GOOD INIT(2015)   
  



## Reference
blog :     

paper : 
- [Understanding the difficulty of training deep feedforward neural networks](https://www.semanticscholar.org/paper/Understanding-the-difficulty-of-training-deep-Glorot-Bengio/ea9d2a2b4ce11aaf85136840c65f3bc9c03ab649)   
- [Delving Deep into Rectifiers: Surpassing Human-Level Performance on ImageNet Classification](https://arxiv.org/abs/1502.01852)    
- [Exact solutions to the nonlinear dynamics of learning in deep linear neural networks](https://arxiv.org/abs/1312.6120)   
- [Weight Uncertainty in Neural Networks](https://arxiv.org/abs/1505.05424)   
- [ALL YOU NEED IS A GOOD INIT](https://arxiv.org/abs/1511.06422)   


