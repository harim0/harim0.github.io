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

## "How important are the weight parameters of a neural network compared to its architecture?"

Weight Agnostic Neural Networks 논문에서는 weight training 없이도 강화학습 tasks를 수행 가능한 최소한의 Neural Network Architecture를 찾을 수 있음을 보인다.     

1. 모든 네트워크 연결에 균일 랜덤 분포에서 샘플링된 single shared weight parameter를 할당하고,   
2. 그 single weight parameter의 광범위한 범위에서 네트워크를 평가함으로써   

weights의 중요성을 강조하지 않는 inductive biases가 강한 neural network architectures를 찾는다.    
(Network Topology : 신경망 구조와 연결 방식으로 layer 수, layer type, node 수, 연결 패턴, activation function 등이 포함된다. )   

![image](/assets/images/pages/2024-07-29.png){: width="600" height="600"}    
> **WANN's 4 Step**    
1) 최소 신경망 topology의 초기 모집단 생성   
2) 각 네트워크는 여러 rollout에 걸쳐 평가되고, 각 rollout마다 다른 single shared weight이 할당되고 평가 기간 동안의 누적 reward가 기록됨   
3) performance와 complexity에 따라 네트워크 순위 매김    
4) 확률적(토너먼트 selection)으로 골라진 최고 순위 네트워크 topology를 무작위로 변경하여 새로운 모집단 구성   
step 2부터 반복하여 generation을 거듭할수록 performance가 향상되고, complexity가 커지는 weight agnostic topology를 생성한다.   



## Weight Initialization   
### Xavier


### He    
Xavier 초기화는 linear activation란 가정에 기반하여 ReLU나 PReLU에는 유효하지 않다.   

**Forward Propagtion Case**   
$y_l = W_l x_l + b_l$   
$$
\text{Var}[y_l] = n_l \text{Var}[W_l x_l]   
$$   
$$
\text{Var}[y_l] = n_l \text{Var}[W_l] E[x_l^2]   
$$   
$$
\text{Var}[y_l] =  \displaystyle \frac{1}{2} n_l \text{Var}[W_l] \text{Var}[y_{l-1}]   
$$   

$$\text{Var}[y_L] = \text{Var}[y_1] \left( \displaystyle \prod_{l=2}^L \frac{1}{2} n_l \text{Var}[W_l] \right)$$   
$$\frac{1}{2} n_l \text{Var}[W_l] = 1, \forall l$$   


**Backward Propagtion Case**   
$$
 \displaystyle \Delta x_l = \hat{W}_l \Delta y_l   
$$   
$$
 \displaystyle \text{Var}[\Delta x_l] = \hat{n}_l \text{Var}[\hat{W}_l] \text{Var}[\Delta y_l]\\    
= \displaystyle  \frac{1}{2} \hat{n}_l \text{Var}[\hat{W}_l] \text{Var}[\Delta x_{l+1}]   
$$   
$$
 \displaystyle \text{Var}[\Delta x_2] = \text{Var}[\Delta x_{L+1}] \left(\prod_{l=2}^L \frac{1}{2} \hat{n}_l \text{Var}[\hat{W}_l]\right)   
$$   
$$
 \displaystyle \frac{1}{2} \hat{n}_l \text{Var}[\hat{W}_l] = 1, \forall l   
$$   

### Orthogonal       
  



## Reference
blog :     

paper : 
- [Weight Agnostic Neural Networks](https://arxiv.org/abs/1906.04358)
- [Delving Deep into Rectifiers: Surpassing Human-Level Performance on ImageNet Classification](https://arxiv.org/abs/1502.01852)   
- 

