---
title:  "[Python] 데이터핸들링-group by QUIZ" 

categories:
  - quiz
tags:
  - [Python,ADP,class101,quiz]

toc: true
toc_sticky: true

date: 2022-11-22

---


# 과제 3-1 Groupby & crosstab

## 데이터 : "7.세종시_아파트(전월세)_실거래가.csv"



```python
import pandas as pd
```


```python
df=pd.read_csv("D:/anaconda/00.studying/data/7.세종시_아파트(전월세)_실거래가.csv")
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
    </tr>
  </tbody>
</table>
</div>




```python
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
    

## 전세의 보증금 평균 값을 구하세요 groupby 사용 


```python
df.groupby(['전월세구분']).mean()['보증금(만원)']
```




    전월세구분
    월세     3514.429264
    전세    17329.536254
    Name: 보증금(만원), dtype: float64




```python
df[df['전월세구분']=='전세'].mean()['보증금(만원)']
```

    C:\Windows\Temp\ipykernel_17416\4042288225.py:1: FutureWarning: Dropping of nuisance columns in DataFrame reductions (with 'numeric_only=None') is deprecated; in a future version this will raise TypeError.  Select only valid columns before calling the reduction.
      df[df['전월세구분']=='전세'].mean()['보증금(만원)']
    




    17329.536253944683



## 세종시 월세 평균 가격을 구하세요 



```python
df.groupby(['전월세구분']).mean()['월세(만원)']
```




    전월세구분
    월세    42.001254
    전세     0.000000
    Name: 월세(만원), dtype: float64




```python
df[df['전월세구분']=='월세'].mean()['월세(만원)']
```

    C:\Windows\Temp\ipykernel_17416\2564067106.py:1: FutureWarning: Dropping of nuisance columns in DataFrame reductions (with 'numeric_only=None') is deprecated; in a future version this will raise TypeError.  Select only valid columns before calling the reduction.
      df[df['전월세구분']=='월세'].mean()['월세(만원)']
    




    42.001254180602004



## 계약년도별, 시군구별 평균 보증금 가격를 구하세요  




```python
#계약년월 ->계약년도 변경하고 칼럼 생성하기 
df['계약년도']=df['계약년월'].astype("str").str[:4]
df['계약년도'].head(5)
```




    0    2017
    1    2017
    2    2017
    3    2017
    4    2017
    Name: 계약년도, dtype: object




```python
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
      <th>계약년도</th>
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
      <td>2017</td>
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
      <td>2017</td>
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
      <td>2017</td>
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
      <td>2017</td>
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
      <td>2017</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(['계약년도','시군구']).mean()[['보증금(만원)']]
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
      <th></th>
      <th>보증금(만원)</th>
    </tr>
    <tr>
      <th>계약년도</th>
      <th>시군구</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2017</th>
      <th>세종특별자치시 고운동</th>
      <td>15983.027397</td>
    </tr>
    <tr>
      <th>세종특별자치시 금남면 용포리</th>
      <td>6287.640449</td>
    </tr>
    <tr>
      <th>세종특별자치시 나성동</th>
      <td>3277.551020</td>
    </tr>
    <tr>
      <th>세종특별자치시 다정동</th>
      <td>6220.833333</td>
    </tr>
    <tr>
      <th>세종특별자치시 대평동</th>
      <td>9650.000000</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">2020</th>
      <th>세종특별자치시 조치원읍 죽림리</th>
      <td>13480.555556</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 침산리</th>
      <td>9636.144578</td>
    </tr>
    <tr>
      <th>세종특별자치시 종촌동</th>
      <td>14617.469504</td>
    </tr>
    <tr>
      <th>세종특별자치시 한솔동</th>
      <td>16266.289655</td>
    </tr>
    <tr>
      <th>세종특별자치시 해밀동</th>
      <td>23691.919192</td>
    </tr>
  </tbody>
</table>
<p>130 rows × 1 columns</p>
</div>



## 계약년도별 전세 건수를 구하세요 


```python
전세만=df[df['전월세구분']=='전세']
answer1=전세만['계약년도'].value_counts()

pd.DataFrame(answer1.sort_index(ascending=True))
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
      <th>계약년도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017</th>
      <td>6344</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>5887</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>7286</td>
    </tr>
    <tr>
      <th>2020</th>
      <td>7418</td>
    </tr>
  </tbody>
</table>
</div>




