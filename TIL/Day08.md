# Today I Learned

> ## 크롤링

- 네이버 연결확인

  ```python
  import requests
  res = requests.get("http://naver.com")
  print("status_code : ", res.status_code)
  --------------------------------------------------------
  import requests
  # res = requests.get("http://naver.com")
  res = requests.get("http://yyy.tistory.com")
  
  print("status_code : ", res.status_code)
  --------------------------------------------------------
  import requests
  # res = requests.get("http://naver.com")
  res = requests.get("http://yyy.tistory.com")
  
  if res.status_code == 200:
      print("정상")
  else:
      print("오류 : ", res.status_code)
  --------------------------------------------------------
  import requests
  res = requests.get("http://naver.com")
  #res = requests.get("http://yyy.tistory.com")
  
  res.raise_for_status()
  print("정상입니다.")
  --------------------------------------------------------
  import requests
  res = requests.get("http://naver.com")
  #res = requests.get("http://yyy.tistory.com")
  
  res.raise_for_status()
  print("정상입니다.")
  print(len(res.text))
  --------------------------------------------------------
  import requests
  res = requests.get("http://naver.com")
  #res = requests.get("http://yyy.tistory.com")
  
  res.raise_for_status()
  print("정상입니다.")
  print(len(res.text))
  print(res.text)
  ```

- 네이버 첫 페이지 받아오기

  ```python
  from urllib.request import urlopen
  
  url = "https://www.naver.com"
  html = urlopen(url)
  print(html.read())
  --------------------------------------------------------
  from urllib.request import urlopen
  from urllib.request import HTTPError
  
  try:
      html = urlopen("http://www.google.com/kim.html")
  except HTTPError as e:
      print(e)
  else:
      print("성공")
  --------------------------------------------------------
  from urllib.request import urlopen
  from urllib.request import HTTPError
  from urllib.request import URLError
  
  try:
      html = urlopen("http://www.google.com/kim.html")
  except HTTPError as e:
      print(e)
  except URLError as e:
      print('The server coult not be found!')
  else:
      print("성공")
  ```

