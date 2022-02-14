# Today I Learned

> 인구 공공데이터 프로젝트

- 우리 동네 인구 구조 시각화하기

  - 데이터 가져오기

  ```python
  import csv
  f = open('./202112_202112_연령별인구현황_월간.csv', 'r', encoding='cp949')
  data = csv.reader(f)
  for row in data :
      print(row)
  ```

  

  - 1번쨰 신도림 지역 사는사람 데이터 가져오기

    ```python
    import csv
    f = open('./202112_202112_연령별인구현황_월간.csv', 'r', encoding='cp949')
    data = csv.reader(f)
    for row in data :
        if '신도림' in row[0]:
            print(row)
        
    ```

  - 신도림 지역 사는사람 데이터 모두 가져오기

    ``` python
    import csv
    f = open('./202112_202112_연령별인구현황_월간.csv', 'r', encoding='cp949')
    data = csv.reader(f)
    for row in data :
        if '신도림' in row[0]:
            for i in row[3:]:
                print(row)
        
    ```

  - 선 그래프로 만들기

    ```python
    import matplotlib.pyplot as plt
    plt.style.use('ggplot')
    plt.plot(result)
    plt.show()
    ```

  - 막대그래프로 만들기

    ```python
    import matplotlib.pyplot as plt
    plt.bar([0,1,2,4,6,10], [1,2,3,5,6,7])
    plt.show()
    ```

  - 막대그래프로 만들기(제목포함)

    ```python
    import csv
    f = open('./gender.csv', 'r', encoding='cp949')
    data = csv.reader(f)
    m = []
    w = []
    for row in data:
        if '신도림' in row[0]:
            for i in row[3:104]:
                m.append(int(i))
            for i in row[106:]:
                w.append(-(int(i)))
    
    import matplotlib.pyplot as plt
    plt.rc('font', family='Malgun Gothic')
    plt.title('신도림 지역의 남녀 성별 인구 분포')
    plt.barh(range(101), m, label='남성')
    plt.barh(range(101), w, label='여성')
    plt.legend()
    plt.show()
    ```

  - 원그래프로 만들기

    ``` python
    import matplotlib.pyplot as plt
    plt.pie([10,20])
    plt.show()
    ```

  - 원 그래프로 만들기(부가요소 포함)

    ``` python
    import matplotlib.pyplot as plt
    plt.rc('font', family='Malgun Gothic')
    size = [2441,2312,1031,1233]
    label = ['A형','B형','AB형','O형']
    plt.axis('equal')
    plt.pie(size, labels=label, autopct='%.1f%%')
    plt.legend()
    plt.show()
    ```

  - 원 그래프로 만들기(부가요소 추가포함)

    ``` python
    import matplotlib.pyplot as plt
    plt.rc('font', family='Malgun Gothic')
    size = [2441,2312,1031,1233]
    label = ['A형','B형','AB형','O형']
    color = ['darkmagenta','deeppink','hotpink','pink']
    plt.axis('equal')
    plt.pie(size, labels=label, autopct='%.1f%%', colors=color, explode=(0,0,0.1,0))
    plt.legend()
    plt.show()
    ```

  - 점 그래프 표현하기(점크기 표현)

    ``` python
    import matplotlib.pyplot as plt
    plt.scatter([1,2,3,4], [10,30,20,40], s=[100,200,250,300], c =['red','blue','green','gold'])
    plt.show()
    ```

    