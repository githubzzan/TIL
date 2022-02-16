

# Day15 Today I Learned

### 의사결정트리(Decision Tree)란?

- **의사결정트리는 일련의 분류 규칙을 통해 데이터를 분류, 회귀하는 지도 학습 모델 중 하나이며,**
- **결과 모델이 Tree 구조를 가지고 있기 때문에 Decision Tree라는 이름을 가집니다.**
- 아래 그림을 보면 더 쉽게 이해가 가능합니다.



![img](https://blog.kakaocdn.net/dn/QkorS/btq2D230cNa/5Gs63KPkcKiZdqNiO5gUBk/img.png)



- 위 그림은 대표적인 의사결정트리의 예시로서, 타이타닉호의 탑승객의 생존여부를 나타내고 있습니다.
- **이렇게 특정 기준(질문)에 따라 데이터를 구분하는 모델을 의사 결정 트리 모델이라고 합니다.**
- **한번의 분기 때마다 변수 영역을 두 개로 구분합니다.**
- 결정 트리에서 질문이나 정답은 노드(Node)라고 불립니다.
  - 맨 처음 분류 기준을 Root Node라고 하고
  - 중간 분류 기준을 Intermediate Node
  - 맨 마지막 노드를 Terminal Node 혹은 Leaf Node라고 합니다.
  - **결정 트리의 기본 아이디어는, Leaf Node가 가장 섞이지 않은 상태로 완전히 분류되는 것, 즉 복잡성(entropy)이 낮도록 만드는 것입니다.**



## 붓꽃 품종 예측하기

데이터 수집 및 객체 생성

```python
from sklearn.datasets import load_iris
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score
import pandas as pd

#붓꽃 데이터 세트 로딩
iris = load_iris()

#iris.data : 피처(feature) - numpy
iris_data = iris.data
print('iris feature값 : ', iris_data)
#iris.target : 레이블(label) - numpy
iris_label = iris.target
print('iris target값 :', iris_label)
print('iris target명 :', iris.target_names)

x_train, x_test, y_train, y_test = train_test_split(iris_data, iris_label, test_size = 0.2, random_state = 11)

#DecisionTreeClasifier객체 생성
df_clf = DecisionTreeClassifier(random_state = 11)

#학습수행
df_clf.fit(x_train, y_train)

#예측수행
pred = df_clf.predict(x_test)

#평가 수행
print('예측 정확도 : {0:.4f}'.format(accuracy_score(y_test, pred)))
```

```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score
from sklearn.model_selection import KFold
import numpy as np

iris = load_iris()
features = iris.data
label = iris.target
dt_clf = DecisionTreeClassifier(random_state=156)

#5개의 폴드 세트로 분리하는 KFold 객체와 폴드 세트별 정확도를 담을 리스트 객체 생성
kfold = KFold(n_splits = 5)
cv_accuracy = []
print('붓꽃 데이터 세트 크기 : ', features.shape[0])

n_iter = 0

#KFold 객체의 split()를 호출하면 폴드 별 학습용, 검증용 테스트의 로우 인덱스를 array로 반환
for train_index, test_index in kfold.split(features):
    #kfold.split()으로 반환된 인덱스를 이용해 학습용, 검증용 테스트 데이터 추출
    
    x_train, x_test = features[train_index], features[test_index]
    y_train, y_test = label[train_index], label[test_index]
    
    #학습 및 예측
    dt_clf.fit(x_train, y_train)
    pred = dt_clf.predict(x_test)
    n_iter += 1
    
    #반복 시마다 정확도 측정
    accuracy = np.round(accuracy_score(y_test, pred), 4)
    train_size = x_train.shape[0]
    test_size = x_test.shape[0]
    
    print('\n#{0} 교차 검증 정확도 : {1},학습 데이터 크기 : {2}, 검증 데이터 크기 : {3}'.format(n_iter, accuracy, train_size, test_size))
    print('#{0} 검증 세트 인덱스 : {1}'.format(n_iter, test_index))
    cv_accuracy.append(accuracy)
    
# 개별 iteration별 정확도를 합하여 평균 정확도 계산
print('\n## 평균 검증 정확도 : ', np.mean(cv_accuracy))
```

## 1. 파라미터(Parameter)

머신러닝에서 사용되는 파라미터는 모델 파라미터라고도 하며, 모델에 적용할 하나 이상의 파라미터를 사용하여 새로운 샘플에 대한 예측을 하기 위해 사용됩니다. 즉, 머신러닝 훈련 모델에 의해 요구되는 변수라 할 수 있습니다.

 

###  파라미터의 특징

- 예측 모델은 새로운 샘플을 주어지면 무엇을 예측할지 결정할 수 있도록 파라미터를 필요로 한다.
- 머신러닝 훈련 모델의 성능은 파라미터에 의해 결정된다.
- 파라미터는 데이터로부터 추정 또는 학습된다.
- 파라미터는 개발자에 의해 수동으로 설정하지 않는다.(임의로 조정이 불가능하다)
- 학습된 모델의 일부로 저장된다.

### 모델 파라미터의 예

- 인공신경망의 가중치
- SVM(Support Vector Machine)의 서포트 벡터
- 선형 회귀 또는 로지스틱 회귀에서의 결정계수

 

## 2. 하이퍼파라미터(Hyperparameter)

머신러닝에서 하이퍼파라미터는 최적의 훈련 모델을 구현하기 위해 모델에 설정하는 변수로 학습률(Learning Rate), 에포크 수(훈련 반복 횟수), 가중치 초기화 등을 결정할 수 있습니다. 또한 하이퍼파라미터 튜닝 기법을 적용하여 훈련 모델의 최적값들을 찾을 수 있습니다.

 

### 하이퍼파라미터의 특징

- 모델의 매개 변수를 추정하는 데 도움이 되는 프로세스에서 사용된다.
- 하이퍼파라미터는 개발자에 의해 수동으로 설정할 수 있다.(임의 조정 가능)
- 학습 알고리즘의 샘플에 대한 일반화를 위해 조절된다.

### 하이퍼파라미터의 예

- 학습률
- 손실 함수
- 일반화 파라미터
- 미니배치 크기
- 에포크 수
- 가중치 초기화
- 은닉층의 개수
- k-NN의 k값

### 하이퍼파라미터의 튜닝 기법

- 그리드 탐색
- 랜덤 탐색
- 베이지안 최적화
- 휴리스틱 탐색



### 파라미터 실습

```python
from sklearn.model_selection import GridSearchCV
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import load_iris

# 데이터를 로딩하고 학습데이타와 테스트 데이터 분리
iris_data = load_iris()
X_train, X_test, y_train, y_test = train_test_split(iris_data.data, iris_data.target, test_size=0.2, random_state=121)

dtree = DecisionTreeClassifier()

### parameter 들을 dictionary 형태로 설정
parameters = {'max_depth':[1,2,3], 'min_samples_split':[2,3]}


import pandas as pd

#param_grid의 하이퍼 파라미터들을 3개의 train, test set fold 로 나누어서 테스트 수행 설정.
### refit=True 가 default 임. True이면 가장 좋은 파라미터 설정으로 재 학습 시킴.
grid_dtree = GridSearchCV(dtree, param_grid=parameters, cv=3, refit=True)

# 붓꽃 Train 데이터로 param_grid의 하이퍼 파라미터들을 순차적으로 학습/평가.
grid_dtree.fit(X_train, y_train)

# GridSearchCV 결과 추출하여 DataFrame으로 변환
scores_df = pd.DataFrame(grid_dtree.cv_results_)
scores_df[['params', 'mean_test_score', 'rank_test_score', \
          'split0_test_score', 'split1_test_score', 'split2_test_score']]

print('GridSearchCV 최적 파라미터:', grid_dtree.best_params_)
print('GridSearchCV 최고 정확도: {0:.4f}'.format(grid_dtree.best_score_))
```

## 원-핫 인코딩

### 원-핫 인코딩(One-Hot Encoding) 

 자연어를 컴퓨터가 처리하도록 하기 위해서 숫자로 바꾸는 방법을 알아야 합니다. 문자를 기계가 이해할 수 있는 숫자로 바꾼 결과 또는 그 과정을 임베딩(Embedding)이라고 합니다. 가장 간단한 형태의 임베딩은 문장에 어떤 단어가 많이 쓰였는지를 파악하여 글쓴이의 의도를 알 수 있습니다. 원-핫 인코딩(One-Hot Encoding)은 여러 기법 중 단어를 표현하는 가장 기본적인 표현 방법입니다.

 원-핫 인코딩은 단어 집합의 크기를 벡터의 차원으로 하고, **표현하고 싶은 단어의 인덱스에 1의 값을 부여하고, 다른 인덱스에는 0을 부여하는 벡터 표현 방식**입니다. 이렇게 표현된 벡터를 원-핫 벡터(One-Hot Vector)라고 합니다. 텍스트를 숫자로 표현하는 대표적인 방법으로 하나의 1과 수많은 0으로 표현하는 방법인데, 예문을 통해 이해해보도록 하겠습니다.

 예를 들어, ”You say goodbye and I say hello.“라는 문서가 있을 때,
“you”,”say”,”goodbye”,”and”,”i”,”hello”,”.” 라는 7개의 단어로 나뉠 수 있습니다.

![원핫벡터](http://ai4school.org/wp-content/uploads/2021/02/%EC%9B%90%ED%95%AB%EB%B2%A1%ED%84%B0.jpg)

 이렇게 표현된 원-핫 벡터는 만약 단어가 20,000개라면 1개만 1이고, 19,999개의 0으로 표현되므로 희소 벡터*이고 벡터를 저장하기 위해 필요한 공간이 계속 늘어나므로 공간의 낭비가 발생하고 컴퓨터의 성능이 저하됩니다. 다른 말로 단어의 갯수만큼 차원 벡터가 만들어 진다고 표현할 수 있습니다.

 또 다른 문제는 단어의 유사도를 표현하지 못한다는 것입니다. 사과, 복숭아, 레몬, 바나나라는 4개의 단어에 대해 원-핫 인코딩을 진행해 각각 [1, 0, 0, 0], [0, 1, 0, 0], [0, 0, 1, 0], [0, 0, 0, 1]이라는 원-핫 벡터를 생성했다고 하면, 사과와 복숭아가 유사하고, 레몬과 바나나가 유사하다는 것을 표현할 수 없습니다.



### 원-핫 인코딩 실습

```python
# GridSearchCV의 refit으로 이미 학습이 된 estimator 반환
estimator = grid_dtree.best_estimator_

#GridSearchCV의 best_estimator_는 이미 최적 하이퍼 파라미터로 학습이 됨
pred = estimator.predict(X_test)
print('테스트 데이터 세트 정확도: {0:.4f}'.format(accuracy_score(y_test,pred)))

from sklearn.preprocessing import LabelEncoder

items = ['TV', '냉장고', '전자레인지', '컴퓨터', '선풍기', '선풍기', '믹서', '믹서']

#LabelEncoder를 객체로 생성한 후, fit()과 transform()으로 레이블인코딩수행.
encoder = LabelEncoder()
encoder.fit(items)
labels = encoder.transform(items)
print('인코딩 변환값 : ', labels)

#print('인코딩 클래스 : ',encoder.classes_)
#print('디코딩 원본값 : ', encoder, encoder.inverse_transform([4,5,2,0,1,1,3,4,2]))

from sklearn.preprocessing import OneHotEncoder
import numpy as np

items = ['TV', '냉장고', '전자레인지', '컴퓨터', '선풍기', '선풍기', '믹서', '믹서']

encoder = LabelEncoder()
encoder.fit(items)
labels = encoder.transform(items)

#2차원 데이터로 변환
labels = labels.reshape(-1,1)

#원-핫 인코딩을 적용
oh_encoder = OneHotEncoder()
oh_encoder.fit(labels)
oh_labels = oh_encoder.transform(labels)
print('원-핫 인코딩 데이터')
print(oh_labels.toarray())
print('원-핫 인코딩 데이터 차원')
print(oh_labels.shape)
```

