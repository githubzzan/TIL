# Today I Learned

> ### 알고리즘

#### 정의

- 정밀성 : 변하지 않는 명확한 작업 단계를 가져야 한다.
- 유일성 : 각 단계마다 명확한 다음 단계를 가져야 한다.
- 타당성 : 구현할 수 있고 실용적이어야 한다.
- 입력  : 정의된 입력을 받아들일 수 있어야 한다.
- 출력 : 답으로 출력을 내보낼 수 있어야 한다.
- 유한성 : 특정 수의 작업 이후에 정지해야 한다.
- 일반성 : 정의된 입력들에 일반적으로 적용할 수 있어야 한다.



#### 구현

알고리즘은 자연어, 의사코드, 순서도, 프로그래밍언어, 인터프리터가 작업하는 제어테이블, 유한상태기계의 상태도 등으로 표현할 수 있다. 다음은 알고리즘 개발의 정형적인 단계이다.

문제 정의 → 모델 고안 → 명세 작성 → 설계 → 검증 → 분석 (복잡도 등) → 구현 → 테스트 → 문서화
알고리즘을 설계하는 기술에는 운용과학의 방법, 설계짜임새를 써먹는 방법 등이 있다. 대부분의 알고리즘은 컴퓨터 프로그램으로 구현되지만, 전기 회로나 생물학적 신경회로를 사용하기도 한다.



#### 분류

- 구현 : 재귀적 알고리즘, 연역적 알고리즘, 결정론적 알고리즘, 근사 알고리즘, 양자 알고리즘 등.
- 설계 : 무차별 대입 공격, 분할 정복 알고리즘, 그래프 순회, 분기 한정법, 확률적 알고리즘, 리덕션, 백트래킹 등.
- 최적화 문제 : 선형 계획법, 동적 계획법, 탐욕 알고리즘, 휴리스틱 함수 등.
- 이론적 분야 : 검색 알고리즘, 정렬 알고리즘, 수치 알고리즘, 그래프 알고리즘, 문자열 알고리즘, 암호학적 알고리즘, 기계 학습, 데이터 압축 등.



#### 복잡성

입력의 크기가 {\displaystyle n}![n](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b)일 경우, [점근 표기법](https://ko.wikipedia.org/wiki/점근_표기법) {\displaystyle O}![O](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d70e1d0d87e2ef1092ea1ffe2923d9933ff18fc)를 사용하여 다음과 같이 나타낸다.

- {\displaystyle O(1)}![O(1)](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) : {\displaystyle n}![n](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b)에 관계없이 일정 시간 이하에 수행되는 알고리즘이다. 예) 파일의 첫 번째 바이트가 [널](https://ko.wikipedia.org/wiki/널_문자)(null)인지 검사하는 것.

- {\displaystyle O(\log n)}![{\displaystyle O(\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/aae0f22048ba6b7c05dbae17b056bfa16e21807d) : {\displaystyle \log _{2}n}![{\displaystyle \log _{2}n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d74677fc45e0d926639433586327cbc2982eae89)에 비례하는 시간 이하에 수행되는 알고리즘이다. 예) [이진 탐색](https://ko.wikipedia.org/wiki/이진_탐색).

- {\displaystyle O(n)}![O(n)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) : {\displaystyle n}![n](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b)에 비례하는 시간 이하에 수행되는 알고리즘이다. 예) [기수 정렬](https://ko.wikipedia.org/wiki/기수_정렬).

- {\displaystyle O(n\log n)}![{\displaystyle O(n\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1) : {\displaystyle n}![n](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b)에 대략 비례할 수 있는 시간 이하에 수행되는 알고리즘이다. 예) [정렬 알고리즘](https://ko.wikipedia.org/wiki/정렬_알고리즘).

- {\displaystyle O(n^{2})}![O(n^{2})](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) : {\displaystyle n^{2}}![n^2](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac9810bbdafe4a6a8061338db0f74e25b7952620)에 비례하는 시간 이하에 수행되는 알고리즘이다. 예) [최장 공통 부분 수열](https://ko.wikipedia.org/wiki/최장_공통_부분_수열) 문제.

- {\displaystyle O(n^{3})}![{\displaystyle O(n^{3})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6b04f5c5cfea38f43406d9442387ad28555e2609) : {\displaystyle n^{3}}![{\displaystyle n^{3}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3e9d1a52e455a7a5272a345b2697e35f1579b681)에 비례하는 시간 이하에 수행되는 알고리즘이다. 예) [행렬 곱셈](https://ko.wikipedia.org/wiki/행렬_곱셈).

- {\displaystyle O(a^{n})}![{\displaystyle O(a^{n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/aa1d036368e1a388a69b459ae4d947703d3fd337) : {\displaystyle 2^{n}}![2^{n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8226f30650ee4fe4e640c6d2798127e80e9c160d)과 같은 꼴의 수행 시간 이하에 수행되는 알고리즘이다. 예) [충족 가능성](https://ko.wikipedia.org/wiki/충족_가능성_문제) 문제.

- {\displaystyle O(n!)}![{\displaystyle O(n!)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/12921c489714d475a454bd39ef644d4334d97113) : {\displaystyle n!}![n!](https://wikimedia.org/api/rest_v1/media/math/render/svg/bae971720be3cc9b8d82f4cdac89cb89877514a6) 즉 {\displaystyle n\times (n-1)\times (n-2)\times ...\times 1}![{\displaystyle n\times (n-1)\times (n-2)\times ...\times 1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f8bf87f1527d263cbbd93bae916efab1100ceb1b)과 같은 꼴의 수행 시간 이하에 수행되는 알고리즘이다. 예) 배열의 모든 [순열](https://ko.wikipedia.org/wiki/순열)을 검사하는 것.

대문자 O 표기법의 정의상 아래의 복잡도는 그 위의 복잡도를 포함하므로, 대부분의 알고리즘은 {\displaystyle O(n!)}![{\displaystyle O(n!)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/12921c489714d475a454bd39ef644d4334d97113)의 수행 시간을 가진다.