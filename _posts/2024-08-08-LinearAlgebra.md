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
 
## 1 Vector, Linear Combination, Span, Linearly Dependent, Linearly Independent, Basis, Change of Basis 
### Vector(벡터)
1) 물리학자 : 길이와 방향을 갖는 공간 상의 화살표   
2) 컴퓨터공학자 : 숫자 data의 배열   
3) 수학자 : 덧셈과 상수배   
![image](/assets/images/pages/vector.jpg){: width="300" height="300"}    

### Vector Space(벡터공간)
정의 : 집합 $\mathbb{R}^n = \Set{(x_1,x_2,\dots,x_n)|x_i \in R}$에서 덧셈, 스칼라 곱 연산이 주어지는 경우 $R^n$을 벡터 공간이라 한다.   
- 부분공간은 첫째로 $\forall x,y \in W : x+y \in W$, 둘째로 $x \in W : \forall \lambda \in R : \lambda_x \in W$를 만족하는 $W(\not = \varnothing) \in \mathbb{R}^n$이다.   
  - $\mathbb{R}^2 \to W=\Set{(0,0)\text{ 과 원점 지나는 직선, }R^2}$   
  - $\mathbb{R}^3 \to W=\Set{(0,0,0)\text{ 과 원점 지나는 평면, 원점 지나는 직선, }R^3}$   

### Linear Algebra(선형대수학)   
직선은 기하학적 의미를 지닌 동시에 대수적 구조를 갖는다.    
**선형대수**는 **유클리드 기하학에서 다루는 직선, 평면들의 관계를 대수적으로 계산할 수 있다**는 의미를 담는다.   

### Linear Combination(선형결합) 
정의 : $x_1,\dots,x_m \in \mathbb{R}^n, \lambda_1, \dots,\lambda_m \in \mathbb{R}$이라고 하였을 때, 
$\lambda_1x_1+\dots+\lambda_m x_m$을 **Linear Combination**이라 한다.

![image](/assets/images/pages/vector0.jpg){: width="300" height="300"}    
선형결합은 벡터계산의 평행선 법칙을 대수화 한 것이다.

벡터는 scale된 두 벡터의 합으로 표현할 수 있다.   
스칼라를 다르게 하여 모든 2차원 벡터를 만들 수 있다.    

### Span(생성)   
정의 : 주어진 $m$개의 벡터 $S=\Set{x_1,\dots,x_m} \subset \mathbb{R}^n$에 대하여, 임의의 m개의 실수 $\lambda_1,\dots,\lambda_m \in \mathbb{R}$와 모든 선형결합을   
$Span(S)=\Set{\lambda_1 x_1,\dots,\lambda_m x_m|\lambda_1,\dots,\lambda_m \in \mathbb{R}}$이라고 하면, $Span(S)$는 $\mathbb{R}^n$의 부분공간이다.   

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
정의 : 주어진 n개의 벡터 $S=\Set{x_1,\dots,x_m} \subset R^n$에 대하여, 다음을 만족할 때 $R^n$의 기저라 한다.   
1. $\mathbb{R}^n=Span(S)$   
2. $n$개의 벡터 $x_1,\dots,x_m $가 선형독립이다.   
3. $S=\Set{x_1,\dots,x_m} \subset \mathbb{R}^n, m \le n$라 하고, m개의 벡터 $x_1,\dots,x_m$가 선형독립일 때 벡터공간 $Span(S)$의 차원은 $dim Span(S)=m$이다.    

기저는 기준이 되는 좌표계를 설정하는 것이다.    
Standard Basis (표준기저): $$ \text{벡터공간 }\mathbb{R}^n = \Set{(x_1, \dots, x_n) \mid x_i \in \mathbb{R}} \text{ 의 원소 } e_1 = (1, 0, \dots, 0), \, e_2 = (0, 1, \dots, 0), \dots, e_n = (0, \dots, 0, 1)$$   

