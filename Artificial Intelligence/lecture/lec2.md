# Lecture 2: Machine Learning 1, Linear Models
[목차](index.md)<br><br>

## 선형 분류기(linear classification)
### application: 스팸 분류기
- input: x = email or message
- output: y (spam, not spam)
- 목적: predictor f를 얻는 것. y = f(x)

### prediction tasks의 종류
- binary classification (이진 분류기)
    - output의 값이 두 종류.
- regression
    - output이 실수 범위.
- multiclass classification
    - output이 여러 종류.
- ranking
    - output은 순서.

### Data (supervised learning)

### Feature extraction
- input x에 대하여, y를 예측하는 데에 필요할 만한 feature을 뽑아낸다.

### Feature vector
- 수학적으로, feature vector는 feature name이 필요 없을수도 있다.
Definition: feature vector
- input x에 대하여, 그것의 feature vector는
    - $\phi(x) = [\phi_1(x), \phi_2(x), ..., \phi_d(x)]$
    - $\phi(x)$는 d-차원 벡터 공간의 하나라고 할 수 있다.

### Weight vector
- weight vector는 feature vector와 차원이 같으며, 각 값에 곱해준다.
- weight vector는 data로 자동적으로 계산된다. (알고리즘)

### Linear predictor
- weight vector와 feature vector의 곱.
- $w\cdot\phi(x)$

### Linear (binary) classifier
- example: $f(x) = sign(w\cdot\phi(x))$

### Lineary classfier: geometric intuition

### Score and margin
- correct label: y
- predicted label: $\^{y} = f_w(x) = sign(w\cdot\phi(x))$
- definition: score, +1이라고 예측하는데에 얼마나 자신이 있는가?
    - $w\cdot\phi(x)$
- definition: margin, 얼마나 올바르게 예측했는가?
    - $(w\cdot\phi(x))y$

### Loss function for linear classifier
#### Loss function
- 손실 함수 l(w,x,y)는 다음을 정량화한다.
    - x에 대하여 w를 사용하여 예측을 할 때, 정답이 y라면 어느 정도의 loss를 갖게 되는가?
#### Loss function for linear (binary) classifier
- $y = sign(w\cdot\phi(x))$라면,
- 이는 $w\cdot\phi(x)y > 0$와 같으며,
- 따라서, 손실함수는 $max(-(w\cdot\phi(x))y, 0)$

### Loss minimization
#### Loss function
$$l(w,x,y) = max{-(w\cdot\phi(x), 0)}$$

#### 학습 데이터 D에 대한 손실 함수 J(w)
$$J(w) = $$ 모두 더하고, 사이즈로 나눈다.

### Loss minimization
- J(w)를 최소로 하는 w를 찾기.

### Gradient Descent
- 어떻게 최소로하는 w를 찾을 수 있을까? => gradient descent
- w에서 기울기를 구하고, 그만큼 w에 빼주면서, local minimum을 찾는다.
- 이때, alpha는 step size로, learning late라는 하이퍼 파라미터이다.

### Gradient Descent is slow!
- 이 방법은 느리다.
- 모든 학습 데이터를 읽어야 하므로

### Stochastic Gradient Descent (SGD)
- 데이터를 batch 단위로 나눠서 학습.

### SGD and Perceptron algorithm
- perceptron algorithm은 batch size가 1.

### Hinge loss (선형 분류기에 대해)
#### Hinge loss function
$$l(w,x,y) = max{1-(w\cdot\phi(x))y, 0}$$
- intuition: margin이 1이하이면, loss가 줄어든다.
- SVM은 L2 정규화에 대해, hinge loss를 쓴다.

## Linear regression (선형 회귀)
### Regression: problem setup

## Logistic regression (로지스틱 회귀)