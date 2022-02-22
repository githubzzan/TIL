# Today I Learned

## 1. 인공지능(AI)



AI는 일반적으로 기계 또는 일반적으로 컴퓨터 프로그램을 통해 인간 행동의 구조를 모방하거나 복제하는 것을 가리킵니다. AI라는 용어는 전문가 시스템, 패턴 분석 시스템 또는 로봇 공학 등 다양한 하위 분야에서 사용됩니다. AI 기반의 시스템은 인간의 행동과 의사 결정 구조를 모방하거나 모델링하기 위해 통계학적 알고리즘, 휴리스틱 절차, 인공 신경망(ANN) 또는 그 밖의 머신러닝 변형 등 다양한 방법을 활용합니다.



<iframe height="400" width="555" src="https://www.baslerweb.com/baslermedia/Vision_Campus/deeplearning/01_AI_ML_DL/AI_ML_DL.html" style="box-sizing: inherit; border: 0px;"></iframe>



## 2. 머신러닝



AI의 하위 분야인 머신러닝은 복수의 예시 데이터에서 일반적인 규칙을 도출하기 위한 자동화된 절차로 구성됩니다. 즉, 예시 데이터로부터 규칙이 "학습"됩니다. 이러한 작업은 사전 정의되고 이해하기 쉬운 알고리즘과 규칙을 적용하여 수행되거나, [딥 러닝](https://www.baslerweb.com/ko/service/glossary/?glossaritem=)의 경우 인공 신경망을 사용하여 수행됩니다. 머신러닝은 지도 학습과 비지도 학습으로 구분됩니다. 지도 학습에서 학습을 위한 샘플 데이터는 입력값과 대응되는 예상 결과(예: 분류)를 모두 포함하는 반면, 비지도 학습에서는 시스템이 입력값 자체에서 가능한 결과를 식별합니다.

## 3. 딥 러닝



[딥 러닝](https://www.baslerweb.com/ko/service/glossary/?glossaritem=)은 머신 러닝의 한 방법으로, 학습 과정 동안 인공 신경망으로서 예시 데이터에서 얻은 일반적인 규칙을 독립적으로 구축(훈련)합니다. 특히 머신 비전 분야에서 신경망은 일반적으로 데이터와 예제 데이터에 대한 사전 정의된 결과와 같은 지도 학습을 통해 학습됩니다.



## 딥 러닝의 작동 원리

### 1. 인공 신경망



머신러닝의 한 기법인 [딥 러닝](https://www.baslerweb.com/ko/service/glossary/?glossaritem=)은 특정 형식의 인공 신경망(ANN)을 사용하며, 우선 샘플 데이터를 통한 훈련 작업이 필요합니다. 그 이후에는 훈련된 ANN을 해당 작업에 사용할 수 있습니다. 훈련된 ANN의 사용하는 것을 "추론"이라고 합니다. 추론이 진행되는 동안 ANN은 학습된 규칙에 따라 제공된 데이터에 대한 평가 결과를 다시

보고합니다. 이러한 평가 결과는 입력 이미지에 결함이 있는지 또는 오류가 없는 객체를 나타내는지에 대한 추정 등이 될 수 있습니다.



![img](https://www.baslerweb.com/fp-1591690074/media/editorial/vision_campus/vc_content_half/02_KNN.png)





<iframe height="400" width="555" src="https://www.baslerweb.com/baslermedia/Vision_Campus/deeplearning/03_NeuronsLayersLinks/VC_DL_03_NeuronsLayersLinks.html" style="box-sizing: inherit; border: 0px;"></iframe>

## 2. 뉴런, 계층 및 연결



인공신경망(ANN)은 서로 연결된 "뉴런" 계층으로 구성됩니다. 가장 간단한 경우, 이 계층은 입력 계층과 출력 계층으로 구성됩니다. 뉴런과 연결(link)은 매트릭스에 비유할 수 있습니다. 링크 매트릭스는 입력 매트릭스 개별 값과 결과 매트릭스의 값 사이의 연결을 포함합니다. 연결 매트릭스의 값에는 각 연결의 가중치가 포함됩니다. 입력 값과 논리 매트릭스의 값에 가중치를 반영하면 결과 매트릭스의 개별 값이 생성됩니다.



## 3. 심층 인공 신경망



[딥 러닝](https://www.baslerweb.com/ko/service/glossary/?glossaritem=)이라는 용어는 소위 "심층" 인공 신경망(ANN)에 대한 훈련을 의미합니다. 이 인공 신경망은 입력 및 출력 계층 뿐만 아니라 입력 및 출력을 위한 가시적인 계층 사이에 존재하는 수백 개의 추가적인 "숨겨진" 계층으로 구성됩니다. 숨겨진 계층의 결과 매트릭스는 다음 계층의 입력 매트릭스로 사용됩니다. 이 경우에는 마지막 계층의 출력 매트릭스에만 결과가 포함됩니다.



![img](https://www.baslerweb.com/fp-1591683363/media/ko/editorial/vision_campus/vc_content_half/04_TKNN.png)





![img](https://www.baslerweb.com/fp-1591683522/media/ko/editorial/vision_campus/vc_content_half/05_Training.png)

## 4. 훈련



인공 신경망(ANN)을 훈련할 때 초기 초점은 무작위로 설정됩니다. 그리고 나서 샘플 데이터가 서서히 추가됩니다. 학습 규칙은 입력 데이터 및 예상 결과에 따라 관계의 가중치를 조정하는 데 사용됩니다. 결과에 대한 평가의 정확성을 의미하는 ANN의 궁극적인 효과는 훈련에서 사용되는 예시 데이터에 큰 영향을 받습니다. 일반적으로 훈련 내용에 변동성이 높은 예시 데이터가 많이 포함될수록 추론에서 더 정확한 결과를 얻을 수 있습니다. 매우 유사하거나 반복적인 데이터를 사용하여 훈련을 수행하는 경우, ANN은 예시 데이터와 다른 분야의 데이터를 추정할 수 없게 됩니다. 이 경우 우리는 ANN이 "과적합(overfit)"하다고 표현합니다.



## 딥 러닝의 활용 용도



크기와 관계 없이 쿠키를 싫어하는 사람은 없습니다. 이와 같은 쿠키에 대한 비유는 [딥 러닝](https://www.baslerweb.com/ko/service/glossary/?glossaritem=)의 작동 원리를 보여줍니다. [딥 러닝](https://www.baslerweb.com/ko/service/glossary/?glossaritem=)의 적용 영역은 매우 다양합니다. 특히 머신 비전 분야에서 [딥 러닝](https://www.baslerweb.com/ko/service/glossary/?glossaritem=)은 매우 다양한 작업에 널리 사용되는 방법입니다. 시각 분야에서 [딥 러닝](https://www.baslerweb.com/ko/service/glossary/?glossaritem=)에 맞는 가장 일반적인 작업은 이미지 데이터의 분류 및 세분화를 위한 이미지 분석 작업일 것입니다.





<iframe height="400" width="555" src="https://www.baslerweb.com/baslermedia/Vision_Campus/deeplearning/06_Classification/index.html" style="box-sizing: inherit; border: 0px;"></iframe>

## 1. 이미지 분류



이미지 분류 작업에서는 이미지를 결함이 있는 구성 요소와 정상적인 구성 요소로 분리한 후 결함의 종류에 따라 정렬하거나 빈 이미지를 다른 카테고리에 할당하는 등 이미지들이 서로 다른 클래스에 할당됩니다. 쿠키 제조 과정에서 쿠키에 아무런 문제가 발생하지 않았는지 또는 쿠키의 일부가 부서졌는지를 확인하는 작업이 이뤄지는 것과 유사합니다.



## 2. 이미지 세분화 및 오브젝트 인식



이미지 세분화 작업은 이미지의 각 픽셀을 하나의 클래스에 할당합니다. 이를 통해 이미지에서 여러 가지 오브젝트들을 식별할 수 있습니다. 예를 들어 쇼핑 바구니에서 서로 다른 과일 조각을 식별하거나 교통 표지판, 도로 및 사람을 구별할 수 있습니다. 이미지 세분화를 통해 어셈블리 라인에서 원형, 정사각형, 육각형 등 어떤 모양의 쿠키가 운반되는지 등을 확인할 수 있습니다.



![img](https://www.baslerweb.com/fp-1591690074/media/editorial/vision_campus/vc_content_half/07_Segmentation.png)





<iframe height="400" width="555" src="https://www.baslerweb.com/baslermedia/Vision_Campus/deeplearning/08_Noise_B-A/index.html" style="box-sizing: inherit; border: 0px;"></iframe>

## 3. 화상 처리



[딥 러닝](https://www.baslerweb.com/ko/service/glossary/?glossaritem=)은 이미지 데이터를 처리하고 최적화하는 데 유용하게 활용될 수 있습니다(예: 이미지에 방해가 되는 노이즈 제거 또는 광학 렌즈로 인한 간섭 보정)