```python
answer2=pd.crosstab(df['계약년도'],df['전월세구분'],dropna=True)
answer2.sort_index(ascending=True)
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
      <th>전월세구분</th>
      <th>월세</th>
      <th>전세</th>
    </tr>
    <tr>
      <th>계약년도</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017</th>
      <td>2530</td>
      <td>6344</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>2486</td>
      <td>5887</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>3379</td>
      <td>7286</td>
    </tr>
    <tr>
      <th>2020</th>
      <td>3565</td>
      <td>7418</td>
    </tr>
  </tbody>
</table>
</div>



## 인덱스에 시군구, 컬럼에는 전월세구분이 있는 도수분포표를 만드세요 


```python
pd.crosstab(df['시군구'],df['전월세구분'],dropna=True)
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
      <th>전월세구분</th>
      <th>월세</th>
      <th>전세</th>
    </tr>
    <tr>
      <th>시군구</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>세종특별자치시 고운동</th>
      <td>1176</td>
      <td>4325</td>
    </tr>
    <tr>
      <th>세종특별자치시 금남면 용포리</th>
      <td>105</td>
      <td>310</td>
    </tr>
    <tr>
      <th>세종특별자치시 나성동</th>
      <td>890</td>
      <td>636</td>
    </tr>
    <tr>
      <th>세종특별자치시 다정동</th>
      <td>765</td>
      <td>2030</td>
    </tr>
    <tr>
      <th>세종특별자치시 대평동</th>
      <td>451</td>
      <td>434</td>
    </tr>
    <tr>
      <th>세종특별자치시 도담동</th>
      <td>1288</td>
      <td>3467</td>
    </tr>
    <tr>
      <th>세종특별자치시 반곡동</th>
      <td>45</td>
      <td>160</td>
    </tr>
    <tr>
      <th>세종특별자치시 보람동</th>
      <td>803</td>
      <td>1937</td>
    </tr>
    <tr>
      <th>세종특별자치시 부강면 부강리</th>
      <td>18</td>
      <td>39</td>
    </tr>
    <tr>
      <th>세종특별자치시 새롬동</th>
      <td>1185</td>
      <td>2299</td>
    </tr>
    <tr>
      <th>세종특별자치시 소담동</th>
      <td>222</td>
      <td>845</td>
    </tr>
    <tr>
      <th>세종특별자치시 소정면 운당리</th>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>세종특별자치시 아름동</th>
      <td>743</td>
      <td>2692</td>
    </tr>
    <tr>
      <th>세종특별자치시 어진동</th>
      <td>364</td>
      <td>683</td>
    </tr>
    <tr>
      <th>세종특별자치시 연동면 명학리</th>
      <td>38</td>
      <td>90</td>
    </tr>
    <tr>
      <th>세종특별자치시 연서면 봉암리</th>
      <td>28</td>
      <td>47</td>
    </tr>
    <tr>
      <th>세종특별자치시 장군면 금암리</th>
      <td>0</td>
      <td>10</td>
    </tr>
    <tr>
      <th>세종특별자치시 전동면 노장리</th>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>세종특별자치시 전의면 동교리</th>
      <td>21</td>
      <td>23</td>
    </tr>
    <tr>
      <th>세종특별자치시 전의면 유천리</th>
      <td>15</td>
      <td>22</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 교리</th>
      <td>16</td>
      <td>59</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 남리</th>
      <td>13</td>
      <td>46</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 번암리</th>
      <td>285</td>
      <td>147</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 상리</th>
      <td>22</td>
      <td>28</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 서창리</th>
      <td>60</td>
      <td>5</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 신안리</th>
      <td>145</td>
      <td>393</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 신흥리</th>
      <td>132</td>
      <td>358</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 원리</th>
      <td>9</td>
      <td>3</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 정리</th>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 죽림리</th>
      <td>210</td>
      <td>652</td>
    </tr>
    <tr>
      <th>세종특별자치시 조치원읍 침산리</th>
      <td>56</td>
      <td>172</td>
    </tr>
    <tr>
      <th>세종특별자치시 종촌동</th>
      <td>2090</td>
      <td>3489</td>
    </tr>
    <tr>
      <th>세종특별자치시 한솔동</th>
      <td>730</td>
      <td>1453</td>
    </tr>
    <tr>
      <th>세종특별자치시 해밀동</th>
      <td>27</td>
      <td>72</td>
    </tr>
  </tbody>
</table>
</div>