### Change of Basis   



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

하나의 $m\times n$ 행렬 $A$는 벡터공간 $\mathbb{R}^n$에서 $\mathbb{R}^m$으로의 함수이며, 두 선형법칙을 만족하는 $A$를 **선형변환**이라 한다.     

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
변환 후 출력의 차원 수 = 열공간의 차원 수 = 행렬이 갖는 선형독립인 열의 수 = 행렬이 갖는 선형독립인 행의 수    
- 변환 후 출력이 직선, 1차원인 경우 rank = 1   
- 모든 벡터가 어떤 2차원 평면 위에 있다면 rank = 2   
- 3차원 변환이 0 아닌 행렬식을 갖고 출력이 3차원 전체를 생성할 수 있다면 rank = 3     

행렬 $A$의 rank는 $A^T$의 rank와 같으므로, 열공간의 차원과 행공간의 차원과 같다.    

$m \times n$ 행렬의 rank = $min(m,n)$ &rarr; full rank   
$m \times n$ 행렬의 rank $\lt min(m,n)$ &rarr; rank-deficient   

### Column Space(열공간)  
$C(A)=range(A)$ = 가능한 모든 출력의 집합 = 열들이 span하는 벡터 공간 = 𝐴𝑥로 생성될 수 있는 모든 벡터들의 집합    

- 행렬의 Column Vector(열벡터)는 Basis(기저벡터)의 도착지이다.   

### Null Space(영공간)  
Kernel = 원점에 도달하는 벡터의 집합 = 0벡터에 도달하는 모든 벡터의 공간   
즉, 쉽게 말해 $A\mathbf{x}=0$을 만족하는 $x$의 집합    

선형연립방정식의 경우, $\mathbf{v}$가 $$\begin{bmatrix} 0 \\ 0 \end{bmatrix}$$인 경우로 방정식의 가능한 모든 해가 된다.   
- $m\times n$ 행렬 A에서 $dim(N(A))=n-r$로, $dim(N(A))+dim(R(A))=n$이다.   
- $A\mathbf{x}=0$는 $A$의 각 행들이 $\mathbf{x}$와 직교한다는 의미이므로, $\mathbf{x}$의 집합인 Null Space는 Row Space와 수직한 공간이다.    

cf) Left Null Space는 Column Space의 관점에서 바라본 것으로 $\mathbf{x}^T A = 0^T$애서 $dim(N_L(A))=m-r$, $dim(N_L(A))+dim(C(A))=n$이다.   

## 3 Inner Products, Duality, Outer Products, Crammer's Rule
### Inner Products(내적)  
내적은 Inner Product, Dot Product로 불린다. (실제로 Inner Product가 Dot Product보다는 더 포괄적 의미를 갖는다.)    
벡터공간 $\mathbb{R}^n=\Set{(x_1,x_2,\dots,x_n)|x_i \in R}$ 의 내적은 다음과 같이 정의된다.   

$<x,y> = x_1y_1+\dots +x_ny_n = \lVert x \rVert \lVert y \rVert \cos \theta$    

 $$<x,y>=\mathbf{x}\centerdot \mathbf{y}=\mathbf{x}^T \mathbf{y}=(x_1,x_2,\dots,x_n)\begin{pmatrix} 1 & 0 & \cdots & 0 \\ 0 & 1 & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & 1 \end{pmatrix} \begin{pmatrix} y_1 \\ y_2 \\ \vdots \\ y_n \end{pmatrix}$$   

두 벡터 사이의 각도와 크기를 고려한 연산으로 대칭성의 성질에 의해 순서는 상관없다.   


![image](/assets/images/pages/innerproduct.jpg){: width="700" height="700"}    

