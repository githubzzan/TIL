# Today I Learned

> ## 머신러닝

### 기계 학습(머신러닝)은 인공 지능의 한 형태

기계 학습은 [인공 지능](https://www.hpe.com/kr/ko/what-is/artificial-intelligence.html)의 하위 집합으로, 분석 모델 빌딩 프로세스를 효과적으로 자동화하고 시스템이 독립적으로 새로운 시나리오에 적응할 수 있도록 합니다.



인공 신경망이 인간의 의식을 복제할 정도로 정교하게 성장 가능하다는 아이디어에 대한 호불호와 상관없이 기계 학습에 따르는 실질적인 이점이 있습니다.

- **지능적인 빅 데이터 관리** – 기계 학습의 속도와 정교함 없이는 인간과 다른 환경적 요인이 기술과 상호작용하면서 생성하는 데이터의 볼륨과 종류를 처리하기 어려우며 그러한 데이터를 통해 인사이트를 얻는 것도 불가능할 것입니다.
- **스마트 장치** – 건강과 체력 관련 목표를 추적하는 웨어러블 장치부터 자율 주행차와 시간 및 에너지 낭비를 자동으로 줄이는 인프라를 갖춘 "스마트 시티"까지 [IoT(사물 인터넷)](https://www.hpe.com/kr/ko/what-is/internet-of-things.html) 는 엄청난 성장 가능성을 보유하고 있으며, 기계 학습은 데이터의 급격한 증가와 관련된 문제를 해결하는 데 도움이 됩니다.
- **다채로운 소비자 경험** – 기계 학습은 검색 엔진, 웹 애플리케이션 및 기타 기술을 활성화하여 사용자의 선호 사항에 맞춘 결과와 권장 사항을 제공하며 이를 통해 소비자가 만족할 만한 경험을 창출합니다.



> ### 사이킷런

#### 사이킷런이란

\- scikit-learn은 파이썬의 머신러닝 라이브러리입니다.

텐서플로가 딥러닝이라고 하면, 사이킷런은 머신러닝 관련한 기술들을 통일되고 쉬운 인터페이스로 사용할수 있게 해주는 라이브러리라고 생각하시면 됩니다.

\- 이미 전에 정리한 적이 있는데, 간단히 설명하자면,

딥러닝이 머신러닝에 속하는 개념이고, 머신러닝은 인공신경망뿐 아니라 여러 기법이 존재한다고 생각하시면 됩니다.

\- 사이킷런 라이브러리 모듈

\1. 지도학습 모듈 : Naive Bayes, Decision Trees, Support Vector Machine, etc...

\2. 비지도학습 모듈 : Clustering, Gaussian mixture models, etc...

\3. 모델 선택 및 평가를 위한 모듈 : Cross validation, Model evaluation, model save and load func, etc...

\4. 데이터 변환 및 데이터를 불러오기 위한 모듈 : pipeline, feature extraction, preprocessing data,

  dimensionality reduction, etc...

\5. 계산 성능 향상을 위한 모듈

 

\- 사이킷런으로 모델을 구축시, 해결할 문제에 따른 적절한 알고리즘의 경우는 아래의 그림을 참고하여 결정할수 있습니다.

 

![img](https://blog.kakaocdn.net/dn/carb7v/btqCrOB9tvj/wSd8cHOosBofc122FIpZE0/img.png)https://scikit-learn.org/stable/tutorial/machine_learning_map/index.html



> ## 사이킷런으로 수행하는 타이타닉 생존자 예측
>
> [타이타닉 자료 위치](https://www.kaggle.com/heptapod/titanic, "data link")

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline

titanic_df = pd.read_csv(r'C:\Users\동동아\Desktop\동희box\빅데이터수업\머신러닝\타이타닉\titanic\titanic_train.csv')
titanic_df.head(3)

print('\n ### train 데이터 정보 ###  \n')
print(titanic_df.info())
```

```python
titanic_df['Age'].fillna(titanic_df['Age'].mean(),inplace=True)
titanic_df['Cabin'].fillna('N',inplace=True)
titanic_df['Embarked'].fillna('N',inplace=True)
print('데이터 세트 Null 값 갯수 ',titanic_df.isnull().sum())

print(' Sex 값 분포 :\n',titanic_df['Sex'].value_counts())
print('\n Cabin 값 분포 :\n',titanic_df['Cabin'].value_counts())
print('\n Embarked 값 분포 :\n',titanic_df['Embarked'].value_counts())

titanic_df['Cabin'] = titanic_df['Cabin'].str[:1]
print(titanic_df['Cabin'].head(3))

titanic_df.groupby(['Sex','Survived'])['Survived'].count()

sns.barplot(x='Sex', y = 'Survived', data=titanic_df)
sns.barplot(x='Pclass', y='Survived', hue='Sex', data=titanic_df)

# 입력 age에 따라 구분값을 반환하는 함수 설정. DataFrame의 apply lambda식에 사용. 
def get_category(age):
    cat = ''
    if age <= -1: cat = 'Unknown'
    elif age <= 5: cat = 'Baby'
    elif age <= 12: cat = 'Child'
    elif age <= 18: cat = 'Teenager'
    elif age <= 25: cat = 'Student'
    elif age <= 35: cat = 'Young Adult'
    elif age <= 60: cat = 'Adult'
    else : cat = 'Elderly'
    
    return cat

# 막대그래프의 크기 figure를 더 크게 설정 
plt.figure(figsize=(10,6))

#X축의 값을 순차적으로 표시하기 위한 설정 
group_names = ['Unknown', 'Baby', 'Child', 'Teenager', 'Student', 'Young Adult', 'Adult', 'Elderly']

# lambda 식에 위에서 생성한 get_category( ) 함수를 반환값으로 지정. 
# get_category(X)는 입력값으로 'Age' 컬럼값을 받아서 해당하는 cat 반환
titanic_df['Age_cat'] = titanic_df['Age'].apply(lambda x : get_category(x))
sns.barplot(x='Age_cat', y = 'Survived', hue='Sex', data=titanic_df, order=group_names)
titanic_df.drop('Age_cat', axis=1, inplace=True)

from sklearn import preprocessing

def encode_features(dataDF):
    features = ['Cabin', 'Sex', 'Embarked']
    for feature in features:
        le = preprocessing.LabelEncoder()
        le = le.fit(dataDF[feature].astype(str))
        dataDF[feature] = le.transform(dataDF[feature].astype(str))

    return dataDF

titanic_df = encode_features(titanic_df)
titanic_df.head()

from sklearn.preprocessing import LabelEncoder

# Null 처리 함수
def fillna(df):
    df['Age'].fillna(df['Age'].mean(),inplace=True)
    df['Cabin'].fillna('N',inplace=True)
    df['Embarked'].fillna('N',inplace=True)
    df['Fare'].fillna(0,inplace=True)
    return df

# 머신러닝 알고리즘에 불필요한 속성 제거
def drop_features(df):
    df.drop(['PassengerId','Name','Ticket'],axis=1,inplace=True)
    return df

# 레이블 인코딩 수행. 
def format_features(df):
    df['Cabin'] = df['Cabin'].str[:1]
    features = ['Cabin','Sex','Embarked']
    for feature in features:
        le = LabelEncoder()
        le = le.fit(df[feature])
        df[feature] = le.transform(df[feature])
    return df

# 앞에서 설정한 Data Preprocessing 함수 호출
def transform_features(df):
    df = fillna(df)
    df = drop_features(df)
    df = format_features(df)
    return df


# 원본 데이터를 재로딩 하고, feature데이터 셋과 Label 데이터 셋 추출. 
titanic_df = pd.read_csv(r'C:\Users\동동아\Desktop\동희box\빅데이터수업\머신러닝\타이타닉\titanic\titanic_train.csv')
y_titanic_df = titanic_df['Survived']
X_titanic_df= titanic_df.drop('Survived',axis=1)

X_titanic_df = transform_features(X_titanic_df)

from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test=train_test_split(X_titanic_df, y_titanic_df, \
                                                  test_size=0.2, random_state=11)

from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score
from sklearn.metrics import precision_score
from sklearn.metrics import recall_score

# 결정트리, Random Forest, 로지스틱 회귀를 위한 사이킷런 Classifier 클래스 생성
dt_clf = DecisionTreeClassifier(random_state=11)
rf_clf = RandomForestClassifier(random_state=11)
lr_clf = LogisticRegression(random_state=11)

# DecisionTreeClassifier 학습/예측/평가
dt_clf.fit(X_train , y_train)
dt_pred = dt_clf.predict(X_test)
print('DecisionTreeClassifier 정확도: {0:.4f}'.format(accuracy_score(y_test, dt_pred)))

# RandomForestClassifier 학습/예측/평가
rf_clf.fit(X_train , y_train)
rf_pred = rf_clf.predict(X_test)
print('RandomForestClassifier 정확도:{0:.4f}'.format(accuracy_score(y_test, rf_pred)))

# LogisticRegression 학습/예측/평가
lr_clf.fit(X_train , y_train)
lr_pred = lr_clf.predict(X_test)
print('LogisticRegression 정확도: {0:.4f}'.format(accuracy_score(y_test, lr_pred)))



```



