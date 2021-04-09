# 머신러닝/딥러닝

<br>

## 1. Machine Learning

### Supervised / Unsupervised Learning

**Supervised Learning**

> 지도학습의 방법은 크게 Classification과 Regression으로 나뉜다

![image](https://user-images.githubusercontent.com/75229881/110902534-64af6680-8349-11eb-95b0-9eb349facd25.png)

* Classification

  * 이산값을 포함하는 집합에서 Label을 나누는 것
  * Logistic Regression
    * 범주형 데이터에 적용, 확률데이터가 0과 1의 범주내에 위치할 수 있도록 한다.
    * 만약 선형회귀를 분류에 사용한다면 우측 상단의 값은 굉장히 큰 비정상값임에도 정상값으로 판단될 수 있기에 부적합하다.

  ![image](https://user-images.githubusercontent.com/75229881/110903293-8fe68580-834a-11eb-91bb-65fa0ff648bf.png)

* Regression

  * 연속적인 데이터의 값을 예측하는 것
  * Linear Regression
    * 평균제곱오차를 활용하여 빨간점과 파란선의 오차를 최소화하는 방향으로 학습

  ![image](https://user-images.githubusercontent.com/75229881/110902740-b1933d00-8349-11eb-9849-57068047e4e5.png)

  

* Decision Tree
  * 주어진 입력값에 대해서 여러 번의 분류를 통해 답을 찾는 방법
  * 회귀모델은 하나의 선을 긋지만 Decision Tree는 여러개의 선을 긋는다
* Random Forest
  
  * 여러개의 decision tree를 형성하고 새로운 데이터 포인트를 각 트리에 동시에 통과시키며, 각 트리가 분류한 결과에서 투표를 실시하여 가장 많이 득표한 결과를 최종 분류 결과로 선택

**Unsupervised Learning**

> 클러스터링, 시각화, 연관 규칙 활용

* K-means Clustring
  * “K”는 주어진 데이터로부터 그룹화 할 그룹, 즉 클러스터의 수.  “Means”는 각 클러스터의 중심과 데이터들의 평균 거리
  * Expectation(K 찾기), Maximization(그룹 짓기) 반복

---

<br>

## 2. Deep Learning

> 기존의 머신러닝에서 다중 퍼셉트론을 이용하여 Hidden Layer를 구성한 네트워크를 이용한 학습을 딥러닝이라고 한다

* 네트워크의 각 노드들이 Weight와 bias를 조정하며 최적해를 찾는과정

* Activation Function
  * 활성화 함수는 입력값을 non-linear한 방식으로 출력값을 도출하기 위해 사용
  * 비 선형함수 사용 + Hidden Layer를 이용한 여러 층의 레이어
  * 두 가지 조건을 이용하여 Non-linear한 문제를 해결가능
  * 또한, Linear한 경우 연속해서 Wx의 연산이므로 Hidden Layerd의 효과가 없음
  
* Back Propagation

  * Non linear한 문제를 해결했지만 다수의 Node에 대한 연산이 필요함
  * 미분의 연쇄법칙을 활용하여 한번의 cost에 대한 연산을 한번의 곱셈으로 가능
  * 따라서, gradient descent를 적용하면서 back propagation을 이용하여 최적해를 구하는 방향으로 학습

* Vanishing gradient problem

  * 앞서 적용한 Activaion Function으로 Sigmoid와 같은 함수를 적용하여 Back Propagation하여 학습을 진행하는 경우 HL가 깊어질수록 앞쪽의 노드의 영향력이 옅어지는 Vanishing gradient 문제가 발생
  * Why? Sigmoid의 도함수의 최대값은 0.25이기 때문에 망이 깊어질수록 그 가중치는 1/4로 옅어짐
  * ReLu를 이용, 도함수는 Step Function
  * 최종 Layer에 Softmax를 활용하여 벡터의 각 원소를 정규화하기 위해 입력 값을 모두 지수 값으로 바꾼다. 지수 함수를 사용하면 가중치를 더 커지게 하는 효과를 얻을 수 있음

* Optimization

  * Hyper Parameter

    * gradient descent, learning rate, hidden layer, epoch, batch size ..

  * Data Preprocessing

    * 모든 값에 대해 동일한 learning rate(상수값)가 적용되므로 전처리하여 범주화시킬 필요
    * Data-centered, Normalization

  * Drop out

  * Weight initialization

    * Xavier, He

  * Batch Normalization

    * Input 레이어의 분포를 Input을 gaussian 범위로 유지 

    * Covariate Shift Problem 해결


---