**내적의 의미**   
쉽게 말해서, 내적은 두 벡터가 얼마나 닯았는지를 나타낸다.    
위 그림에서 $\mathbf{v} \centerdot \mathbf{w}$는 $\lVert \mathbf{v} \rVert \lVert \mathbf{w} \rVert \cos \theta$로, v의 길이($\lVert \mathbf{v} \rVert$)와 w를 v에 정사영한 벡터의 길이($\lVert \mathbf{w} \rVert \cos \theta$) 곱이다.   
이는 좌표를 짝짓고 곱한 다음 합하는 내적의 수치적 과정과 Projection의 연관성을 보여준다.   
즉, **두 벡터를 내적하는 것**은 **두 벡터 중 하나를 변환 인자로 보는 것**과 동일하다.   

Matrix-Vector Space Product &rarr; Dot Product   
단위 벡터의 내적 = 벡터를 단위벡터로 투영한 길이   

**정사영 벡터 구하기**   
1) 위에서 $\mathbf{w}$가 사영된 $\mathbf{p}$의 길이($\lVert \mathbf{w} \rVert \cos \theta$)는 $\frac{\mathbf{v} \centerdot \mathbf{w}}{\lVert \mathbf{v} \rVert} = \frac{\mathbf{v}^T \mathbf{w}}{\sqrt{\mathbf{v}^T \mathbf{v}}}$이다.    
정사영된 벡터는 길이에 방향도 포함되어야 하므로 방향 성분을 나타내는 $\frac{\mathbf{v}}{\lVert \mathbf{v} \rVert}$를 곱해주면 다음과 같이 나타낼 수 있다.         

$$\mathbf{p} = \frac{\mathbf{w} \centerdot \mathbf{v}}{\mathbf{v}\centerdot \mathbf{v}}\mathbf{v}$$   

2) $\mathbf{p}$를 $\mathbf{v} \hat{\mathbf{x}}$로 두고 이에 직교하는 $\mathbf{w}-\mathbf{v}\hat{\mathbf{x}}$를 통해, $(\mathbf{w}-\mathbf{v}\hat{\mathbf{x}})^T \mathbf{v}\hat{\mathbf{x}} = 0$ 식에서 $\hat{\mathbf{x}} = \frac{\mathbf{v}^T\mathbf{w}}{\mathbf{v}^T\mathbf{v}}$를 도출할 수 있다.    
즉, $\mathbf{v}\hat{\mathbf{x}} = \frac{\mathbf{w} \centerdot \mathbf{v}}{\mathbf{v}\centerdot \mathbf{v}}\mathbf{v}$이다.      

**벡터 크기와 거리**   
norm(크기) : $ {\lVert v \rVert}_2 = \sqrt{<v,v>} = \sqrt{(x_1^2,\dots,x_n^2)}$    
위는 $l_2-norm$이고, 벡터의 크기를 나타내는 방법으로는 이외에도 $l_1-norm$, $infinity-norm$ 등이 있다.    

dist(거리) : $ dist<v,v> = \lVert v-w \rVert$    

cauchy-schwarz 부등식 : $| \langle v, w \rangle | \le \lVert v \rVert \lVert w \rVert$    
.


**동일한 표현**   
벡터들이 거의 평행하다 = 벡터들이 밀접하게 위치해 있다 = 벡터 간 방향이 거의 같다 = 벡터 간 내적이 크다     

  
### Duality(쌍대성)   
어떤 공간을 수선으로 선형변환할 때 마다 그 공간의 한 특정 벡터와 연관이 있다.   
$$\begin{bmatrix} 2\\1 \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} 2&1 \end{bmatrix}  \begin{bmatrix} x\\ y \end{bmatrix}  = 2\centerdot x+1\centerdot y$$   
- 벡터에서의 "Dual" : 그 벡터가 가진 선형변환 성질   
- 1차원으로 변환시키는 선형변환에서 "Dual" : 공간 상의 특정 벡터   

### Cross Products(외적)  
$\mathbf{\vec{x}} \times \mathbf{\vec{y}} = \lVert \vec{x} \rVert \lVert \vec{y} \rVert \sin \theta n = \mathbf{\vec{p}}$   

