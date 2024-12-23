  ### References
[Ref 1. 세종대학교 github](https://github.com/sejongresearch/2024.DeepLearning)
# Personal Study
---
##### Machine Learning vs. Deep Learning
[Ref 2. 딥 러닝과 머신 러닝의 비교](https://www.zendesk.kr/blog/machine-learning-and-deep-learning/)
###### 머신러닝 PipeLine
1. **데이터를 수집**
2. **데이터를 전처리**
3. **훈련 데이터, 처리 검증데이터 분리**
4. **알고리즘 선택**
5. **실행**
6. **결과 도출**
### 1. 데이터 수집

문제를 해결하기 위한 가장 첫 단계는 **적절한 데이터를 확보**하는 것입니다. 이는 프로젝트의 성패를 좌우하는 중요한 단계로, 다양한 방법을 통해 데이터를 수집합니다.

- **내부 데이터**: 기존 시스템에서 이미 수집한 데이터나 로그, 고객 행동 데이터, 거래 내역 등을 활용합니다.
- **외부 데이터**: 웹 스크래핑을 통해 온라인 데이터베이스나 공개 API를 사용해 추가 데이터를 수집할 수 있습니다.
- **공공 데이터 및 데이터셋**: Kaggle, UCI ML 리포지토리 등에서 공개된 데이터를 사용할 수도 있습니다.

데이터를 수집할 때는 문제가 무엇인지, 예측하고자 하는 목적이 무엇인지에 맞춰 데이터를 적절히 수집하고 저장해야 합니다.

### 2. 데이터 전처리

수집한 데이터는 대부분 바로 사용할 수 없으므로 **모델 학습에 적합한 상태로 가공**해야 합니다. 전처리는 모델이 더 효과적으로 학습할 수 있도록 데이터를 정리하는 과정입니다.

- **결측치 처리**: 데이터에 누락된 값이 있을 경우, 이를 보정하거나 제거해야 합니다. 보통 평균, 중앙값으로 대체하거나, 특정 행 전체를 삭제할 수 있습니다.
- **이상치 탐지**: 데이터의 범위를 벗어나거나 비정상적인 값은 모델 성능을 저하시킬 수 있습니다. 이런 값은 도메인 지식에 따라 수정하거나 제거합니다.
- **데이터 정규화 및 표준화**: 데이터 값의 범위가 너무 크면 학습에 불리할 수 있습니다. 표준화(평균과 표준편차로 스케일 조정)나 정규화(데이터 값을 0에서 1 사이로 변환)를 통해 모델이 학습하기 쉽게 조정합니다.
- **레이블 인코딩**: 범주형 데이터를 숫자로 변환해야 합니다. 예를 들어, ‘남성’은 1로, ‘여성’은 0으로 변환하는 식입니다. 이는 텍스트 데이터를 모델이 이해할 수 있도록 하는 과정입니다.

이 외에도, 텍스트 분석에서는 **불용어 제거**, **어간 추출** 등의 전처리, 이미지 처리에서는 **이미지 크기 조정** 및 **필터링** 같은 다양한 전처리 방법이 사용됩니다.

### 3. 훈련 데이터와 검증 데이터 분리

모델의 성능을 정확하게 평가하기 위해, 수집된 데이터를 **훈련 데이터**와 **검증 데이터(또는 테스트 데이터)**로 나눕니다. 훈련 데이터는 모델 학습에 사용하고, 검증 데이터는 학습된 모델이 새로운 데이터에서도 잘 일반화되었는지 평가하기 위해 사용됩니다.

- **비율 설정**: 일반적으로 데이터의 70~~80%는 훈련 데이터로, 20~~30%는 검증 데이터로 사용합니다.
- **교차 검증**: 데이터셋을 여러 번 나누어 학습하고 평가해, 모델의 일반화 성능을 높입니다. K-폴드 교차 검증이 대표적입니다.

이 과정에서 검증 데이터는 학습 과정에 참여하지 않기 때문에 모델이 과적합(overfitting)되지 않고 일반화 능력을 갖출 수 있도록 돕습니다.

### 4. 알고리즘 선택

데이터의 특성과 문제의 성격에 맞는 **알고리즘을 선택**합니다. 이 단계에서는 문제의 유형에 따라 적합한 알고리즘을 선택하는 것이 중요합니다.

- **회귀 분석**: 숫자 예측 문제에 적합합니다. 예를 들어, 주택 가격 예측에서는 선형 회귀나 다중 회귀 모델을 사용할 수 있습니다.
- **분류 알고리즘**: 카테고리를 예측하는 문제에는 로지스틱 회귀, 의사결정 나무, 서포트 벡터 머신(SVM) 등이 사용됩니다.
- **신경망 및 딥러닝 모델**: 이미지 인식에는 합성곱 신경망(CNN), 텍스트 분석에는 순환 신경망(RNN)이나 트랜스포머 등이 유리합니다.

문제에 맞는 알고리즘을 선택해야만 모델이 데이터의 패턴을 더 잘 학습하고 정확하게 예측할 수 있습니다.

### 5. 모델 학습 및 최적화

선택한 알고리즘을 **훈련 데이터에 적용하여 학습**합니다. 이 과정에서 **하이퍼파라미터 튜닝**을 통해 모델의 성능을 최적화합니다. 딥러닝의 경우 연산량이 크기 때문에 **GPU**나 **TPU** 같은 고성능 컴퓨팅 자원을 사용해 학습 속도를 높일 수 있습니다.

- **하이퍼파라미터 튜닝**: 학습률, 배치 크기 등 모델의 성능에 영향을 미치는 요소들을 최적화합니다. Grid Search나 Random Search, Bayesian Optimization과 같은 방법으로 최적의 하이퍼파라미터를 찾습니다.
- **조기 종료**: 학습이 진행될수록 훈련 데이터에서는 성능이 높아지지만 검증 데이터에서 성능이 떨어질 수 있습니다. 이를 방지하기 위해 일정 기준에서 학습을 중단해 과적합을 방지합니다.

### 6. 결과 도출 및 성능 평가

모델 학습이 완료되면, **검증 데이터로 최종 평가**하여 예측의 성능을 확인합니다. 주요 평가 지표는 다음과 같습니다.

- **정확도(Accuracy)**: 전체 예측 중 맞힌 예측의 비율로, 분류 문제에서 가장 일반적인 평가 척도입니다.
- **정밀도(Precision)와 재현율(Recall)**: 특정 클래스의 예측 성능을 측정하는 데 유용합니다. 예를 들어, 의료 데이터에서는 False Positive를 최소화하는 것이 중요할 때 정밀도를 높게 설정합니다.
- **F1-score**: 정밀도와 재현율의 조화 평균으로, 두 지표가 균형을 이룬 모델을 만들 때 유용합니다.
- **MSE, MAE**: 회귀 모델의 평가에 많이 사용되며, 모델이 예측한 값과 실제 값의 차이를 측정합니다.

최종 결과를 분석한 후, 모델이 실제 문제에 적합하다면 배포할 준비를 합니다. 필요 시 추가적인 **모델 개선**과 **성능 튜닝**을 반복하며, 결과에 따라 새로운 데이터나 추가적인 학습을 통해 모델을 점진적으로 발전시킬 수 있습니다.

이와 같은 반복적이고 체계적인 과정이 머신러닝 및 딥러닝 모델의 성공적인 구축과 실사용에서의 성능을 보장합니다.
# Lecture Study
---
[Ref 3. 인공뉴런 관련](https://www.mql5.com/ko/articles/5486)
### 인공 신경망(Artificial Neural Networks)
- **`연결주의 인공지능`** 
##### 구성
- `수상돌기(dendrite)` - `신경세포체(soma)` - `축삭돌기(axon)` - `시냅스(synapse)`
	- `수상돌기(denite)` : **입력**, _연결 가중치를 학습_
	- `신경세포체(soma)` : **연산 수행**, _노드_
	- `축삭돌기(axon)` : **출력**, _처리한 정보를 뉴런에게 전달_
- **1957년, Frank Rosenblatt : 퍼셉트론(Perceptron) 학습 모델 제시**
	- *1969, 단층 퍼셉트론은 배타적 논리합(XOR)과 같은 간단한 문제도 해결 못함*
	- **1974, 다층 퍼셉트론 구조의 학습 방법이 발표 -> `역전파(backpropagation) 알고리즘`**
==단층, 다층, 가중치 ==
- **`심층 신경망(deep neural network)`**
	- 많은 수의 층으로 구성하면 더욱 높은 차원의 표현이 가능
- `**딥러닝(deep learning)**`
	- 심층 신경망을 학습하기 위해 활용되는 기계학습 알고리즘
	- 학습 성능을 제한하는 제반 문제의 개선이 필요
		- *(부족한 학습 데이터, 불안정한 경사, 과적합, 방대한 계산량)*
### 신경망의 기본 구조
##### 인공 뉴런
![[cs_artificialneural.gif]]
**연산 과정**
1. `입력 값`과 `가중치`를 곱한다.
2. `입력 값 * 가중치` 모두 더한다. 이때, `편향치`도 함께 더한다.
3. `∑(입력 값 * 가중치) + 편향치`를 `활성함수`에 넣는다.
4. 결과 도출

- **활성함수(activation function)**
	- 일반적으로 비선형 특징을 갖는 함수 사용
	- u의 값이 0보다 작으면 출력 억제, 0보다 크면 출력
- **가중치(바이어스, bias)**
	- 뉴런이 활성화 되는 레벨을 조정

### 활성함수
1. **계단 함수**
	- *정의역을 유한한 개수의 구간으로 나누어서 각 구간에서 상수인 함수*
		- **활성함수 결과가 >=0 일 경우 ,1** 
		- **활성함수 결과가 <0 일 경우, 0**

2.  **시그모이드 함수**
	- 'S' 자 형태의 곡선 함수
	- 모든 $x$에 대해 미분 가능 함(경사 하강법)
	- `경사 소멸`의 문제 원인이 됨
		- **`로지스틱 함수(logistic)`**
			- $\sigma(x) = \frac{1}{1 + e^{-x}}$
				- $x$가 $-\infty$ 이면, 분모가 $\infty$으로 수렴 = 0
				- $x$가 +$\infty$ 이면, 분모가 1로 수렴 = 1
		- **`쌍곡탄젠트(tanh)`**
			- $\tanh(x) = \frac{\sinh(x)}{\cosh(x)} = \frac{e^x - e^{-x}}{e^x + e^{-x}}$
		- **`오차 함수(erf)` 등**
			- $\text{erf}(x) = \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2} \, dt$
3. **ReLU**
	- 심층망에서 경사 `소멸 문제`를 개선하기 위해 `시그모이드`의 대안으로 활용되는 활성함수
		- **활성함수 결과가 < 0 일 경우, 0으로 표현**
		- **활성함수 결과가 >= 0 일 경우, 결과를 표현**
	- 활성함수 결과가 0 일 때, 미분 불가
	- `Dying ReLU` 문제
	- `ReLU`의 변형
		- **Leaky ReLU**
		- **PReLU**
		- **GELU**
		- **Swish**
### 단층 피드포워드 신경망
- `피드포워드 신경망` 
	- `입력층`에서 `출력층` 방향으로 뉴런 층의 연결이 이루어지는 구조
- `단층 퍼셉트론`
	- 층이 1개로 이루어진 퍼셉트론
	- `지도방식`으로 학습
		- 학습표본 집합($x$, $y$)
			- $x$ = $[x1, x2 ... xd]$ : 입력
			- $y$ = 레이블, 출력으로 나와야 하는 값
		- 학습 대상 파라미터
			- $w$ = $[w1, w2 ... wd]$ : 입력이 뉴런에 전달ㄹ되는 연결의 가중치
			- $b$ : 가중치
	- **퍼셉트론의 학습**
		1. 파라미터 ($w, b$) 초기화: 작은 크기의 랜덤 값으로 초기화
		2. 모든 학습표본을 대상으로 파라미터 업데이트를 반복
			1. $t$번 반복 업데이트된 $w(t)$와 $b(t)$를 이용하여 $k$번째 학습표본 $x(k)$에 대한 출력 $\hat{y(k)}$를 예측
			2. 오차 $\delta = \hat{y(k)} - y(k)$ 와 입력의 곱에 비례하여 $w$와 $b$를 업데이트 함
### 실습 - 퍼셉트론:붓꽃
```colab
# 퍼셉트론-붓꽃

# 필요한 패키지 Load
import matplotlib.pyplot as plt
import numpy as np
from sklearn.datasets import load_iris

# 데이터 준비 함수 정의
def prepare_data(target):
    iris = load_iris()          # iris data set 읽기
    X_tr = iris.data[:, 2:]     # 4개의 특징 중 꽃잎의 길이와 폭 선택
    labels = iris.target_names  # 'setosa', 'versicolor', 'virginica'
    y = iris.target

    # 학습표본의 레이블 지정 - target에 지정된 레이블이면 1, 그 외는 0
    y_tr = []
    for i in range(150):
        y_tr.append(labels[y[i]] == target)
    y_tr = np.array(y_tr, dtype=int)
    return X_tr, y_tr, ['(1) '+target, '(0) the others']

# 활성합수 - 단위 계단 함수
def step(x):
    return int(x >= 0)


# 퍼셉트론 클래스 선언
class Perceptron():
    def __init__(self, dim, activation):
        rnd = np.random.default_rng()
        self.dim = dim
        self.activation = activation
        # 가중치(w)와 바이어스(b)를 He normal 방식으로 초기화
        self.w = rnd.normal(scale = np.sqrt(2.0 / dim), size=dim)
        self.b = rnd.normal(scale = np.sqrt(2.0 / dim))

    def printW(self):
        for i in range(self.dim):
            print('  w{} = {:6.3f}'.format(i+1, self.w[i]), end='')
        print('  b = {:6.3f}'.format(self.b))

    def predict(self, x):  # numpy 배열 x에 저장된 표본의 출력 계산
        return np.array([self.activation(np.dot(self.w, x[i]) + self.b)
                          for i in range(len(x))])

    def fit(self, X, y, N, epochs, eta=0.01):
        # 학습표본의 인덱스를 무작위 순서로 섞음
        idx = list(range(N))
        np.random.shuffle(idx)
        X = np.array([X[idx[i]] for i in range(N)])
        y = np.array([y[idx[i]] for i in range(N)])

        f = 'Epochs = {:4d}    Loss = {:8.5f}'
        print('w의 초깃값  ', end='')
        self.printW()
        for j in range(epochs):
            for i in range(N):
                # x[i]에 대한 출력 오차 계산
                delta = self.predict([X[i]])[0] - y[i]
                self.w -= eta * delta * X[i]
                self.b -= eta * delta
            # 학습 과정 출력
            if j < 10 or (j+1) % 100 == 0:
                loss = self.predict(X) - y
                loss = (loss * loss).sum() / N
                print(f.format(j+1, loss), end='')
                self.printW()

# 시각화
def visualize(net, X, y, multi_class, labels, class_id, colors,
               xlabel, ylabel, legend_loc='lower right'):
    # 데이터의 최소~최대 범위를 0.05 간격의 좌표값으로 나열
    x_max = np.ceil(np.max(X[:, 0])).astype(int)
    x_min = np.floor(np.min(X[:, 0])).astype(int)
    y_max = np.ceil(np.max(X[:, 1])).astype(int)
    y_min = np.floor(np.min(X[:, 1])).astype(int)
    x_lin = np.linspace(x_min, x_max, (x_max-x_min)*20+1)
    y_lin = np.linspace(y_min, y_max, (y_max-y_min)*20+1)

    # x_lin과 y_lin의 격자좌표의 x와 y 값 구하기
    x_mesh, y_mesh = np.meshgrid(x_lin, y_lin)

    # (x, y) 좌표의 배열로 만들어 신경망의 입력 구성
    X_test = np.column_stack([x_mesh.ravel(), y_mesh.ravel()])

    # 학습된 신경망으로 X_test에 대한 출력 계산
    if multi_class:
        y_hat = net.predict(X_test)
        y_hat = np.array([np.argmax(y_hat[k])
                            for k in range(len(y_hat))], dtype=int)
    else:
        y_hat = (net.predict(X_test) >= 0.5).astype(int)
        y_hat = y_hat.reshape(len(y_hat))

    # 출력할 그래프의 수평/수직 범위 설정
    plt.xlim(x_min, x_max)
    plt.ylim(y_min, y_max)

    # 클래스별로 산점도 그리기
    for c, i, c_name in zip(colors, labels, class_id):
        # 격자 좌표의 클래스별 산점도
        plt.scatter(X_test[y_hat == i, 0], X_test[y_hat == i, 1],
                     c = c, s = 5, alpha = 0.3, edgecolors = 'none')
        # 학습 표본의 클래스별 산점도
        plt.scatter(X[y == i, 0], X[y == i, 1],
                     c = c, s = 20, label=c_name)
    # 범례의 표시 위치 지정
    plt.legend(loc=legend_loc)
    # x축과 y축의 레이블을 지정한 후 그래프 출력
    plt.xlabel(xlabel, size=12)
    plt.ylabel(ylabel, size=12)
    plt.show()

# 훈련 데이터 준비
nSamples = 150
nDim = 2
target = 'virginica'         # 식별하고자 하는 붓꽃 종류 지정
X_tr, y_tr, labels = prepare_data(target)

# 퍼셉트론 객체 생성 및 학습
p = Perceptron(nDim, activation=step)
p.fit(X_tr, y_tr, nSamples, epochs=1000, eta=0.01)

# 특징 공간 결정 영역 시각화
visualize(p, X_tr, y_tr,
          multi_class=False,
          class_id=labels,
          labels=[1, 0],
          colors=['magenta', 'blue'],
          xlabel='petal length',
          ylabel='petal width',
          legend_loc='upper left')
```