---
title:  "[Python] 데이터핸들링-조건에 따른 행/열 선택Quiz" 

categories:
  - Python
tags:
  - [Python,ADP,quiz]

toc: true
toc_sticky: true

date: 2022-11-12

---


# 과제 3 
    데이터 : "7.세종시_아파트(전월세)_실거래가.csv"
    1) 단지명 중  '해밀마을 2단지'인 row 삭제 
    2) new_시군구' 컬럼을 만들고 '세종특별자치시 고운동' => '세종특별자치시 해밀동' 으로 변경
    3) 'Class'컬럼을 만든 뒤 전세면 True 아니면 False로 입력 (loc사용) 
    4) 전세이면서 보증금이 1억 이상인 데이터만을 추출 
    5) -10~0층 : 지하 , 1~5층 : 저층 6~15층 : 중층, 16층 이상 : 고층으로 할당하는 새로운 컬럼 생성 


```python
import pandas as pd
import numpy as np
```


```python
df=pd.read_csv("D:/anaconda/00.studying/data/7.세종시_아파트(전월세)_실거래가.csv")
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 38895 entries, 0 to 38894
    Data columns (total 13 columns):
     #   Column      Non-Null Count  Dtype  
    ---  ------      --------------  -----  
     0   Unnamed: 0  38895 non-null  int64  
     1   계약년월        38895 non-null  int64  
     2   계약일         38895 non-null  int64  
     3   시군구         38895 non-null  object 
     4   본번          38895 non-null  object 
     5   부번          38895 non-null  int64  
     6   단지명         38895 non-null  object 
     7   전월세구분       38895 non-null  object 
     8   전용면적(㎡)     38895 non-null  float64
     9   보증금(만원)     38895 non-null  int64  
     10  월세(만원)      38895 non-null  int64  
     11  층           38895 non-null  int64  
     12  건축년도        38895 non-null  int64  
    dtypes: float64(1), int64(8), object(4)
    memory usage: 3.9+ MB
    

## 단지명 중  '해밀마을 2단지'인 row 삭제


```python
df.drop(df.loc[df['단지명']=='해밀마을 2단지'].index,inplace=True)
df['단지명']
```




    0        가락마을 20단지(호반베르디움5차)
    1        가락마을 20단지(호반베르디움5차)
    2        가락마을 20단지(호반베르디움5차)
    3        가락마을 20단지(호반베르디움5차)
    4        가락마을 20단지(호반베르디움5차)
                    ...         
    38852               해밀마을 1단지
    38853               해밀마을 1단지
    38854               해밀마을 1단지
    38855               해밀마을 1단지
    38856               해밀마을 1단지
    Name: 단지명, Length: 38857, dtype: object



## new_시군구' 컬럼을 만들고 '세종특별자치시 고운동' => '세종특별자치시 해밀동' 으로 변경


```python
df.loc[df['시군구']=='세종특별자치시 고운동','new_시군구']='세종특별자치시 해밀동'
df
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
      <th>Unnamed: 0</th>
      <th>계약년월</th>
      <th>계약일</th>
      <th>시군구</th>
      <th>본번</th>
      <th>부번</th>
      <th>단지명</th>
      <th>전월세구분</th>
      <th>전용면적(㎡)</th>
      <th>보증금(만원)</th>
      <th>월세(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>new_시군구</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>201701</td>
      <td>13</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>10000</td>
      <td>0</td>
      <td>13</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>201701</td>
      <td>14</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>18000</td>
      <td>0</td>
      <td>19</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>201701</td>
      <td>14</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>59.8338</td>
      <td>17000</td>
      <td>0</td>
      <td>10</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>201701</td>
      <td>15</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>17000</td>
      <td>0</td>
      <td>2</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>201702</td>
      <td>4</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>월세</td>
      <td>84.9895</td>
      <td>10000</td>
      <td>30</td>
      <td>13</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>38852</th>
      <td>38852</td>
      <td>202012</td>
      <td>6</td>
      <td>세종특별자치시 해밀동</td>
      <td>6401</td>
      <td>1</td>
      <td>해밀마을 1단지</td>
      <td>월세</td>
      <td>59.4000</td>
      <td>2000</td>
      <td>75</td>
      <td>5</td>
      <td>2020</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>38853</th>
      <td>38853</td>
      <td>202012</td>
      <td>8</td>
      <td>세종특별자치시 해밀동</td>
      <td>6401</td>
      <td>1</td>
      <td>해밀마을 1단지</td>
      <td>월세</td>
      <td>59.4000</td>
      <td>15000</td>
      <td>30</td>
      <td>6</td>
      <td>2020</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>38854</th>
      <td>38854</td>
      <td>202012</td>
      <td>11</td>
      <td>세종특별자치시 해밀동</td>
      <td>6401</td>
      <td>1</td>
      <td>해밀마을 1단지</td>
      <td>전세</td>
      <td>84.8500</td>
      <td>30000</td>
      <td>0</td>
      <td>6</td>
      <td>2020</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>38855</th>
      <td>38855</td>
      <td>202012</td>
      <td>13</td>
      <td>세종특별자치시 해밀동</td>
      <td>6401</td>
      <td>1</td>
      <td>해밀마을 1단지</td>
      <td>월세</td>
      <td>84.8500</td>
      <td>5000</td>
      <td>95</td>
      <td>8</td>
      <td>2020</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>38856</th>
      <td>38856</td>
      <td>202012</td>
      <td>19</td>
      <td>세종특별자치시 해밀동</td>
      <td>6401</td>
      <td>1</td>
      <td>해밀마을 1단지</td>
      <td>전세</td>
      <td>84.6700</td>
      <td>43000</td>
      <td>0</td>
      <td>3</td>
      <td>2020</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>38857 rows × 14 columns</p>
</div>



## 'Class'컬럼을 만든 뒤 전세면 True 아니면 False로 입력 (loc사용) 


```python
df['Class']=False
df.loc[df['전월세구분']=='전세','Class']=True
df.head(3)
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
      <th>Unnamed: 0</th>
      <th>계약년월</th>
      <th>계약일</th>
      <th>시군구</th>
      <th>본번</th>
      <th>부번</th>
      <th>단지명</th>
      <th>전월세구분</th>
      <th>전용면적(㎡)</th>
      <th>보증금(만원)</th>
      <th>월세(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>new_시군구</th>
      <th>Class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>201701</td>
      <td>13</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>10000</td>
      <td>0</td>
      <td>13</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>201701</td>
      <td>14</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>18000</td>
      <td>0</td>
      <td>19</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>201701</td>
      <td>14</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>59.8338</td>
      <td>17000</td>
      <td>0</td>
      <td>10</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



## 전세이면서 보증금이 1억 이상인 데이터만을 추출


```python
df[(df['Class']==True) & (df['보증금(만원)']>=10000)]
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
      <th>Unnamed: 0</th>
      <th>계약년월</th>
      <th>계약일</th>
      <th>시군구</th>
      <th>본번</th>
      <th>부번</th>
      <th>단지명</th>
      <th>전월세구분</th>
      <th>전용면적(㎡)</th>
      <th>보증금(만원)</th>
      <th>월세(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>new_시군구</th>
      <th>Class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>201701</td>
      <td>13</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>10000</td>
      <td>0</td>
      <td>13</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>201701</td>
      <td>14</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>18000</td>
      <td>0</td>
      <td>19</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>201701</td>
      <td>14</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>59.8338</td>
      <td>17000</td>
      <td>0</td>
      <td>10</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>201701</td>
      <td>15</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>17000</td>
      <td>0</td>
      <td>2</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>201702</td>
      <td>8</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>19000</td>
      <td>0</td>
      <td>8</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>38849</th>
      <td>38849</td>
      <td>202011</td>
      <td>24</td>
      <td>세종특별자치시 해밀동</td>
      <td>6401</td>
      <td>1</td>
      <td>해밀마을 1단지</td>
      <td>전세</td>
      <td>84.4000</td>
      <td>25000</td>
      <td>0</td>
      <td>12</td>
      <td>2020</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
    <tr>
      <th>38850</th>
      <td>38850</td>
      <td>202011</td>
      <td>26</td>
      <td>세종특별자치시 해밀동</td>
      <td>6401</td>
      <td>1</td>
      <td>해밀마을 1단지</td>
      <td>전세</td>
      <td>84.8500</td>
      <td>35000</td>
      <td>0</td>
      <td>1</td>
      <td>2020</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
    <tr>
      <th>38851</th>
      <td>38851</td>
      <td>202012</td>
      <td>1</td>
      <td>세종특별자치시 해밀동</td>
      <td>6401</td>
      <td>1</td>
      <td>해밀마을 1단지</td>
      <td>전세</td>
      <td>84.8400</td>
      <td>41000</td>
      <td>0</td>
      <td>1</td>
      <td>2020</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
    <tr>
      <th>38854</th>
      <td>38854</td>
      <td>202012</td>
      <td>11</td>
      <td>세종특별자치시 해밀동</td>
      <td>6401</td>
      <td>1</td>
      <td>해밀마을 1단지</td>
      <td>전세</td>
      <td>84.8500</td>
      <td>30000</td>
      <td>0</td>
      <td>6</td>
      <td>2020</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
    <tr>
      <th>38856</th>
      <td>38856</td>
      <td>202012</td>
      <td>19</td>
      <td>세종특별자치시 해밀동</td>
      <td>6401</td>
      <td>1</td>
      <td>해밀마을 1단지</td>
      <td>전세</td>
      <td>84.6700</td>
      <td>43000</td>
      <td>0</td>
      <td>3</td>
      <td>2020</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
<p>24769 rows × 15 columns</p>
</div>



## -10~0층 : 지하 , 1~5층 : 저층 6~15층 : 중층, 16층 이상 : 고층으로 할당하는 새로운 컬럼 생성


```python
conditionlist=[ (df['층']<1), ((df['층']<6)&(df['층']>0)),((df['층']<16)&(df['층']>5)),(df['층']>15)]
choicelist=['지하','저층','중층','고층']
df['층구분']=np.select(conditionlist,choicelist,default='Not_specified')
df.head(5)
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
      <th>Unnamed: 0</th>
      <th>계약년월</th>
      <th>계약일</th>
      <th>시군구</th>
      <th>본번</th>
      <th>부번</th>
      <th>단지명</th>
      <th>전월세구분</th>
      <th>전용면적(㎡)</th>
      <th>보증금(만원)</th>
      <th>월세(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>new_시군구</th>
      <th>Class</th>
      <th>층구분</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>201701</td>
      <td>13</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>10000</td>
      <td>0</td>
      <td>13</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
      <td>중층</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>201701</td>
      <td>14</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>18000</td>
      <td>0</td>
      <td>19</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
      <td>고층</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>201701</td>
      <td>14</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>59.8338</td>
      <td>17000</td>
      <td>0</td>
      <td>10</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
      <td>중층</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>201701</td>
      <td>15</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>전세</td>
      <td>84.9895</td>
      <td>17000</td>
      <td>0</td>
      <td>2</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>True</td>
      <td>저층</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>201702</td>
      <td>4</td>
      <td>세종특별자치시 고운동</td>
      <td>1396</td>
      <td>0</td>
      <td>가락마을 20단지(호반베르디움5차)</td>
      <td>월세</td>
      <td>84.9895</td>
      <td>10000</td>
      <td>30</td>
      <td>13</td>
      <td>2015</td>
      <td>세종특별자치시 해밀동</td>
      <td>False</td>
      <td>중층</td>
    </tr>
  </tbody>
</table>
</div>


