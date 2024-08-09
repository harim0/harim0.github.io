---
title: "[선형대수학] 기본 개념 정리"
categories:
  - linear_algebra
tags:
  - linear_algebra
toc: true
toc_sticky: true
toc_label: "선형대수학 정리"
date: 2024-08-09 17:30:00 +0900
author_profile: false
header:
  overlay_image: # assets/images/pages/2024-07-20.png
  overlay_filter: 0.5 
  teaser: # assets/images/pages/2024-07-20.png
use_math: true
# published: false
---   
 
## 1 Vector, Linear Combination, Span, Linearly Dependent, Linearly Independent, Basis 
### Vector(벡터)
1) 물리학자 : 길이와 방향을 갖는 공간 상의 화살표   
2) 컴퓨터공학자 : 숫자 data의 배열   
3) 수학자 : 덧셈과 상수배   
![image](/assets/images/pages/vector.jpg){: width="300" height="300"}    

### Vector Space(벡터공간)
정의 : 집합 $\mathbb{R}^n = \Set{(x_1,x_2,...,x_n)|x_i \in R}$에서 덧셈, 스칼라 곱 연산이 주어지는 경우 $R^n$을 벡터 공간이라 한다.   
- 부분공간은 첫째로 $\forall x,y \in W : x+y \in W$, 둘째로 $x \in W : \forall \lambda \in R : \lambda_x \in W$를 만족하는 $W(\not = \varnothing) \in \mathbb{R}^n$이다.   
  - $\mathbb{R}^2 \to W=\Set{(0,0)\text{ 과 원점 지나는 직선, }R^2}$   
  - $\mathbb{R}^3 \to W=\Set{(0,0,0)\text{ 과 원점 지나는 평면, 원점 지나는 직선, }R^3}$   

### Linear Algebra(선형대수학)   
직선은 기하학적 의미를 지닌 동시에 대수적 구조를 갖는다.    
**선형대수**는 **유클리드 기하학에서 다루는 직선, 평면들의 관계를 대수적으로 계산할 수 있다**는 의미를 담는다.   

### Linear Combination(선형결합) 
정의 : $x_1,...,x_m \in \mathbb{R}^n, \lambda_1, ...,\lambda_m \in \mathbb{R}$이라고 하였을 때, 
$\lambda_1x_1+...+\lambda_m x_m$을 **Linear Combination**이라 한다.

![image](/assets/images/pages/vector0.jpg){: width="300" height="300"}    
선형결합은 벡터계산의 평행선 법칙을 대수화 한 것이다.

벡터는 scale된 두 벡터의 합으로 표현할 수 있다.   
스칼라를 다르게 하여 모든 2차원 벡터를 만들 수 있다.    

### Span(생성)   
정의 : 주어진 $m$개의 벡터 $S=\Set{x_1,...,x_m} \subset \mathbb{R}^n$에 대하여, 임의의 m개의 실수 $\lambda_1,...,\lambda_m \in \mathbb{R}$와 모든 선형결합을   
$Span(S)=\Set{\lambda_1 x_1,...,\lambda_m x_m|\lambda_1,...,\lambda_m \in \mathbb{R}}$이라고 하면, $Span(S)$는 $\mathbb{R}^n$의 부분공간이다.   

벡터 $\vec{v}$와 $\vec{w}$의 **"span"**은 모든 Linear Combination의 집합이다.   
즉, 각자 scale하여 더했을 때 얻을 수 있는 모든 가능한 벡터의 집합이다.   

$a\vec{v}+b\vec{w}$   

대부분의 2차원 벡터 쌍의 span은 2차원 공간의 벡터 전체가 된다.   

### Linearly Dependent(선형종속)   
1. 벡터 $\vec{v}, \vec{w}, \vec{u}$에 대해  $a\vec{v}+b\vec{w}+c\vec{u}=\vec{0}$에 0이외의 다른 해가 존재하면, 선형종속이다.   
2. 모든 스칼라 $a,b$에 대해 $\vec{u} = a\vec{v}+b\vec{w}$이면 선형종속이다.     

벡터들 중 span의 축소 없이 하나를 제거해도 되는 경우.   

### Linearly Independent(선형독립)   
1. 벡터 $\vec{v}, \vec{w}, \vec{u}$에 대해  $a\vec{v}+b\vec{w}+c\vec{u}=\vec{0}$의 유일한 해가 $a=b=c=0$이라면, 선형독립이다.   
2. 모든 스칼라 $a,b$에 대해 $\vec{u} \not = a\vec{v}+b\vec{w}$이면 선형독립이다.   
  
벡터 모두가 각자 span에 다른 차원을 구성하는 경우.   

ex) 3개의 벡터가 있을 때, 세번째 벡터가 두 벡터의 span 위에 놓여 있지 않은 경우 별개의 방향을 가리키기 때문에 모든 가능한 3차원 벡터에 접근할 수 있다.   

### Basis(기저)  
정의 : 주어진 n개의 벡터 $S=\Set{x_1,...,x_m} \subset R^n$에 대하여, 다음을 만족할 때 $R^n$의 기저라 한다.   
1. $\mathbb{R}^n=Span(S)$   
2. $n$개의 벡터 $x_1,...,x_m $가 선형독립이다.   
3. $S=\Set{x_1,...,x_m} \subset \mathbb{R}^n, m \le n$라 하고, m개의 벡터 $x_1,...,x_m$가 선형독립일 때 벡터공간 $Span(S)$의 차원은 $dim Span(S)=m$이다.    

