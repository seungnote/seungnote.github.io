---
title:  "[Python] 데이터핸들링-날짜데이터(datatime)QUIZ" 

categories:
  - quiz
tags:
  - [Python,ADP,quiz,class101]

toc: true
toc_sticky: true

date: 2022-11-30

---

# 날짜 데이터 전처리 과제 
- 데이터 : "6.세종시_오피스텔(매매)_실거래가.csv"


```python
import pandas as pd 
df_sejong = pd.read_csv("D:/anaconda/00.studying/data/6.세종시_오피스텔(매매)_실거래가.csv",encoding='utf8')
```


```python
df_sejong
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>계약년월</th>
      <th>계약일</th>
      <th>시군구</th>
      <th>본번</th>
      <th>부번</th>
      <th>단지명</th>
      <th>전용면적(㎡)</th>
      <th>거래금액(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>해제사유발생일</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201701</td>
      <td>4</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,000</td>
      <td>14</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201701</td>
      <td>6</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,500</td>
      <td>11</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201702</td>
      <td>5</td>
      <td>세종특별자치시 나성동</td>
      <td>713</td>
      <td>0</td>
      <td>세진이너스빌</td>
      <td>34.15</td>
      <td>13,000</td>
      <td>8</td>
      <td>2013</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>201702</td>
      <td>7</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,500</td>
      <td>4</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201702</td>
      <td>7</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,000</td>
      <td>4</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>340</th>
      <td>202012</td>
      <td>20</td>
      <td>세종특별자치시 나성동</td>
      <td>756</td>
      <td>0</td>
      <td>리치먼드시티세종</td>
      <td>26.18</td>
      <td>16,410</td>
      <td>6</td>
      <td>2020</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>341</th>
      <td>202012</td>
      <td>21</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>24.22</td>
      <td>8,600</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>342</th>
      <td>202012</td>
      <td>23</td>
      <td>세종특별자치시 나성동</td>
      <td>756</td>
      <td>0</td>
      <td>리치먼드시티세종</td>
      <td>26.18</td>
      <td>15,340</td>
      <td>7</td>
      <td>2020</td>
      <td>20210118.0</td>
    </tr>
    <tr>
      <th>343</th>
      <td>202012</td>
      <td>23</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>2차푸르지오시티</td>
      <td>30.48</td>
      <td>11,500</td>
      <td>9</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>344</th>
      <td>202012</td>
      <td>24</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>44.84</td>
      <td>15,600</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>345 rows × 11 columns</p>
</div>



### 아래와 같이 계약년월을 datetime으로 변경하세요. 


```python
df_sejong.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 345 entries, 0 to 344
    Data columns (total 11 columns):
     #   Column    Non-Null Count  Dtype  
    ---  ------    --------------  -----  
     0   계약년월      345 non-null    int64  
     1   계약일       345 non-null    int64  
     2   시군구       345 non-null    object 
     3   본번        345 non-null    int64  
     4   부번        345 non-null    int64  
     5   단지명       345 non-null    object 
     6   전용면적(㎡)   345 non-null    float64
     7   거래금액(만원)  345 non-null    object 
     8   층         345 non-null    int64  
     9   건축년도      345 non-null    int64  
     10  해제사유발생일   9 non-null      float64
    dtypes: float64(2), int64(6), object(3)
    memory usage: 29.8+ KB
    


```python
from datetime import datetime
from datetime import timedelta
```


```python
df_sejong['계약년월'] = df_sejong['계약년월'].astype(str)
df_sejong['계약일'] = df_sejong['계약일'].astype(str)
df_sejong['계약년월']=df_sejong['계약년월']+df_sejong['계약일']
```