두 벡터 사이의 평행사변형의 면적과 방향을 나타내는 연산으로 순서가 중요하다.    
새 벡터 p의 길이는 평행사변형의 면적과 같고, 방향은 평행사변형에 수직이다(양수라면 오른손 법칙, 음수라면 왼손 법칙).   

2차원 공간 : $\mathbf{\vec{v}} \begin{bmatrix} 3 \\ 1 \end{bmatrix}$이고, $\mathbf{\vec{w}} \begin{bmatrix} 2 \\ -1 \end{bmatrix}$ 일 때, $\mathbf{\vec{v}} \times \mathbf{\vec{w}} = det \begin{pmatrix} \begin{bmatrix} 3 & 2 \\ 1 & -1 \end{bmatrix} \end{pmatrix}$

![image](/assets/images/pages/crossproduct.png){: width="600" height="600"}   


### Outer Products(외적)  
Cross Product와 다른 연산으로 두 벡터를 행렬로 결합하는 텐서 곱이다.   
$$\mathbf{x} \otimes \mathbf{y} = \begin{pmatrix} x_1 y_1 & x_1 y_2 & \cdots & x_1 y_n \\ x_2 y_1 & x_2 y_2 & \cdots & x_2 y_n \\
\vdots & \vdots & \ddots & \vdots \\ x_m y_1 & x_m y_2 & \cdots & x_m y_n \end{pmatrix}$$    

### Crammer's Rule  

## 4 EigenVectors & EigenValues

### EigenVectors(고유벡터) & EigenValues(고유값) 
정의 : 하나의 $n\times n$ 행렬 $A: R^n \to R^n$을 선형변환이라 할 때, 0이 아닌 벡터 $v \in R^n$이 $A(v) = \lambda v$를 만족한다. $\lambda$를 행렬 $A$의 고유값이라 하고, $v$를 고유벡터라 한다.    

쉽게 말해서 선형변환 후 방향이 변하지 않고 같은 직선 상에 머무르는 벡터가 $v$, $v$가 얼마나 확대되거나 축소되었는지의 크기 변화율을 나타내는 스칼라 값이  $\lambda$이다.    

- triangular 행렬의 고유값들은 그 행렬의 주 대각선 위의 성분이다.    
- 만약 $v_1,v_2, \dots ,v_r$이 서로 다른(distinct) $\lambda_1,\lambda_2, \dots ,\lambda_r$에 대응되는 고유벡터라면, $\{v_1,v_2, \dots ,v_r\}$은 선형독립이다.   
- $n\times n$ 행렬 $A$와 $B$가 similar하면, 동일한 characteristic polynomial을 갖고 동일한 고유값(with same multiplicities)을 갖는다.   
  가역 행렬 $P$가 $P^{-1}AP=B$ 또는 $A=PBP^{-1}$이면, $A$는 $B$에 **"similar"**하다    
- $n$개의 서로 다른 고유값을 갖는(=$n$개의 선형독립인 고유벡터를 갖는) $n\times n$ 행렬은 대각화가능(diagnalizable)하다.   

## 5 Orthogonality & Least Squares   
### Orthogonality   

### Orthogonal Sets, Projections    

### Gram-Schmidt Process    

### Least-Squares Problems     


## 6 Symmetric Matrices & Quadratic Forms


## 7 Geometry of Vector Spaces   


## 8 Optimization   

## 9 Finite-State Markov Chains   


## Reference

youtube : 
- Essence of linear algebra(3Blue1Brown) (https://www.youtube.com/watch?v=v8VSDg_WQlA&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab&index=8)    
- 혁펜하임의 "보이는" 선형대수학(혁펜하임)    
book : 
- 최적화 이론(임정환) 6장  
- Linear Algebra and Its Applications 5th(David C. Lay)    