기저는 기준이 되는 좌표계를 설정하는 것이다.    
- Standard Basis (표준기저): $ \text{벡터공간 }\mathbb{R}^n = \Set{(x_1, \dots, x_n) \mid x_i \in \mathbb{R}} \text{ 의 원소 } e_1 = (1, 0, \dots, 0), \, e_2 = (0, 1, \dots, 0), \dots, e_n = (0, \dots, 0, 1)$
 

## 2 Linear Transformation, Determinant, Inverse Matrix, Column Space, Null Space
### Linear Transformation(선형변환)   
- Linear(선형)
  - 모든 직선은 휘지 않고 직선인 상태를 유지한다. 즉, 격자선이 평행하고 균등 간격을 가져야 한다.   
  - 원점은 제자리에 고정되어야 한다.   
- Transformation(변환) : 함수를 의미하며, 입출력 관계의 특정 시각화 방식을 내포한다.   

> **벡터공간에서 선형변환의 조건(선형성의 속성)**
1. Additivity(덧셈의 보존) : $T(v+w)=T(v)+T(w)$   
2. Scalar Multiplication(스칼라 곱의 보존) : $T(cv)=cT(v)$       
격자선이 평행하고 균등 간격을 가져야 하는 이유는 선형성을 유지하기 위해서(즉, 덧셈의 보존과 스칼라 곱의 보존이 유지)이다. 또한, 선형변환의 기본 성질 $T(0)=0$을 만족시키려면 원점이 고정되어야 한다.   

  $$\vec{v} = -1\hat{i}+2\hat{j}$$   
  $$\text{변환된 }\vec{v} = -1(\text{변환된 }\hat{i})+2(\text{변환된 }\hat{j})$$   

- matrix : 선형변환을 설명하는 정보를 묶어 표현하는 방법.   

회전 후 전단(두번의 움직임) &rarr; 한번의 동작   
  $$\begin{bmatrix}
    1 & 1 \\
    0 & 1
  \end{bmatrix} \begin{pmatrix}\begin{bmatrix}
    0 & -1 \\
    1 & 0
  \end{bmatrix}
  \begin{bmatrix}
    x \\
    y
  \end{bmatrix}\end{pmatrix} = 
  \begin{bmatrix}
    1 & -1 \\
    1 & 0
  \end{bmatrix}
  \begin{bmatrix}
    x \\
    y
  \end{bmatrix}$$    
**행렬의 곱셈 = 두 변환의 순차적 적용 !**   

### Determinant(행렬식)  
선형변환으로 인해 어떤 scale 인자 만큼 넓이에 변화가 있을 때, 그 인자를 determinant(행렬식) of transformation이라 한다.   
![image](/assets/images/pages/determinant.jpg){: width="800" height="800"}    

- $det(A) \not = 0$ : 넓이 0으로 찌그러지지 않는 경우로, v에 도달하는 단 하나의 벡터가 존재하므로 $A^{-1}$ 존재.   
- $det(A) = 0$ : 방정식계와 연관된 변환이 공간을 하위차원으로 찌그러뜨리는 경우로, $A^{-1}$ 존재 X.   

### Linear System of Equations(연립선형방정식)  
기하학적 해석 : matrix $A$는 어떠한 선형변환에 대응되기 때문에 $Ax=v$를 푸는 것은 변환 후 $v$가 되는 벡터 $x$를 구하는 것   

"서로 복잡하게 얽여 있는 많은 변수를 구하는 방법에 대한 아이디어를 공간 변형 후 특정 벡터에 도달하는 벡터를 찾는 것으로 축소"   

### Inverse Matrix(역행렬)  

### Rank
변환 후 출력의 차원 수 = 열공간의 차원 수   
- 변환 후 출력이 직선, 1차원인 경우 rank = 1   
- 모든 벡터가 어떤 2차원 평면 위에 있다면 rank = 2   
- 3차원 변환이 0 아닌 행렬식을 갖고 출력이 3차원 전체를 생성할 수 있다면 rank = 3     

### Column Space(열공간)  
가능한 모든 출력의 집합 = 열들의 span

### Null Space(영공간)  
Kernel = 원점에 도달하는 벡터의 집합 = 0벡터에 도달하는 모든 벡터의 공간   

선형연립방정식의 경우, v가 $$\begin{bmatrix} 0 \\ 0 \end{bmatrix}$$인 경우로 방정식의 가능한 모든 해가 된다.   

## 3 Inner Products, Duality, Outer Products, Crammer's Rule

## 4 Change of Basis, EigenVectors, EigenValues, Gram-Schmidt 

### EigenVectors(고유벡터), EigenValues(고유값) 
정의 : 하나의 $nxn$ 행렬 $A: R^n \to R^n$을 선형변환이라 할 때, 0이 아닌 벡터 $v \in R^n$이 $A(v) = \lambda v$를 만족한다. $\lambda$를 행렬 $A$의 고유값이라 하고, $v$를 고유벡터라 한다.   

### Gram-Schmidt 직교화 과정

## 5 Abstract Vector Spaces



## Reference

youtube : 
- Essence of linear algebra(3Blue1Brown) (https://www.youtube.com/watch?v=v8VSDg_WQlA&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab&index=8)    
book : 
- 최적화 이론(임정환) 6장   