```python
df_sejong['계약년월'] = df_sejong['계약년월'].map(lambda x : datetime.strptime(x, "%Y%m%d"))
df_sejong
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>계약년월</th>
      <th>계약일</th>
      <th>시군구</th>
      <th>본번</th>
      <th>부번</th>
      <th>단지명</th>
      <th>전용면적(㎡)</th>
      <th>거래금액(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>해제사유발생일</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-01-04</td>
      <td>4</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,000</td>
      <td>14</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-01-06</td>
      <td>6</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,500</td>
      <td>11</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-02-05</td>
      <td>5</td>
      <td>세종특별자치시 나성동</td>
      <td>713</td>
      <td>0</td>
      <td>세진이너스빌</td>
      <td>34.15</td>
      <td>13,000</td>
      <td>8</td>
      <td>2013</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017-02-07</td>
      <td>7</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,500</td>
      <td>4</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-02-07</td>
      <td>7</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,000</td>
      <td>4</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>340</th>
      <td>2020-12-20</td>
      <td>20</td>
      <td>세종특별자치시 나성동</td>
      <td>756</td>
      <td>0</td>
      <td>리치먼드시티세종</td>
      <td>26.18</td>
      <td>16,410</td>
      <td>6</td>
      <td>2020</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>341</th>
      <td>2020-12-21</td>
      <td>21</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>24.22</td>
      <td>8,600</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>342</th>
      <td>2020-12-23</td>
      <td>23</td>
      <td>세종특별자치시 나성동</td>
      <td>756</td>
      <td>0</td>
      <td>리치먼드시티세종</td>
      <td>26.18</td>
      <td>15,340</td>
      <td>7</td>
      <td>2020</td>
      <td>20210118.0</td>
    </tr>
    <tr>
      <th>343</th>
      <td>2020-12-23</td>
      <td>23</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>2차푸르지오시티</td>
      <td>30.48</td>
      <td>11,500</td>
      <td>9</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>344</th>
      <td>2020-12-24</td>
      <td>24</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>44.84</td>
      <td>15,600</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>345 rows × 11 columns</p>
</div>



## 계약년월을 아래와 같이 문자열로 다시 변경하세요. 


```python
df_sejong['계약년월']=df_sejong['계약년월'].dt.strftime('%Y_%m_%d')
df_sejong
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>계약년월</th>
      <th>계약일</th>
      <th>시군구</th>
      <th>본번</th>
      <th>부번</th>
      <th>단지명</th>
      <th>전용면적(㎡)</th>
      <th>거래금액(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>해제사유발생일</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017_01_04</td>
      <td>4</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,000</td>
      <td>14</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017_01_06</td>
      <td>6</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,500</td>
      <td>11</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017_02_05</td>
      <td>5</td>
      <td>세종특별자치시 나성동</td>
      <td>713</td>
      <td>0</td>
      <td>세진이너스빌</td>
      <td>34.15</td>
      <td>13,000</td>
      <td>8</td>
      <td>2013</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017_02_07</td>
      <td>7</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,500</td>
      <td>4</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017_02_07</td>
      <td>7</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,000</td>
      <td>4</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>340</th>
      <td>2020_12_20</td>
      <td>20</td>
      <td>세종특별자치시 나성동</td>
      <td>756</td>
      <td>0</td>
      <td>리치먼드시티세종</td>
      <td>26.18</td>
      <td>16,410</td>
      <td>6</td>
      <td>2020</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>341</th>
      <td>2020_12_21</td>
      <td>21</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>24.22</td>
      <td>8,600</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>342</th>
      <td>2020_12_23</td>
      <td>23</td>
      <td>세종특별자치시 나성동</td>
      <td>756</td>
      <td>0</td>
      <td>리치먼드시티세종</td>
      <td>26.18</td>
      <td>15,340</td>
      <td>7</td>
      <td>2020</td>
      <td>20210118.0</td>
    </tr>
    <tr>
      <th>343</th>
      <td>2020_12_23</td>
      <td>23</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>2차푸르지오시티</td>
      <td>30.48</td>
      <td>11,500</td>
      <td>9</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>344</th>
      <td>2020_12_24</td>
      <td>24</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>44.84</td>
      <td>15,600</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>345 rows × 11 columns</p>
</div>




```python
## 6월 데이터만 추출해보세요 
```


```python
df_sejong['계약년월']
```




    0      2017_01_04
    1      2017_01_06
    2      2017_02_05
    3      2017_02_07
    4      2017_02_07
              ...    
    340    2020_12_20
    341    2020_12_21
    342    2020_12_23
    343    2020_12_23
    344    2020_12_24
    Name: 계약년월, Length: 345, dtype: object




```python
df_sejong['계약년월']=pd.to_datetime(df_sejong['계약년월'],format='%Y%m%d')
df_sejong['계약년월']
```




    0     2017-01-04
    1     2017-01-06
    2     2017-02-05
    3     2017-02-07
    4     2017-02-07
             ...    
    340   2020-12-20
    341   2020-12-21
    342   2020-12-23
    343   2020-12-23
    344   2020-12-24
    Name: 계약년월, Length: 345, dtype: datetime64[ns]




```python
df_sejong[df_sejong['계약년월'].dt.strftime('%m')=='06']
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>계약년월</th>
      <th>계약일</th>
      <th>시군구</th>
      <th>본번</th>
      <th>부번</th>
      <th>단지명</th>
      <th>전용면적(㎡)</th>
      <th>거래금액(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>해제사유발생일</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>21</th>
      <td>2017-06-06</td>
      <td>6</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>2차푸르지오시티</td>
      <td>23.24</td>
      <td>9,300</td>
      <td>10</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2017-06-08</td>
      <td>8</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>24.22</td>
      <td>9,900</td>
      <td>19</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2017-06-19</td>
      <td>19</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>2차푸르지오시티</td>
      <td>30.48</td>
      <td>14,800</td>
      <td>15</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2017-06-21</td>
      <td>21</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>호수의아침</td>
      <td>24.01</td>
      <td>11,700</td>
      <td>10</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>64</th>
      <td>2018-06-20</td>
      <td>20</td>
      <td>세종특별자치시 도담동</td>
      <td>246</td>
      <td>5</td>
      <td>세종한신휴시티</td>
      <td>32.19</td>
      <td>13,000</td>
      <td>6</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>98</th>
      <td>2019-06-04</td>
      <td>4</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>8,500</td>
      <td>12</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>99</th>
      <td>2019-06-04</td>
      <td>4</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>8,500</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>100</th>
      <td>2019-06-06</td>
      <td>6</td>
      <td>세종특별자치시 나성동</td>
      <td>0</td>
      <td>0</td>
      <td>더리치세종의아침</td>
      <td>25.39</td>
      <td>11,920</td>
      <td>5</td>
      <td>2015</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>101</th>
      <td>2019-06-08</td>
      <td>8</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>22.42</td>
      <td>8,500</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>173</th>
      <td>2020-06-01</td>
      <td>1</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>7,800</td>
      <td>10</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>174</th>
      <td>2020-06-03</td>
      <td>3</td>
      <td>세종특별자치시 도담동</td>
      <td>246</td>
      <td>5</td>
      <td>세종한신휴시티</td>
      <td>24.03</td>
      <td>8,400</td>
      <td>8</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>175</th>
      <td>2020-06-08</td>
      <td>8</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>2차푸르지오시티</td>
      <td>21.92</td>
      <td>8,000</td>
      <td>12</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>176</th>
      <td>2020-06-08</td>
      <td>8</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>24.22</td>
      <td>7,500</td>
      <td>14</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>177</th>
      <td>2020-06-08</td>
      <td>8</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>8,050</td>
      <td>19</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>178</th>
      <td>2020-06-11</td>
      <td>11</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>22.42</td>
      <td>8,000</td>
      <td>20</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>179</th>
      <td>2020-06-15</td>
      <td>15</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>22.42</td>
      <td>6,900</td>
      <td>12</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>180</th>
      <td>2020-06-16</td>
      <td>16</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>2차푸르지오시티</td>
      <td>21.92</td>
      <td>6,850</td>
      <td>15</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>181</th>
      <td>2020-06-18</td>
      <td>18</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>2차푸르지오시티</td>
      <td>23.24</td>
      <td>7,800</td>
      <td>7</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>182</th>
      <td>2020-06-18</td>
      <td>18</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>44.84</td>
      <td>14,000</td>
      <td>20</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>183</th>
      <td>2020-06-18</td>
      <td>18</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>7,900</td>
      <td>12</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>184</th>
      <td>2020-06-20</td>
      <td>20</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>29.06</td>
      <td>11,750</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>185</th>
      <td>2020-06-20</td>
      <td>20</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>호수의아침</td>
      <td>28.65</td>
      <td>10,600</td>
      <td>16</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>186</th>
      <td>2020-06-23</td>
      <td>23</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>7,800</td>
      <td>9</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>187</th>
      <td>2020-06-24</td>
      <td>24</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>22.42</td>
      <td>8,500</td>
      <td>4</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>188</th>
      <td>2020-06-24</td>
      <td>24</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>8,500</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>189</th>
      <td>2020-06-27</td>
      <td>27</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>7,500</td>
      <td>12</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>190</th>
      <td>2020-06-29</td>
      <td>29</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>22.42</td>
      <td>8,000</td>
      <td>12</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>191</th>
      <td>2020-06-29</td>
      <td>29</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>호수의아침</td>
      <td>24.01</td>
      <td>9,500</td>
      <td>14</td>
      <td>2014</td>
      <td>20200720.0</td>
    </tr>
    <tr>
      <th>192</th>
      <td>2020-06-29</td>
      <td>29</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>호수의아침</td>
      <td>24.01</td>
      <td>9,500</td>
      <td>14</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## 날짜순으로 데이터를 정렬해보세요 


```python
df_sejong.sort_values("계약년월")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>계약년월</th>
      <th>계약일</th>
      <th>시군구</th>
      <th>본번</th>
      <th>부번</th>
      <th>단지명</th>
      <th>전용면적(㎡)</th>
      <th>거래금액(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>해제사유발생일</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-01-04</td>
      <td>4</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,000</td>
      <td>14</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-01-06</td>
      <td>6</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,500</td>
      <td>11</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-02-05</td>
      <td>5</td>
      <td>세종특별자치시 나성동</td>
      <td>713</td>
      <td>0</td>
      <td>세진이너스빌</td>
      <td>34.15</td>
      <td>13,000</td>
      <td>8</td>
      <td>2013</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017-02-07</td>
      <td>7</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,500</td>
      <td>4</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-02-07</td>
      <td>7</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>23.74</td>
      <td>9,000</td>
      <td>4</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>340</th>
      <td>2020-12-20</td>
      <td>20</td>
      <td>세종특별자치시 나성동</td>
      <td>756</td>
      <td>0</td>
      <td>리치먼드시티세종</td>
      <td>26.18</td>
      <td>16,410</td>
      <td>6</td>
      <td>2020</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>341</th>
      <td>2020-12-21</td>
      <td>21</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>24.22</td>
      <td>8,600</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>343</th>
      <td>2020-12-23</td>
      <td>23</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>2차푸르지오시티</td>
      <td>30.48</td>
      <td>11,500</td>
      <td>9</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>342</th>
      <td>2020-12-23</td>
      <td>23</td>
      <td>세종특별자치시 나성동</td>
      <td>756</td>
      <td>0</td>
      <td>리치먼드시티세종</td>
      <td>26.18</td>
      <td>15,340</td>
      <td>7</td>
      <td>2020</td>
      <td>20210118.0</td>
    </tr>
    <tr>
      <th>344</th>
      <td>2020-12-24</td>
      <td>24</td>
      <td>세종특별자치시 어진동</td>
      <td>0</td>
      <td>0</td>
      <td>푸르지오시티</td>
      <td>44.84</td>
      <td>15,600</td>
      <td>18</td>
      <td>2014</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>345 rows × 11 columns</p>
</div>


