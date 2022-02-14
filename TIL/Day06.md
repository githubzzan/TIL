

# Today I Learned

## 기온공공 데이터

> ### 기온 데이터를 다양하게 시각화하기

- 데이터 다운로드 
  - 기상자료 개방포털(https://data.kma.go.kr/)
- 서울 기온 데이터 분석

``` python
import csv
f = open('seoul.csv','r', encoding='cp949')
data = csv.reader(f, delimiter=',')
print(data)
f.close()
```

- 데이터 출력하기

  ``` python
  import csv
  f = open('seoul.csv','r', encoding='cp949')
  data = csv.reader(f, delimiter=',')
  for row in data :
      print(row)
  f.close()
  ```

- 헤더 저장하기

``` python
import csv
f = open('seoul.csv','r', encoding='cp949')
data = csv.reader(f)
header = next(data)
for row in data :
    row[-1] = float(row[-1])
    print(row)
f.close()
```

- 서울의 가장 더웟던 날 구하기

  ``` python
  for row in data :
      if row[-1] == '' :
          row[-1] = -999
      row[-1] = float(row[-1])
      
      if max_temp < row[-1] :
          max_date = row[0]
          max_temp = row[-1]
  ```

  

## 데이터의 시각화

> ### 기본그래프 그리기

- 기본 그래프 그리기(선그래프)

  ``` python
  import matplotlib.pyplot as plt
  plt.plot([10,20,30,40])
  plt.show()
  ```

- 기본 그래프 그리기(선그래프)

  ``` python
  import matplotlib.pyplot as plt
  plt.plot([1,2,3,4],[12,43,25,15])
  plt.show()
  ```

- 제목 넣기

  ```python
  import matplotlib.pyplot as plt
  plt.title('plotting') #제목
  plt.plot([10,20,30,40])
  plt.show()
  ```

- 그래프에 옵션 추가하기

``` python
plt.title('legend')
plt.plot([10,20,30,40], label='asc') #옵션
plt.plot([40,30,20,10], label='desc') #옵션
plt.legend()
plt.show()

plt.title('legend')
plt.plot([10,20,30,40], label='asc') #옵션
plt.plot([40,30,20,10], label='desc') #옵션
plt.legend(loc=2) #옵션위치변경
plt.show()
```

- 그래프에 선 색상 추가하기

  ``` python
  plt.title('color')
  plt.plot([10,20,30,40], color ='skyblue', label='skyblue')
  plt.plot([40,30,20,10], 'pink',label='pink')
  plt.legend()
  plt.show()
  ```

- 그래프 선 모양 변경하기

  ```python
  plt.title('linestyle')
  plt.plot([10,20,30,40], color ='r', linestyle='--', label='dashed')
  plt.plot([40,30,20,10], color = 'g', ls=':', label='dotted')
  plt.legend()
  plt.show()
  ```

- 마커모양 변경하기

  ```python
  plt.title('marker')
  plt.plot([10,20,30,40], color ='r.',label='dashed')
  plt.plot([40,30,20,10], color = 'g^',label='dotted')
  plt.legend()
  plt.show()
  ```

> ### 내 생일의 기온 변화를 그래프로 그리기

- 날짜 추출하기

  ```python
  for row in data :
      if row[-1] != '' :
          if row[0].split('-')[1] == '01' and row[0].split('-')[2] == 10:
              result.append(float(row[-1]))
  ```

- 데이터 시각화

  ```python
  for row in data :
      if row[-1] != '' and row [-2] != '' :
          if 1983 <= int(row[0].split('-')[0]) :
              if row[0].split('-')[1] == '01' and row[0].split('-')[2] == '10' :
                  
                  high.append(float(row[-1]))
                  low.append(float(row[-2]))
  plt.plot(high, 'hotpink')
  plt.plot(low, 'skyblue')
  plt.show()
  ```

- 데이터를 다양하게 시각화 하기

  - 히스토그램

    ```python
    import matplotlib.pyplot as plt
    plt.hist([1,1,2,3,4,5,6,6,7,8,10])
    plt.show()
    ```

  - 히스토그램 주사위

    ```python
    import random
    dice = []
    for i in range(100) :
        dice.append(random.randint(1,6))
    print(dice)
    ```

  - 기온 데이터를 히스토그램으로 표현하기

    ```python
    f = open('seoul.csv')
    data = csv.reader(f)
    next(data)
    aug = []
    
    for row in data :
        month = row[0].split('-')[1]
        if row[-1] != '' :
            if month == '08' :
                aug.append(float(row[-1]))
    plt.hist(result, bins=100, color='r')
    plt.show()
    ```

  - 1월부터 8월의 데이터를 히스토그램으로 시각화하기

    ```python
    f = open('seoul.csv')
    data = csv.reader(f)
    next(data)
    aug = []
    jan = []
    
    for row in data :
        month = row[0].split('-')[1]
        if row[-1] != '' :
            if month == '08' :
                aug.append(float(row[-1]))
            elif month == '01' :
                jan.append(float(row[-1]))
                
    plt.hist(aug, bins=100, color='r', label='Aug')
    plt.hist(jan, bins=100, color='b', label='Jan')
    plt.show()
    ```

  - 기온 데이터를 상자 그림으로 표현

    ``` python
    import matplotlib.pyplot as plt
    import random
    result = []
    for i in range(13) :
        result.append(random.randint(1,1000))
    print(sorted(result))
    
    plt.boxplot(result)
    plt.show()
    ```

  - 기온 데이터를 상자 그림으로 표현(1월부터 12월까지 한번에 담기)

    ```python
    import csv
    f = open('seoul.csv')
    data = csv.reader(f)
    next(data)
    
    month = [[],[],[],[],[],[],[],[],[],[],[],[]]
    
    for row in data :
        if row[-1] != '' :
            month[int(row[0].split('-')[1])-1].append(float(row[-1]))
                
    plt.boxplot(month)
    plt.show()
    ```

    