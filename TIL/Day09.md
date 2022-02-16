# Today I Learned

### 주가 정보예측 Project

``` python
from dataclasses import replace
import requests
import bs4
import pymysql

################
#클래스 부분
################

# 클래스 선언
class SQLmanagement :
    # 클래스 선언시 데이터베이스 이름과 패스워드가 필요하며, 데이터베이스가 없을 시 생성한다.
    def __init__(self,dbname,passwords):
        self.password = passwords
        self.dbname = dbname
        conn, cur = None,None
        conn = pymysql.connect(host='localhost',user = 'root', password=self.password ,charset='utf8')
        cur = conn.cursor()
        cur.execute("CREATE DATABASE IF NOT EXISTS {}".format(self.dbname))
        conn.commit()
        conn.close()

    # 데이터베이스와 연결하는 함수. useQuery(), dataLoad() 함수를 쓰기전 사용해야함.
    def openDB(self):
        self.conn = None
        self.cur = None
        self.conn = pymysql.connect(host='localhost',user = 'root', password=self.password ,db = self.dbname,charset='utf8')
        self.cur = self.conn.cursor()

    # opneDB()를 사용하고 난 이후에 꼭 사용해야함. DB를 닫아줘야 에러가 나지 않음.
    def closeDB(self):
        self.conn.commit()
        self.conn.close()

    # 함수 안에 쿼리문을 작성하면 실행시켜주는 함수.
    def useQuery(self,queries):
        self.query = queries
        self.cur.execute(self.query)

    # 테이블 안에 모든 데이터를 불러오는 함수. 리스트를 반환한다.
    def selectTableData(self,tableName):
        data = []
        self.useQuery("SELECT * FROM {}".format(tableName))
        while (True) :
            row = self.cur.fetchone()
            if row == None :
                break
            data.append(row)
        return data

    # 주가 정보가 들어있는 테이블에서 회사이름, 시작날짜, 종료날짜를 설정하면 해당 기간의 주가정보를 보여주는 함수
    def selectDateData(self, tableName, companyName, startDate, endDate):
        data = []
        self.useQuery("SELECT * FROM {} WHERE companyName = '{}' and date >= '{}' AND date <= '{}'".
            format(tableName,companyName,startDate,endDate))
        while (True) :
            row = self.cur.fetchone()
            if row == None :
                break
            data.append(row)
        return data


################
#함수 부분
################

# 주가 코드가 6자리가 아닐경우 6자리로 만들기 위한 코드.
def codeTune(data):
    stockdata = []
    for i in range(len(data)):
        if len(data[i][1]) == 3:
            code = '000' + data[i][1]
        elif len(data[i][1]) == 4:
            code = '00' + data[i][1]
        elif len(data[i][1]) == 5:
            code = '0' + data[i][1]
        else :
            code = data[i][1]
        stockdata.append([data[i][0],code])
    return stockdata

# 페이지별로 데이터를 크롤링하는 함수 page는 몇 페이지까지 데이터를 받아올 것인가.
def getPages(data,page,url,header):
    pagedata = []
    for i in range(page):
        pagedata.append(getPageData(data,i+1,url,header))
    return pagedata

# 특정 페이지의 주식정보를 크롤링하는 함수. data는 코드를 의미, page는 현재 페이지를 의미
def getPageData(data,page,url,header):
    url2 = url.format(data,page)
    res = requests.get(url2,headers=header)
    res.raise_for_status() 

    # 객체 생성
    bs = bs4.BeautifulSoup(res.text,"html.parser")

    # 주가정보 긁어오기
    table = bs.find("table",{"class":"type2"})
    tr = table.findAll("tr",{"onmouseover":"mouseOver(this)"})

    # tr의 길이만큼의 이중 지능리스트 생성
    data = [ [] for i in range(len(tr))]

    # 모든 텍스트 정보 가져오기
    for i in range(len(tr)):
        td = tr[i].findAll("td")
        for s in range(len(td)):
            data[i].append(td[s].text.strip())
    return data



#########################################################################
# 데이터를 크롤링하는 파일. 데이터베이스에 데이터를 최초로 넣을 때만 실행 #
#########################################################################
import stockproject as sp
import pandas as pd


# 사용할 데이터베이스 정보. pw는 각자 데이터베이스에 맞는 pw 사용
db = 'INVESTAR'
pw = '1111'
companyTable = 'company_info'
stockTable = 'daily_price'

# 데이터를 가져오기 위한 정보. header는 각자 컴퓨터에 맞는 header 사용
header = {'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Whale/3.12.129.46 Safari/537.36'}
url = "https://finance.naver.com/item/sise_day.nhn?code={}&page={}"
page = 1

# 클래스 선언과 동시에 db생성
st = sp.SQLmanagement(db,pw)

# 상장사 데이터를 넣을 테이블 만들기
st.openDB()
st.useQuery('CREATE TABLE IF NOT EXISTS {} (cname char(15), ccode char(6))'.format(companyTable))
st.closeDB()

# 주가 데이터를 넣을 테이블 만들기
st.openDB()
query = "CREATE TABLE IF NOT EXISTS {} (companyName VARCHAR(15), date DATE, cp VARCHAR(15), ade VARCHAR(15), mp VARCHAR(15), hp VARCHAR(15), rp VARCHAR(15), tv VARCHAR(15),PRIMARY KEY(companyName, date));"
st.useQuery(query.format(stockTable))
st.closeDB()

# 테이블에 상장사 데이터 넣기
st.openDB()
url3 = "http://kind.krx.co.kr/corpgeneral/corpList.do?method=download&searchType=13"
tables = pd.read_html(url3)
comp_data = tables[0][['회사명','종목코드']]
for i in range(len(comp_data)):
    st.useQuery("INSERT INTO {} VALUES('{}','{}')".format(companyTable, comp_data.iloc[i][0], comp_data.iloc[i][1]))
st.closeDB()

# 상장사 데이터 불러오기
st.openDB()
comp_data = st.selectTableData(companyTable)
st.closeDB()

# 데이터 튜닝
comp_data = sp.codeTune(comp_data)

# 상장사 데이터를 이용해 주가정보 가져오기
st.openDB()
for row in range(len(comp_data)):
    stdata = sp.getPages(comp_data[row][1],page,url,header) # 데이터 크롤링
    for p in range(page):
        for i in range(10):
            st.useQuery("INSERT IGNORE INTO {} VALUES('{}', '{}', '{}', '{}', '{}', '{}', '{}', '{}')".
                format(stockTable, comp_data[row][0], stdata[p][i][0], stdata[p][i][1], stdata[p][i][2], \
                    stdata[p][i][3], stdata[p][i][4], stdata[p][i][5], stdata[p][i][6]))
st.closeDB()

###################
#주가정보확인
###################

from pymysql import DataError
from sklearn.exceptions import DataDimensionalityWarning
import stockproject as sp

# 사용할 데이터베이스 정보. pw는 각자 데이터베이스에 맞는 pw 사용
db = 'INVESTAR'
pw = '1111'
companyTable = 'company_info'
stockTable = 'daily_price'

# 데이터를 가져오기 위한 정보. header는 각자 컴퓨터에 맞는 header 사용
header = {'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) \
    Chrome/96.0.4664.110 Whale/3.12.129.46 Safari/537.36'}
url = "https://finance.naver.com/item/sise_day.nhn?code={}&page={}"

# 클래스 선언과 동시에 db생성
st = sp.SQLmanagement(db,pw)

# 원하는 회사의 원하는 날짜 데이터 뽑기
st.openDB()
datedata = st.selectDateData(stockTable,"DL","2022-01-21","2022-02-08")
st.closeDB() 

for i in range(len(datedata)):
    print(datedata[i])
```

