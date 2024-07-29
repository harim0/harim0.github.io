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

Weight Agnostic Neural Networks 논문에서는 균일 랜덤 분포에서 샘플링된 single shared weight 파라미터로 연결을 채워 성능을 측정하여, 명시적 weight training 없이도 강화학습 tasks를 수행 가능한 최소한의 Neural Network Architecture를 찾을 수 있음을 시사한다.   
> "How important are the weight parameters of a neural network compared to its architecture?"   

1. 모든 네트워크 연결에 single shared weight parameter를 할당하고,   
2. 그 single weight parameter의 넓은 범위에서 네트워크를 평가함으로써   

weights의 중요성을 강조하여 inductive biases가 강한 neural network architectures를 찾는다.    

> 자체적으로 solutions를 인코딩하는 architectures를 만들기 위해서 weights의 중요성은 최소화되어야 한다. &larr; 최적의 weight values로 네트워크 성능을 판단하기 보다는, 랜덤 분포에서 도출한 weight values로 네트워크 성능을 판단한다.       


# Summary   
NAS 기술의 목표는 사람이 디자인한 것 보다 성능이 뛰어난 아키텍처를 만드는 것이다.   


## 4. Reference
blog :     

paper : 
- [Weight Agnostic Neural Networks](https://arxiv.org/abs/1906.04358)

