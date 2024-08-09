---
title: "Information & Learning Lecture 1 Review"
categories:
  - lectures
tags:
  - lectures
toc: true
toc_sticky: true
toc_label: "Lecture Review"
date: 2024-07-30 17:30:00 +0900
author_profile: false
header:
  overlay_image: # assets/images/pages/2024-07-20.png
  overlay_filter: 0.5 
  teaser: # assets/images/pages/2024-07-20.png
use_math: true
# published: false
---
단기 특강 빠르게 정리 !    
 
## 1 Information Theory 기초
최대한 많은 데이터를 매체에 저장하거나 채널을 통해 통신하기 위해 데이터를 정량화하는 응용 수학의 한 분야로, 수학적 모델은 크게 소스 코딩 이론, 채널 코딩 이론, 부호율-변형 이론 3가지가 있다.    

### Entropy 란?   
random event에 대해서, information quantity를 Entropy라 부른다.   

**"How can we measure the uncertainty mathematically?"**   
information entropy가 커질수록 uncertainty가 커진다.   

- Hartley Measure    
: 가능한 사건의 수만을 고려   
$$H = \log_b (\# of Possibilities)$$    
- Shannon's Measure   
: 사건의 확률분포 고려
X가 PMF $P_X$와 함께 RV라 한다.   
$$H(X)\equiv E[-\log_b P_x(X)] \\ = \sum_{a \in supp(P_X)} -P_X(a)\log_b P_X(X)$$   
(* UNIT : b = 2 -> bits, b = e -> nats)   
- Rényi Entropy   
$$\displaystyle H_\alpha(X) = \frac{1 - \alpha}{\alpha} \log \left( \sum_i P(x_i)^\alpha \right)$$   

- 성질 : $0\le H(X) \le \log_2 L$   

*증명 생략   

### Joint Entropy
$$
H(X,Y) = E[- \log_2 P_XY(X,Y)] \\
= \displaystyle \sum_{[b.c] \in supp(P_XY)} -P_XY(b, c) \log_2 P_{XY}(b,c)
$$   

### Conditional Entropy
$$
\displaystyle H(X|Y=b) = \sum_{a \in supp(P_{X|Y}(\cdot|b))} -P_XY(a|b) \log_2 P_{X|Y}(a|b)
$$   
- 성질 
  - $ H(X|Y) = H(X, Y) - H(Y) $    
  - $ I(X; Y) = H(Y) - H(Y|X) $    
  - $ I(X; Y) = H(X) + H(Y) - H(X, Y) $   
  - $ I(X; Y) = I(Y; X) $   
  - $  I(X; X) = H(X) $   
  - $  0 \leq I(X; Y) \leq \min(H(X), H(Y)) $   

*증명 생략   

### Relative Entropy   
Informational Divergence or Kullback-Leibler Distance   
$$
D(P_X||P_Y) = \displaystyle \sum_{a \in supp(P_X)} P_X(a) \log_2 \frac{P_X(a)}{P_Y(a)}\\
= E[\log_2 \frac{P_X(X)}{P_Y(X)}]
$$   

*증명 생략   

### Mutual Information   
두 확률 변수 사이의 상호 의존성   
하나의 RV가 다른 RV에 대해 갖고 있는 정보의 양   
$$I(X;Y) = D(P_{XY}||P_XP_Y) $$   
- 성질 : $I(X;Y) \ge 0$   

### Conditional Mutual Information
$$I(X; Y|Z) = H(X|Z) - H(X|YZ)$$   

### Data Processing Inequality
"system"을 source $P_X$ ---$X$---> channel $P_{Y|X}$ ---$Y$---> channel $P_{X|Y}$---> $Z$ 라고 하자.   
만약 X-Y-Z가 Markov chain을 형성한다면,   
$$I(X; Z) \leq I(X; Y)$$   
$$I(Y; Z) \leq I(X; Y)$$   

*증명 생략   

### Fano's Inequality   
"system"을 ---$X$---> system $P_{\hat{X}|X}$ ---$\hat{X}$---> 라고 하자.   
Error Prob : $P_e = Pr[X \ne \hat{X}]$   
$$H(X|\hat{X}) \le H_2(P_e)+P_e\log_2(|\chi|-1)$$   

만약 $\hat{X}$가 X-Y-$\hat{X}$ 의 estimator이고 $P_e = Pr[X \ne \hat{X}]$ 라면,   
$$H(X|Y) \le H(X|\hat{X}) \le H_2(P_e)+P_e\log_2(|\chi|-1)$$    
즉, Data-processing inequality.   

*증명 생략   

### Asymptotic Equipartition Property (AEP)
$$|- \frac{1}{n} \log_b P_X(X^n) - H(X)| < \epsilon$$     
1. $2^{n [H(X) - \epsilon]} < P_X(x^n) < 2^{n [H(X) + \epsilon]}$    
2. $\Pr(x^n \in \mathcal{A}_\epsilon^{(n)}) \geq 1 - \epsilon$    
3. $1 - \epsilon < \frac{|\mathcal{A}_\epsilon^{(n)}|}{2^n H(X)} < 1 + \epsilon $    

### Data Compression
확률 변수 M은 $X^n$에 의존한다. (block-to-variable length encoder)    
rate : $\frac{E[M]}{n}$   
$$\frac{E[M]}{n}=H(X)+\epsilon \text{  for any }\epsilon > 0$$   
- Source Coding Theorem : 

### Channel Capacity   
- Uniformly Dispersive Channels   
- Uniformly Focusing Channels   
- Symmetric Channels   
$$
C = \displaystyle \max_{P_{X}} I(X; Y) \leq \max_{P_{X}} H(X) \leq \log_2 J$$    
$$
\displaystyle C \leq \max_{P_{X}} H(Y) \leq \log_2 K
$$        
- Channel Coding Theorem : $ C= \displaystyle \max_{P_X(\cdot)} I(X;Y)$   

*증명 생략   

---

- Channel Capacity 성질
  $C \triangleq \max_{p_X} I(X; Y)$ 라고 할 때,   
  - $ C \geq 0  \text{ since } I(X; Y) \geq 0  $   
  - $ C \leq \log |\mathcal{X}| \text{ since } 
    C = \displaystyle \max_{p(x)} I(X; Y) \leq \max_{p(x)} H(X) = \log |\mathcal{X}|
    $     
  - $ 𝐼(𝑋; 𝑌)\text{ is a continuous function of }𝑝(𝑥). $    
  - $ 𝐼(𝑋; 𝑌)\text{ is a concave function of }𝑝(𝑥). $   

- Communication channel (𝒳, 𝑝(𝑦|𝑥) , 𝒴)   
- Jointly typical sequences   
- Error 가 정말로 작은가?   
- Source-Channel Separation Theorem   

### Differential Entropy

### Gaussian Channel

### Rate Distortion Theorem

### Network Information Theory



--- 

## 2 Graph Learning 기초

### Graph Convolutional Network

### Graph Filtering (Graph Signal Processing)    

--- 

### Graph Matching

### Graph Matching & Clustering




기초 중 기초인데도 너무 어렵다ㅜㅜㅜ   

## Reference
lecture : 정보 및 학습이론 단기강좌     

web : 
- 위키피디아 (https://ko.wikipedia.org/wiki/%EC%A0%95%EB%B3%B4_%EC%9D%B4%EB%A1%A0)    
- 블로그 (https://gem763.github.io/machine%20learning/%EC%A0%95%EB%B3%B4%EC%9D%B4%EB%A1%A0%EC%9D%98-%EA%B8%B0%EC%B4%88.html)   
paper : 
- []()
- 

