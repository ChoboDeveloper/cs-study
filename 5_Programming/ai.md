# AI

<br>

### 결정트리

* 분류(Classification)와 회귀(Regression) 모두 가능한 **Supervised Learning** 모델

---

### SVM

* 분류 과제에 사용할 수 있는 강력한  **Supervised Learning** 모델
* 분류를 위한 기준 선을 정의하는 모델

---

### 베이시안 네트워크

> 베이지안 네트워크(Bayesian NetWork)란 **방향성을 갖는 비순환 그래프 (DAG : Directed Acyclic Graph)와 조건부 확률 테이블 (CPT : Conditional Probability Tables)**을 통하여 집합을 조건부 독립으로 표현하는 확률의 그래픽 모델로써 다양한 변수를 표현하는 노드(Node)와 변수들 사이의 의존 관계를 표현하는 호(Arc)를 이용하여 **부모 노드와 자식 노드의 인과관계**를 확률을 기반으로 불완전한 입력값에 대해서도 사후확률 추론이 가능한 확률적 계산 기법이다.

---

### CNN

CNN(Convolutional Neural Network)은 기존 Fully Connected Neural Network와 비교하여 다음과 같은 차별성을 갖는다.

> 이전 레이어의 모든 노드가 다음 레이어의 모든 노드에 연결된 레이어를 Fully Connected Layer(FC Layer)라고 한다. (Dense Layer)
>
> 완전연결 계층에 입력할 때는 3차원 데이터를 평평한 1차원 데이터로 평탄화해줘야 한다.
>
> 완전연결 계층은 형상을 무시하고 모든 입력 데이터를 동등한 뉴런(같은 차원의 뉴런)으로 취급하여 형상에 담긴 정보를 살릴 수 없다.

- 각 레이어의 입출력 데이터의 형상 유지
- 이미지의 공간 정보를 유지하면서 인접 이미지와의 특징을 효과적으로 인식
- 복수의 필터로 이미지의 특징 추출 및 학습
- 추출한 이미지의 특징을 모으고 강화하는 Pooling 레이어
- 필터를 공유 파라미터로 사용하기 때문에, 일반 인공 신경망과 비교하여 학습 파라미터가 매우 적음

**용어**

- Convolution(합성곱)
  - 컨볼루션 연산을 통해서 입력 데이터로 부터 특징을 추출
- 채널(Channel)
- 필터(Filter)
- 커널(Kernel)
- 스트라이드(Strid)
- 패딩(Padding)
- 피처 맵(Feature Map)
- 액티베이션 맵(Activation Map)
- 풀링(Pooling) 레이어
  - 풀링 레이어는 컨볼류션 레이어의 출력 데이터를 입력으로 받아서 출력 데이터(Activation Map)의 크기를 줄이거나 특정 데이터를 강조하는 용도로 사용
  - Pooling 레이어는 Convolution 레이어와 비교하여 다음과 같은 특징
    - 학습대상 파라미터가 없음
    - Pooling 레이어를 통과하면 행렬의 크기 감소
    - Pooling 레이어를 통해서 채널 수 변경 없음
    - Overfitting 감소

---

### 분류성능 평가지표

<img src = "https://user-images.githubusercontent.com/75229881/164005690-d082470f-4f58-47ea-af76-b9159cbc4fc4.png" width="40%">

1. Precision
   * **정밀도**란 모델이 Positive라고 분류한 것 중에서 실제 True인 것의 비율
   
   * TP / (TP + FP)
   
     > 안타깝게도 recall도 완벽한 통계치는 아닙니다. 예를 들어, 위의 눈내림 예측기 예에서 이번에는 항상 `True` 로 예측한다고 가정해봅시다. 물론 accuracy는 낮겠지만, 모델이 모든 날을 눈이 내릴거라 예측하기 때문에 recall은 `1`이 되고 맙니다. 이 모델은 항상 `False` 로 예측하는 모델과 다를 바 없지만 높은 recall을 보유하게됩니다.
     >
     > 이러한 상황에서 도움을 줄 수 있는 통계치는 바로 *precision(정밀도)* 입니다. **Precision은 모델이 True로 예측한 데이터 중 실제로 True인 데이터이 수입니다**. 위의 예시에서 precision은 실제로 눈이 내린 날의 수를 모델이 눈이 내릴거라 예측한 날의 수로 나눈 값입니다.
   
2. Recall
   * **재현율**이란 실제 True인 것 중에서 모델이 Positive라고 예측한 것의 비율
   
   * TP / (TP + FN)
   
     > accuracy는 데이터에 따라 매우 잘못된 통계를 나타낼 수도 있습니다. 예를 들어, 내일 눈이 내릴지 아닐지를 예측하는 모델이 있다고 가정해 봅시다. 꽤 괜찮은 성능을 내는 모델을 작성할 수 있는데요, 바로 항상 `False` 로 예측하는 것입니다. 이 모델은 놀랍게도 굉장히 높은 accuracy를 갖습니다. 왜냐하면 눈이 내리는 날은 그리 많지 않기 때문이죠. 하지만 높은 accuracy를 보유함에도 불구하고 이 모델은 전혀 쓸모가 없습니다.
     >
     > 이러한 상황에서 도움을 줄 수 있는 통계치는 바로 *recall(재현율)* 입니다. **Recall은 실제로 True인 데이터를 모델이 True라고 인식한 데이터의 수입니다**. 위의 예시에서 recall은 모델이 눈이 내릴거라 예측한 날의 수를 실제로 눈이 내린 날의 수로 나눈 값입니다.
   
3. Sensitivity(=Recall)

4. Specificity
   * Specificity는 Sensitivity와 반대로 False set을 입력하였을때, False로 인식한 것의 비율이다.
   * 분류기에 빗대어 말하면 0이라는 값을 넣었을 때 0이라는 결과를 얻은 비율이다.

**F1-Score**
$$
F1Score=2*\frac{precison*recall}{precision+recall}
$$

> 모델의 성능을 측정하는데 있어서 precision과 recall은 유용하게 사용됩니다. 그러나, 우리는 여전히 모델이 얼마나 효과적인지를 설명할 수 있는 한 가지 지표를 더 필요로합니다. 이 때 *F1 score* 가 사용됩니다.
>
> **F1 score는 precision 과 recall의 조화평균입니다**. 
>
> F1 score는 precision과 recall을 조합하여 하나의 통계치를 반환합니다. 여기서 일반적인 평균이 아닌 조화 평균을 계산하였는데, 그 이유는 precision과 recall이 `0` 에 가까울수록 F1 score도 동일하게 낮은 값을 갖도록 하기 위함입니다.
>
> 예를 들어, `recall = 1` 이고 `precision = 0.01` 로 측정된 모델이 있다고 생각해봅시다. 위 모델에는 분명 문제가 있다고 판단할 수 있는데요. precision이 매우 낮기 때문에 F1 score에도 영향을 미치게 됩니다. 만약 일반적인 평균을 구하면 다음과 같습니다.



---

