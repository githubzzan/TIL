#  Today I Learned

## 판다스(Pandas)

* 시리즈

  * 시리즈 만들기

    ```dict_data = {'a' : 1, 'b':2, 'c':3}```

  * 인덱스 구조

    * 인덱스 배열 : Series객체.index
    * 데이터 값 배열 : Series객체.values

  * 리스트 => 시리즈로 변환

    ```python
    list_data = ['2019-01-02', 3.14, 'ABC', 100, True]
    sr = pd.Series(list_data)
    ```

  * 튜플 -> 시리즈로 변환

    ```python
    tup_data = ('민수', '2017-04-08', '여', True)
    sr = pd.Series(tup_data, index = ['이름', '생년월일', '성별', '학생여부'])
    ```

    

## 데이터프레임

* 데이터프레임 만들기

  ```python
  ditc_data = {'A':[1,2,3], 'B':[4,5,6]}
  df = pd.DataFrame(dict_data)
  ```

  

* 행/열 삭제

  * 행 삭제 : DataFrame객체.drop(행 인덱스 또는 배열, axis=0)
  * 열 삭제 : DataFrame객체.drop(열 이름 또는 배열, axis=1)

* 행 선택

  * loc : 인덱스 이름
  * iloc : 정수형 위치 인덱스

* 열 선택

  * DataFrame 객체["열 이름"] or DataFrame 객체.열 이름

* 원소 선택

  ```python
  exam_data = {'이름' : ['서준', '우현', '인아'],
              '수학' : [ 90, 80, 70]}
  df = pd.DataFrame(exam_data)
  df.set_index('이름', inplace=True)
  
  
  
  a = df.loc['서준','수학']
  b = df.iloc[0,1]
  ```

  

* 열 추가

  * DataFrame 객체[ '추가하려는 열 이름'] = 데이터 값

* 행 추가

  * DataFrame 객체[ '새로운 행 이름'] = 데이터 값 (또는 배열)

* 원소 값 변경

  * DataFrame 객체의 일부분 또는 원소를 선택 = 새로운 값

* 행, 열의 위치 바꾸기

  * df = df.transpos()
  * df = df.T

* 특정 열을 행 인덱스로 설정

  * DataFrame 객체.set_index( [ '열 이름'] 또는 '열 이름')