- 크롤러 만들기

  - 뷰티풀솝

    ```python
    import bs4
    
    html_str = "<html><div>hello</div><html>"
    bs_obj = bs4.BeautifulSoup(html_str, "html.parser")
    
    print(type(bs_obj))
    print(bs_obj)
    print(bs_obj.find("div"))
    --------------------------------------------------------
    import bs4
    
    html_str = """
    <html>
        <body>
            <ul>
                <li>hello</li>
                <li>bye</li>
                <li>welcome</li>
            </ul>
        </body>
    </html>
    """
    bs_obj = bs4.BeautifulSoup(html_str, "html.parser")
    ul = bs_obj.find("ul")
    print(ul)
    --------------------------------------------------------
    import bs4 # hello만 출력하기
    
    html_str = """
    <html>
        <body>
            <ul>
                <li>hello</li>
                <li>bye</li>
                <li>welcome</li>
            </ul>
        </body>
    </html>
    """
    bs_obj = bs4.BeautifulSoup(html_str, "html.parser")
    ul = bs_obj.find("ul")
    li = ul.find("li")
    print(li)
    --------------------------------------------------------
    import bs4 #<li>bye</li>만 출력하기
    
    html_str = """
    <html>
        <body>
            <ul>
                <li>hello</li>
                <li>bye</li>
                <li>welcome</li>
            </ul>
        </body>
    </html>
    """
    bs_obj = bs4.BeautifulSoup(html_str, "html.parser")
    ul = bs_obj.find("ul")
    lis = ul.findAll("li")
    print(lis)
    print(lis[1])
    --------------------------------------------------------
    import bs4 #bye만 출력하기
    
    html_str = """
    <html>
        <body>
            <ul>
                <li>hello</li>
                <li>bye</li>
                <li>welcome</li>
            </ul>
        </body>
    </html>
    """
    bs_obj = bs4.BeautifulSoup(html_str, "html.parser")
    ul = bs_obj.find("ul")
    lis = ul.findAll("li")
    print(lis)
    print(lis[1].text)
    ```

  - 데이터 뽑을 때 class 속성 이용하기

    ```python
    import bs4
    
    html_str = """
    <html>
        <body>
            <ul class = "greet">
                <li>hello</li>
                <li>bye</li>
                <li>welcome</li>
            </ul>
            <ul class = "reply">
                <li>ok</li>
                <li>no</li>
                <li>sure</li>
            </ul>
        </body>
    </html>
    """
    bs_obj = bs4.BeautifulSoup(html_str, "html.parser")
    ul = bs_obj.find("ul")
    print(ul)
    --------------------------------------------------------
    import bs4
    
    html_str = """
    <html>
        <body>
            <ul class = "greet">
                <li>hello</li>
                <li>bye</li>
                <li>welcome</li>
            </ul>
            <ul class = "reply">
                <li>ok</li>
                <li>no</li>
                <li>sure</li>
            </ul>
        </body>
    </html>
    """
    bs_obj = bs4.BeautifulSoup(html_str, "html.parser")
    ul = bs_obj.find("ul", {"class":"reply"})
    print(ul)
    --------------------------------------------------------
    import bs4
    html_str = """
    <html>
        <body>
            <ul class = "ko">
                <li>
                    <a bref = "http://naver.com/">네이버</a>
                </li>
                <li>
                    <a bref = "http://www.daum.net/">다음</a>
                </li>
            </ul>
            <ul class = "sns">
                <li>
                    <a bref = "http://www.google.com/">구글</a>
                </li>
                <li>
                    <a bref = "http://www.facebook.com/">페이스북</a>
                </li>
            </ul>
        </body>
    </html>
    """
    bs_obj = bs4.BeautifulSoup(html_str, "html.parser")
    atag = bs_obj.find("a")
    print(atag['bref'])
    ```

  - 웹툰 크롤링

    ```python
    #네이버 열기
    from selenium import webdriver
    
    url = "http://naver.com"
    
    driver = webdriver.Chrome("./chromedriver.exe")
    driver.get(url)
    --------------------------------------------------------
    #네이버 웹툰열기
    from urllib.request import urlopen
    
    url = "https://comic.naver.com/webtoon/weekday"
    html = urlopen(url)
    print(html.read())
    --------------------------------------------------------
    #네이버 웹툰 제목 가지고오기
    import requests
    from bs4 import BeautifulSoup
    
    url = "https://comic.naver.com/webtoon/weekday.nhn"
    res = requests.get(url)
    res.raise_for_status()
    
    soup = BeautifulSoup(res.text, "html.parser")
    print(soup.title)
    print(soup.title.get_text())
    print(soup.title.text)
    
    print(soup.a)
    print(soup.a.attrs)
    print(soup.a["href"])
    --------------------------------------------------------
    #네이버 웹툰 옆에 베너 1~3순위 가져오기 
    import requests
    from bs4 import BeautifulSoup
    
    url = "https://comic.naver.com/webtoon/weekday.nhn"
    res = requests.get(url)
    res.raise_for_status()
    
    soup = BeautifulSoup(res.text, "html.parser")
    r1 = soup.find("li", attrs = {"class":"rank01"})
    print(r1.a)
    r2 = r1.next_sibling.next_sibling
    print(r2.a.get_text())
    r3 = r2.next_sibling.next_sibling
    print(r3.a.text)
    
    pr2 = r3.previous_sibling.previous_sibling
    print(pr2.a.text)
    
    print(r1.parent)
    --------------------------------------------------------
    #웹툰 제목 긁어오기
    webtoons = soup.find_all("a", attrs=("class", "title"))
    for webtoon in webtoons:
        print(webtoon.text)
    --------------------------------------------------------
    #웹툰 홈페이지에서 웹툰 제목들 긁어오기
    import requests
    from bs4 import BeautifulSoup
    
    url = "https://comic.naver.com/webtoon/list?titleId=786537"
    res = requests.get(url)
    res.raise_for_status()
    
    soup = BeautifulSoup(res.text, "html.parser")
    r1 = soup.findAll("td", attrs = {"class":"title"})
    for r2 in r1:
        print(r2.a.text, "")
    --------------------------------------------------------
    #웹툰 평점긁어오기
    import requests
    from bs4 import BeautifulSoup
    
    url = "https://comic.naver.com/webtoon/list?titleId=786537"
    res = requests.get(url)
    res.raise_for_status()
    
    soup = BeautifulSoup(res.text, "html.parser")
    r1 = soup.findAll("div", attrs = {"class":"rating_type"})
    for r2 in r1:
        print(r2.strong.text, "")
    
    ```

  - Selenium

    ```python
    #네이버 로그인창 띄우기
    from selenium import webdriver
    
    url = "http://naver.com"
    driver = webdriver.Chrome(r"C:\Users\동동아\Desktop\동희box\빅데이터수업\jupyter_Notebook\데이터웹크롤링\chromedriver.exe")
    
    driver.get(url)
    element = driver.find_element_by_class_name("link_login")
    print(element)
    element.click
    --------------------------------------------------------
    #네이버 검색창에 컴퓨터 검색
    from selenium import webdriver
    from selenium.webdriver.common.keys import Keys
    
    url = "http://naver.com"
    driver = webdriver.Chrome(r"C:\Users\동동아\Desktop\동희box\빅데이터수업\jupyter_Notebook\데이터웹크롤링\chromedriver.exe")
    
    driver.get(url)
    element = driver.find_element_by_id("query")
    element.send_keys("컴퓨터")
    element.send_keys(Keys.ENTER)
    --------------------------------------------------------
    #네이버 tag_name a를 긁어오기
    from selenium import webdriver
    from selenium.webdriver.common.keys import Keys
    import time
    
    url = "http://naver.com"
    driver = webdriver.Chrome(r"C:\Users\동동아\Desktop\동희box\빅데이터수업\jupyter_Notebook\데이터웹크롤링\chromedriver.exe")
    
    driver.get(url)
    element = driver.find_element_by_tag_name("a")
    elements = driver.find_elements_by_tag_name("a")
    
    for idx, e in enumerate(elements):
        ele = e.get_attribute('href')
        print(ele)
        time.sleep(0.5)
    --------------------------------------------------------
    #다음에서 인기영화 검색하기
    from selenium import webdriver
    from selenium.webdriver.common.keys import Keys
    
    url = "http://daum.net"
    driver = webdriver.Chrome(r"C:\Users\동동아\Desktop\동희box\빅데이터수업\jupyter_Notebook\데이터웹크롤링\chromedriver.exe")
    
    driver.get(url)
    element = driver.find_element_by_id("q")
    element.send_keys("인기영화")
    #element.send_keys(Keys.ENTER)
    element = driver.find_element_by_xpath("//*[@id='daumSearch']/fieldset/div/div/button[2]") #검색을 마우스 클릭으로 하는법
    element.click()
    --------------------------------------------------------
    #네이버 로그인하기(검열걸림)
    from selenium import webdriver
    
    url = "http://naver.com"
    driver = webdriver.Chrome(r"C:\Users\동동아\Desktop\동희box\빅데이터수업\jupyter_Notebook\데이터웹크롤링\chromedriver.exe")
    
    driver.get(url)
    element = driver.find_element_by_class_name("link_login")
    element.click()
    element = driver.find_element_by_id("id")
    element.send_keys("aaaaaaa123")
    element = driver.find_element_by_id("pw")
    element.send_keys("bbbb213")
    #element.send_keys(Keys.ENTER)
    element = driver.find_element_by_xpath("//*[@id='log.login']/span") #검색을 마우스 클릭으로 하는법
    element.click()
    --------------------------------------------------------
    #네이버 로그인 타자로 자동으로 치기(검열 안걸림)
    import pyperclip
    from selenium import webdriver
    from selenium.webdriver.common.keys import Keys
    
    
    
    url = "http://naver.com"
    driver = webdriver.Chrome(r"C:\Users\동동아\Desktop\동희box\빅데이터수업\jupyter_Notebook\데이터웹크롤링\chromedriver.exe")
    
    try:
        driver.get(url)
        element = driver.find_element_by_class_name("link_login")
        element.click()
    
        pyperclip.copy("thdusdl213")
        driver.find_element_by_id("id").send_keys(Keys.CONTROL, 'v')
        pyperclip.copy("fpwltmxkdtm8&")
        driver.find_element_by_id("pw").send_keys(Keys.CONTROL, 'v')
        driver.find_element_by_id("pw").send_keys(Keys.ENTER)
        
    except Exception as e:
        print(e)
    finally:
        print("성공")
    ```

    