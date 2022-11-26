---
title:  "[Python] 데이터핸들링_문자열데이터 변환str" 

categories:
  - Python
tags:
  - [Python,ADP,class101]

toc: true
toc_sticky: true

date: 2022-11-26

---


# 문자열 변환

## 인덱싱

시리즈.str[:n] : 문자열 인덱스로 추출 


```python
import pandas as pd
import numpy as np
```


```python
df_sejong=pd.read_csv("D:/anaconda/00.studying/data/7.세종시_아파트(전월세)_실거래가.csv")
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
    </tr>
    <tr>
      <th>38890</th>
      <td>38890</td>
      <td>202011</td>
      <td>21</td>
      <td>세종특별자치시 해밀동</td>
      <td>6402</td>
      <td>1</td>
      <td>해밀마을 2단지</td>
      <td>월세</td>
      <td>102.8300</td>
      <td>10000</td>
      <td>100</td>
      <td>5</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>38891</th>
      <td>38891</td>
      <td>202012</td>
      <td>8</td>
      <td>세종특별자치시 해밀동</td>
      <td>6402</td>
      <td>1</td>
      <td>해밀마을 2단지</td>
      <td>월세</td>
      <td>102.5300</td>
      <td>10000</td>
      <td>95</td>
      <td>14</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>38892</th>
      <td>38892</td>
      <td>202012</td>
      <td>11</td>
      <td>세종특별자치시 해밀동</td>
      <td>6402</td>
      <td>1</td>
      <td>해밀마을 2단지</td>
      <td>전세</td>
      <td>84.9500</td>
      <td>30000</td>
      <td>0</td>
      <td>18</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>38893</th>
      <td>38893</td>
      <td>202012</td>
      <td>12</td>
      <td>세종특별자치시 해밀동</td>
      <td>6402</td>
      <td>1</td>
      <td>해밀마을 2단지</td>
      <td>전세</td>
      <td>84.9500</td>
      <td>34000</td>
      <td>0</td>
      <td>18</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>38894</th>
      <td>38894</td>
      <td>202012</td>
      <td>13</td>
      <td>세종특별자치시 해밀동</td>
      <td>6402</td>
      <td>1</td>
      <td>해밀마을 2단지</td>
      <td>월세</td>
      <td>84.9500</td>
      <td>8000</td>
      <td>85</td>
      <td>16</td>
      <td>2020</td>
    </tr>
  </tbody>
</table>
<p>38895 rows × 13 columns</p>
</div>




```python
#필요없는 값 없애주기
df_sejong.drop(columns='Unnamed: 0',inplace=True)
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
    </tr>
    <tr>
      <th>38890</th>
      <td>202011</td>
      <td>21</td>
      <td>세종특별자치시 해밀동</td>
      <td>6402</td>
      <td>1</td>
      <td>해밀마을 2단지</td>
      <td>월세</td>
      <td>102.8300</td>
      <td>10000</td>
      <td>100</td>
      <td>5</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>38891</th>
      <td>202012</td>
      <td>8</td>
      <td>세종특별자치시 해밀동</td>
      <td>6402</td>
      <td>1</td>
      <td>해밀마을 2단지</td>
      <td>월세</td>
      <td>102.5300</td>
      <td>10000</td>
      <td>95</td>
      <td>14</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>38892</th>
      <td>202012</td>
      <td>11</td>
      <td>세종특별자치시 해밀동</td>
      <td>6402</td>
      <td>1</td>
      <td>해밀마을 2단지</td>
      <td>전세</td>
      <td>84.9500</td>
      <td>30000</td>
      <td>0</td>
      <td>18</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>38893</th>
      <td>202012</td>
      <td>12</td>
      <td>세종특별자치시 해밀동</td>
      <td>6402</td>
      <td>1</td>
      <td>해밀마을 2단지</td>
      <td>전세</td>
      <td>84.9500</td>
      <td>34000</td>
      <td>0</td>
      <td>18</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>38894</th>
      <td>202012</td>
      <td>13</td>
      <td>세종특별자치시 해밀동</td>
      <td>6402</td>
      <td>1</td>
      <td>해밀마을 2단지</td>
      <td>월세</td>
      <td>84.9500</td>
      <td>8000</td>
      <td>85</td>
      <td>16</td>
      <td>2020</td>
    </tr>
  </tbody>
</table>
<p>38895 rows × 12 columns</p>
</div>




```python
df_sejong['시군구'].unique()
```




    array(['세종특별자치시 고운동', '세종특별자치시 금남면 용포리', '세종특별자치시 나성동', '세종특별자치시 다정동',
           '세종특별자치시 대평동', '세종특별자치시 도담동', '세종특별자치시 반곡동', '세종특별자치시 보람동',
           '세종특별자치시 부강면 부강리', '세종특별자치시 새롬동', '세종특별자치시 소담동', '세종특별자치시 아름동',
           '세종특별자치시 어진동', '세종특별자치시 연동면 명학리', '세종특별자치시 연서면 봉암리',
           '세종특별자치시 장군면 금암리', '세종특별자치시 전동면 노장리', '세종특별자치시 전의면 동교리',
           '세종특별자치시 전의면 유천리', '세종특별자치시 조치원읍 교리', '세종특별자치시 조치원읍 남리',
           '세종특별자치시 조치원읍 번암리', '세종특별자치시 조치원읍 상리', '세종특별자치시 조치원읍 신안리',
           '세종특별자치시 조치원읍 신흥리', '세종특별자치시 조치원읍 원리', '세종특별자치시 조치원읍 정리',
           '세종특별자치시 조치원읍 죽림리', '세종특별자치시 조치원읍 침산리', '세종특별자치시 종촌동',
           '세종특별자치시 한솔동', '세종특별자치시 소정면 운당리', '세종특별자치시 조치원읍 서창리',
           '세종특별자치시 해밀동'], dtype=object)




```python
#프레임 형태가 아니기때문에 시리즈 형태가 맞다
df_sejong['시군구']
```




    0        세종특별자치시 고운동
    1        세종특별자치시 고운동
    2        세종특별자치시 고운동
    3        세종특별자치시 고운동
    4        세종특별자치시 고운동
                ...     
    38890    세종특별자치시 해밀동
    38891    세종특별자치시 해밀동
    38892    세종특별자치시 해밀동
    38893    세종특별자치시 해밀동
    38894    세종특별자치시 해밀동
    Name: 시군구, Length: 38895, dtype: object




```python
df_sejong['시군구'].str[0:7]
```




    0        세종특별자치시
    1        세종특별자치시
    2        세종특별자치시
    3        세종특별자치시
    4        세종특별자치시
              ...   
    38890    세종특별자치시
    38891    세종특별자치시
    38892    세종특별자치시
    38893    세종특별자치시
    38894    세종특별자치시
    Name: 시군구, Length: 38895, dtype: object




```python
df_sejong['시']=df_sejong['시군구'].str[0:7]
df_sejong['시']
```




    0        세종특별자치시
    1        세종특별자치시
    2        세종특별자치시
    3        세종특별자치시
    4        세종특별자치시
              ...   
    38890    세종특별자치시
    38891    세종특별자치시
    38892    세종특별자치시
    38893    세종특별자치시
    38894    세종특별자치시
    Name: 시, Length: 38895, dtype: object



## 띄어쓰기로 분할


```python
df_sejong['시군구'].str.split(' ')
```




    0        [세종특별자치시, 고운동]
    1        [세종특별자치시, 고운동]
    2        [세종특별자치시, 고운동]
    3        [세종특별자치시, 고운동]
    4        [세종특별자치시, 고운동]
                  ...      
    38890    [세종특별자치시, 해밀동]
    38891    [세종특별자치시, 해밀동]
    38892    [세종특별자치시, 해밀동]
    38893    [세종특별자치시, 해밀동]
    38894    [세종특별자치시, 해밀동]
    Name: 시군구, Length: 38895, dtype: object



## 데이터 프레임으로 변경하고 띄어쓰기로 분할하기 


```python
df_sejong_split=df_sejong['시군구'].str.split(' ',expand=True)
df_sejong_split
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>세종특별자치시</td>
      <td>고운동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>세종특별자치시</td>
      <td>고운동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2</th>
      <td>세종특별자치시</td>
      <td>고운동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>세종특별자치시</td>
      <td>고운동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>4</th>
      <td>세종특별자치시</td>
      <td>고운동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>38890</th>
      <td>세종특별자치시</td>
      <td>해밀동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>38891</th>
      <td>세종특별자치시</td>
      <td>해밀동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>38892</th>
      <td>세종특별자치시</td>
      <td>해밀동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>38893</th>
      <td>세종특별자치시</td>
      <td>해밀동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>38894</th>
      <td>세종특별자치시</td>
      <td>해밀동</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
<p>38895 rows × 3 columns</p>
</div>




```python
# 대충 컬럼 이름명 넣어주기
df_sejong_split.columns=['시','군','구']
df_sejong_split

# None은 공백이다 None=None==TRUE가 되지않는다 
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
      <th>시</th>
      <th>군</th>
      <th>구</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>세종특별자치시</td>
      <td>고운동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>세종특별자치시</td>
      <td>고운동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2</th>
      <td>세종특별자치시</td>
      <td>고운동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>세종특별자치시</td>
      <td>고운동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>4</th>
      <td>세종특별자치시</td>
      <td>고운동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>38890</th>
      <td>세종특별자치시</td>
      <td>해밀동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>38891</th>
      <td>세종특별자치시</td>
      <td>해밀동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>38892</th>
      <td>세종특별자치시</td>
      <td>해밀동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>38893</th>
      <td>세종특별자치시</td>
      <td>해밀동</td>
      <td>None</td>
    </tr>
    <tr>
      <th>38894</th>
      <td>세종특별자치시</td>
      <td>해밀동</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
<p>38895 rows × 3 columns</p>
</div>




```python
df_sejong_split['구']==df_sejong_split['구']
```




    0        False
    1        False
    2        False
    3        False
    4        False
             ...  
    38890    False
    38891    False
    38892    False
    38893    False
    38894    False
    Name: 구, Length: 38895, dtype: bool




```python
df_sejong_split[df_sejong_split['구']==df_sejong_split['구']]
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
      <th>시</th>
      <th>군</th>
      <th>구</th>
      <th>None</th>
      <th>용포리</th>
      <th>부강리</th>
      <th>명학리</th>
      <th>봉암리</th>
      <th>금암리</th>
      <th>노장리</th>
      <th>...</th>
      <th>번암리</th>
      <th>상리</th>
      <th>신안리</th>
      <th>신흥리</th>
      <th>원리</th>
      <th>정리</th>
      <th>죽림리</th>
      <th>침산리</th>
      <th>운당리</th>
      <th>서창리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1898</th>
      <td>세종특별자치시</td>
      <td>금남면</td>
      <td>용포리</td>
      <td>None</td>
      <td>용포리</td>
      <td>부강리</td>
      <td>명학리</td>
      <td>봉암리</td>
      <td>금암리</td>
      <td>노장리</td>
      <td>...</td>
      <td>번암리</td>
      <td>상리</td>
      <td>신안리</td>
      <td>신흥리</td>
      <td>원리</td>
      <td>정리</td>
      <td>죽림리</td>
      <td>침산리</td>
      <td>운당리</td>
      <td>서창리</td>
    </tr>
    <tr>
      <th>1899</th>
      <td>세종특별자치시</td>
      <td>금남면</td>
      <td>용포리</td>
      <td>None</td>
      <td>용포리</td>
      <td>부강리</td>
      <td>명학리</td>
      <td>봉암리</td>
      <td>금암리</td>
      <td>노장리</td>
      <td>...</td>
      <td>번암리</td>
      <td>상리</td>
      <td>신안리</td>
      <td>신흥리</td>
      <td>원리</td>
      <td>정리</td>
      <td>죽림리</td>
      <td>침산리</td>
      <td>운당리</td>
      <td>서창리</td>
    </tr>
    <tr>
      <th>1900</th>
      <td>세종특별자치시</td>
      <td>금남면</td>
      <td>용포리</td>
      <td>None</td>
      <td>용포리</td>
      <td>부강리</td>
      <td>명학리</td>
      <td>봉암리</td>
      <td>금암리</td>
      <td>노장리</td>
      <td>...</td>
      <td>번암리</td>
      <td>상리</td>
      <td>신안리</td>
      <td>신흥리</td>
      <td>원리</td>
      <td>정리</td>
      <td>죽림리</td>
      <td>침산리</td>
      <td>운당리</td>
      <td>서창리</td>
    </tr>
    <tr>
      <th>1901</th>
      <td>세종특별자치시</td>
      <td>금남면</td>
      <td>용포리</td>
      <td>None</td>
      <td>용포리</td>
      <td>부강리</td>
      <td>명학리</td>
      <td>봉암리</td>
      <td>금암리</td>
      <td>노장리</td>
      <td>...</td>
      <td>번암리</td>
      <td>상리</td>
      <td>신안리</td>
      <td>신흥리</td>
      <td>원리</td>
      <td>정리</td>
      <td>죽림리</td>
      <td>침산리</td>
      <td>운당리</td>
      <td>서창리</td>
    </tr>
    <tr>
      <th>1902</th>
      <td>세종특별자치시</td>
      <td>금남면</td>
      <td>용포리</td>
      <td>None</td>
      <td>용포리</td>
      <td>부강리</td>
      <td>명학리</td>
      <td>봉암리</td>
      <td>금암리</td>
      <td>노장리</td>
      <td>...</td>
      <td>번암리</td>
      <td>상리</td>
      <td>신안리</td>
      <td>신흥리</td>
      <td>원리</td>
      <td>정리</td>
      <td>죽림리</td>
      <td>침산리</td>
      <td>운당리</td>
      <td>서창리</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>36637</th>
      <td>세종특별자치시</td>
      <td>조치원읍</td>
      <td>침산리</td>
      <td>None</td>
      <td>용포리</td>
      <td>부강리</td>
      <td>명학리</td>
      <td>봉암리</td>
      <td>금암리</td>
      <td>노장리</td>
      <td>...</td>
      <td>번암리</td>
      <td>상리</td>
      <td>신안리</td>
      <td>신흥리</td>
      <td>원리</td>
      <td>정리</td>
      <td>죽림리</td>
      <td>침산리</td>
      <td>운당리</td>
      <td>서창리</td>
    </tr>
    <tr>
      <th>36638</th>
      <td>세종특별자치시</td>
      <td>조치원읍</td>
      <td>침산리</td>
      <td>None</td>
      <td>용포리</td>
      <td>부강리</td>
      <td>명학리</td>
      <td>봉암리</td>
      <td>금암리</td>
      <td>노장리</td>
      <td>...</td>
      <td>번암리</td>
      <td>상리</td>
      <td>신안리</td>
      <td>신흥리</td>
      <td>원리</td>
      <td>정리</td>
      <td>죽림리</td>
      <td>침산리</td>
      <td>운당리</td>
      <td>서창리</td>
    </tr>
    <tr>
      <th>36639</th>
      <td>세종특별자치시</td>
      <td>조치원읍</td>
      <td>침산리</td>
      <td>None</td>
      <td>용포리</td>
      <td>부강리</td>
      <td>명학리</td>
      <td>봉암리</td>
      <td>금암리</td>
      <td>노장리</td>
      <td>...</td>
      <td>번암리</td>
      <td>상리</td>
      <td>신안리</td>
      <td>신흥리</td>
      <td>원리</td>
      <td>정리</td>
      <td>죽림리</td>
      <td>침산리</td>
      <td>운당리</td>
      <td>서창리</td>
    </tr>
    <tr>
      <th>36640</th>
      <td>세종특별자치시</td>
      <td>조치원읍</td>
      <td>침산리</td>
      <td>None</td>
      <td>용포리</td>
      <td>부강리</td>
      <td>명학리</td>
      <td>봉암리</td>
      <td>금암리</td>
      <td>노장리</td>
      <td>...</td>
      <td>번암리</td>
      <td>상리</td>
      <td>신안리</td>
      <td>신흥리</td>
      <td>원리</td>
      <td>정리</td>
      <td>죽림리</td>
      <td>침산리</td>
      <td>운당리</td>
      <td>서창리</td>
    </tr>
    <tr>
      <th>36641</th>
      <td>세종특별자치시</td>
      <td>조치원읍</td>
      <td>침산리</td>
      <td>None</td>
      <td>용포리</td>
      <td>부강리</td>
      <td>명학리</td>
      <td>봉암리</td>
      <td>금암리</td>
      <td>노장리</td>
      <td>...</td>
      <td>번암리</td>
      <td>상리</td>
      <td>신안리</td>
      <td>신흥리</td>
      <td>원리</td>
      <td>정리</td>
      <td>죽림리</td>
      <td>침산리</td>
      <td>운당리</td>
      <td>서창리</td>
    </tr>
  </tbody>
</table>
<p>3594 rows × 24 columns</p>
</div>




```python
df_sejong['단지명'].unique()
```




    array(['가락마을 20단지(호반베르디움5차)', '가락마을11단지(중흥에듀카운티)', '가락마을13단지(대광로제비앙)',
           '가락마을15단지(중흥파크뷰)', '가락마을16단지(에듀그린)', '가락마을17단지(골드클래스)',
           '가락마을21단지(에듀포레)', '가락마을22단지(에듀힐스)', '가락마을3단지(호반베르디움)',
           '가락마을5단지(유승한내들)', '가락마을6단지(중흥S클래스프라디움)', '가락마을7단지(중흥S-클래스프라디움)',
           '가락마을8단지(고운뜰아파트)', '가락마을9단지(신동아 파밀리에)', '이지더원(가락마을10단지)',
           '이지더원(가락마을4단지)', '두진리버빌', '신성연기미소지움', '리베라아이누리(2-2)', '블루지움(2-4)',
           '세종갤러리밸류시티', '세종마루(CB5-3BL)', '세종모닝시티2차', '세종퍼스트타워', '세종포레뷰원',
           '세진팰리스', '에스알파크', '에스알파크시티', '우빈가온', '포레뷰투도시형생활주택',
           '한스웰시티(CB5-1BL)', '행복의아침', '가온마을1단지', '가온마을2단지',
           '가온마을5단지(중흥에스클래스센텀시티)', '가온마을9단지', '해들마을3단지', '까사리움',
           '도램마을 14단지(한림풀에버)', '도램마을 19단지(모아미래도)', '도램마을10단지 호반 어반시티',
           '도램마을11단지(반도유보라)', '도램마을16단지(모아미래도)', '도램마을17단지(모아미래도)',
           '도램마을18단지(모아미래도)', '도램마을1단지(웅진스타클래스)', '도램마을20단지(에듀파크)',
           '도램마을2단지(웅진스타클래스)', '도램마을3단지(웅진스타클래스)', '도램마을4단지(이지더원)',
           '도램마을8단지(행복1차아파트)', '도램마을9단지(제일풍경채)', '라온프라이빗시티 Ⅰ', '라온프라이빗시티 Ⅱ',
           '엘가도램마을12단지', '엘가에코힐(도램마을5단지)', '중흥 그린카운티(13단지)',
           '현대힐스테이트(도램마을15단지)', '수루배마을5단지', '스타힐타워Ⅰ', '스타힐타워Ⅱ',
           '호려울마을 4단지 센트럴파크', '호려울마을10단지(중흥S클래스)', '호려울마을1단지(대방노블랜드)',
           '호려울마을2단지', '호려울마을5단지(제일풍경채)', '호려울마을6단지(모아엘가)',
           '호려울마을8단지(중흥 에코시티)', '호려울마을9단지(한양수자인와이즈시티)', '대신하나로', '주연', '청솔',
           '새뜸마을 3단지', '새뜸마을 4단지', '새뜸마을10단지(더샵힐스테이트)', '새뜸마을11단지(더샵힐스테이트)',
           '새뜸마을12단지(금성백조예미지)', '새뜸마을1단지(메이저시티)', '새뜸마을2단지(메이저시티)',
           '새뜸마을3단지(캐슬&파밀리에)', '새뜸마을4단지(캐슬&파밀리에)', '새뜸마을5단지(메이저시티)',
           '새뜸마을6단지(메이저시티)', '새뜸마을7단지(투머로우시티)', '새뜸마을9단지(금성백조예미지)',
           '새샘마을2단지(한양수자인)', '새샘마을3단지(모아미래도리버시티)', '새샘마을5단지(한양수자인엘시티)',
           '새샘마을6단지(한신더휴펜타힐스)', '새샘마을9단지(중흥S클래스 리버뷰)', '퍼스트시티',
           '대우푸르지오(10단지)', '범지가마을5단지(세종상록어울림)', '범지기마을 4단지',
           '범지기마을11단지(영무예다음)', '범지기마을12단지(중흥S-에코타운)', '범지기마을1단지(한양수자인에듀센텀)',
           '범지기마을3단지(중흥에듀하이)', '범지기마을6단지(세종상록어울림)', '범지기마을7단지 호반에코시티',
           '푸르지오(8단지)', '한신엘리트파크(범지기9단지)', '더샵레이크파크', '더샵센트럴시티', '모닝시티',
           '세종리슈빌S', '한뜰마을1단지(상록데시앙)', '호수의 아침', '다산청정', '대원네스트빌', '정보마을',
           '도원', '성호늘푸른', '재동', '재동(1,2동)', '민석그린', '계룡', '목화', '현대',
           '다원파크리안', '청송', '리치빌 2차 임대아파트(102동)', '리치빌1차', '번암리 리치빌 3차 임대아파트',
           '번암주공', '굿애플 허브', '세종파인시티', '도화', '세종e편한세상', '유니빌', '조형',
           '신흥대우푸르지오', '신흥주공', '조치원 신흥 e편한세상(아)', '세종 스카이뷰', '로하스', '풍산',
           '삼일', '삼정하이츠', '신동아', '조치원신동아파밀리에', '조치원죽림자이', '죽림대우푸르지오',
           '죽림우방유셀', '욱일아파트', '가재마을 5단지', '가재마을10단지', '가재마을11단지', '가재마을12단지',
           '가재마을1단지', '가재마을2단지', '가재마을3단지', '가재마을4단지(센트레빌)', '가재마을6단지',
           '가재마을7단지', '가재마을8단지', '가재마을9단지', '첫마을1단지(퍼스트프라임)',
           '첫마을2단지(퍼스트프라임)', '첫마을3단지(퍼스트프라임)', '첫마을4단지(대우푸르지오)',
           '첫마을5단지(푸르지오)', '첫마을6단지(힐스테이트)', '첫마을7단지(래미안)', '가락마을 19단지',
           '가락마을 2단지', '가락마을18단지', '가락마을1단지(힐데스하임)', '더리치세종의아침(CB4-1BL-2BL)',
           '세종마루투', '가온마을10단지', '가온마을12단지', '가온마을3단지', '가온마을6단지',
           '가온마을8단지(더하이스트)', '해들마을1단지', '해들마을2단지', '해들마을4단지', '해들마을6단지',
           '다산마을(도램마을6단지)', '도램마을 7단지(행복 2차)', '더스테이빌딩', '호려울마을3단지',
           '새뜸마을14단지(더샵힐스테이트)', '새뜸마을2단지', '새뜸마을8단지', '새샘마을1단지', '무궁화',
           '영상마을아파트', '세종3차 굿애플', '리치빌4차', '두진한라', '세종서창행복주택', '대도', 'SR파크센텀',
           '가온마을11단지(세종지웰푸르지오)', '가온마을4단지', '가온마을7단지', '해들마을5단지', '수루배마을1단지',
           '수루배마을2단지', '수루배마을3단지', '수루배마을4단지(세종더샵예미지)', '수루배마을6단지',
           '호려울마을 7단지', '블루빌', '새뜸마을13단지', '가락마을14단지(우남퍼스트빌)', '대광',
           '새샘마을8단지', '서창리 예원드림빌 도시형생활주택', '해밀마을 1단지', '해밀마을 2단지'],
          dtype=object)



## 특정 단어로 시작되는 것만 가져오기


```python
df_sejong[ df_sejong['단지명'].str.startswith('가락마을') ]
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
      <th>전월세구분</th>
      <th>전용면적(㎡)</th>
      <th>보증금(만원)</th>
      <th>월세(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>시</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
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
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>1</th>
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
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>2</th>
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
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>3</th>
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
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>4</th>
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
      <td>세종특별자치시</td>
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
    </tr>
    <tr>
      <th>28924</th>
      <td>202011</td>
      <td>20</td>
      <td>세종특별자치시 고운동</td>
      <td>1408</td>
      <td>0</td>
      <td>가락마을9단지(신동아 파밀리에)</td>
      <td>전세</td>
      <td>59.9940</td>
      <td>25000</td>
      <td>0</td>
      <td>2</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>28925</th>
      <td>202011</td>
      <td>28</td>
      <td>세종특별자치시 고운동</td>
      <td>1408</td>
      <td>0</td>
      <td>가락마을9단지(신동아 파밀리에)</td>
      <td>월세</td>
      <td>84.9860</td>
      <td>2000</td>
      <td>80</td>
      <td>8</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>28926</th>
      <td>202012</td>
      <td>4</td>
      <td>세종특별자치시 고운동</td>
      <td>1408</td>
      <td>0</td>
      <td>가락마을9단지(신동아 파밀리에)</td>
      <td>월세</td>
      <td>84.9860</td>
      <td>14000</td>
      <td>35</td>
      <td>5</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>28927</th>
      <td>202012</td>
      <td>5</td>
      <td>세종특별자치시 고운동</td>
      <td>1408</td>
      <td>0</td>
      <td>가락마을9단지(신동아 파밀리에)</td>
      <td>전세</td>
      <td>59.9720</td>
      <td>27000</td>
      <td>0</td>
      <td>12</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>28928</th>
      <td>202012</td>
      <td>20</td>
      <td>세종특별자치시 고운동</td>
      <td>1408</td>
      <td>0</td>
      <td>가락마을9단지(신동아 파밀리에)</td>
      <td>월세</td>
      <td>59.9720</td>
      <td>2000</td>
      <td>75</td>
      <td>8</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
  </tbody>
</table>
<p>5010 rows × 13 columns</p>
</div>



## 특정 단어가 포함된거 가져오기(중간에 있어도 가능)


```python
df_sejong[ df_sejong['단지명'].str.contains('가락마을') ]
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
      <th>전월세구분</th>
      <th>전용면적(㎡)</th>
      <th>보증금(만원)</th>
      <th>월세(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>시</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
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
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>1</th>
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
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>2</th>
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
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>3</th>
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
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>4</th>
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
      <td>세종특별자치시</td>
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
    </tr>
    <tr>
      <th>29065</th>
      <td>202012</td>
      <td>19</td>
      <td>세종특별자치시 고운동</td>
      <td>1703</td>
      <td>0</td>
      <td>이지더원(가락마을4단지)</td>
      <td>전세</td>
      <td>79.5988</td>
      <td>32000</td>
      <td>0</td>
      <td>12</td>
      <td>2014</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>29066</th>
      <td>202012</td>
      <td>19</td>
      <td>세종특별자치시 고운동</td>
      <td>1703</td>
      <td>0</td>
      <td>이지더원(가락마을4단지)</td>
      <td>전세</td>
      <td>79.5988</td>
      <td>32000</td>
      <td>0</td>
      <td>8</td>
      <td>2014</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>29067</th>
      <td>202012</td>
      <td>19</td>
      <td>세종특별자치시 고운동</td>
      <td>1703</td>
      <td>0</td>
      <td>이지더원(가락마을4단지)</td>
      <td>전세</td>
      <td>59.9853</td>
      <td>16800</td>
      <td>0</td>
      <td>7</td>
      <td>2014</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>29068</th>
      <td>202012</td>
      <td>26</td>
      <td>세종특별자치시 고운동</td>
      <td>1703</td>
      <td>0</td>
      <td>이지더원(가락마을4단지)</td>
      <td>전세</td>
      <td>59.9650</td>
      <td>14700</td>
      <td>0</td>
      <td>4</td>
      <td>2014</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>29069</th>
      <td>202012</td>
      <td>31</td>
      <td>세종특별자치시 고운동</td>
      <td>1703</td>
      <td>0</td>
      <td>이지더원(가락마을4단지)</td>
      <td>전세</td>
      <td>59.9853</td>
      <td>13650</td>
      <td>0</td>
      <td>8</td>
      <td>2014</td>
      <td>세종특별자치시</td>
    </tr>
  </tbody>
</table>
<p>5501 rows × 13 columns</p>
</div>




```python
print("starts with: ", len(df_sejong[ df_sejong['단지명'].str.startswith('가락마을') ]))

print("contains: ", len(df_sejong[ df_sejong['단지명'].str.contains('가락마을') ]))
```

    starts with:  5010
    contains:  5501
    


```python
df_sejong[ df_sejong['단지명'].str.contains("가락마을") ]['단지명'].unique()

# 이지더원(가락마을10단지)이 이상하다는 것을 발견할 수 있음 
```




    array(['가락마을 20단지(호반베르디움5차)', '가락마을11단지(중흥에듀카운티)', '가락마을13단지(대광로제비앙)',
           '가락마을15단지(중흥파크뷰)', '가락마을16단지(에듀그린)', '가락마을17단지(골드클래스)',
           '가락마을21단지(에듀포레)', '가락마을22단지(에듀힐스)', '가락마을3단지(호반베르디움)',
           '가락마을5단지(유승한내들)', '가락마을6단지(중흥S클래스프라디움)', '가락마을7단지(중흥S-클래스프라디움)',
           '가락마을8단지(고운뜰아파트)', '가락마을9단지(신동아 파밀리에)', '이지더원(가락마을10단지)',
           '이지더원(가락마을4단지)', '가락마을 19단지', '가락마을 2단지', '가락마을18단지',
           '가락마을1단지(힐데스하임)', '가락마을14단지(우남퍼스트빌)'], dtype=object)



## 데이터 바꿔주기 


```python
df_sejong.loc[df_sejong['단지명']=='이지더원(가락마을10단지)','단지명']
```




    1788     이지더원(가락마을10단지)
    1789     이지더원(가락마을10단지)
    1790     이지더원(가락마을10단지)
    1791     이지더원(가락마을10단지)
    1792     이지더원(가락마을10단지)
                  ...      
    29015    이지더원(가락마을10단지)
    29016    이지더원(가락마을10단지)
    29017    이지더원(가락마을10단지)
    29018    이지더원(가락마을10단지)
    29019    이지더원(가락마을10단지)
    Name: 단지명, Length: 329, dtype: object




```python
# 다가져올때 
df_sejong.loc[df_sejong['단지명']=='이지더원(가락마을10단지)',:]
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
      <th>전월세구분</th>
      <th>전용면적(㎡)</th>
      <th>보증금(만원)</th>
      <th>월세(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>시</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1788</th>
      <td>201701</td>
      <td>8</td>
      <td>세종특별자치시 고운동</td>
      <td>1400</td>
      <td>0</td>
      <td>이지더원(가락마을10단지)</td>
      <td>전세</td>
      <td>84.986</td>
      <td>18000</td>
      <td>0</td>
      <td>17</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>1789</th>
      <td>201701</td>
      <td>26</td>
      <td>세종특별자치시 고운동</td>
      <td>1400</td>
      <td>0</td>
      <td>이지더원(가락마을10단지)</td>
      <td>월세</td>
      <td>84.986</td>
      <td>5000</td>
      <td>40</td>
      <td>2</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>1790</th>
      <td>201702</td>
      <td>4</td>
      <td>세종특별자치시 고운동</td>
      <td>1400</td>
      <td>0</td>
      <td>이지더원(가락마을10단지)</td>
      <td>전세</td>
      <td>72.497</td>
      <td>15000</td>
      <td>0</td>
      <td>3</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>1791</th>
      <td>201702</td>
      <td>11</td>
      <td>세종특별자치시 고운동</td>
      <td>1400</td>
      <td>0</td>
      <td>이지더원(가락마을10단지)</td>
      <td>전세</td>
      <td>107.698</td>
      <td>20000</td>
      <td>0</td>
      <td>11</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>1792</th>
      <td>201702</td>
      <td>24</td>
      <td>세종특별자치시 고운동</td>
      <td>1400</td>
      <td>0</td>
      <td>이지더원(가락마을10단지)</td>
      <td>월세</td>
      <td>84.986</td>
      <td>3000</td>
      <td>40</td>
      <td>3</td>
      <td>2015</td>
      <td>세종특별자치시</td>
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
    </tr>
    <tr>
      <th>29015</th>
      <td>202012</td>
      <td>4</td>
      <td>세종특별자치시 고운동</td>
      <td>1400</td>
      <td>0</td>
      <td>이지더원(가락마을10단지)</td>
      <td>월세</td>
      <td>72.497</td>
      <td>2000</td>
      <td>70</td>
      <td>4</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>29016</th>
      <td>202012</td>
      <td>6</td>
      <td>세종특별자치시 고운동</td>
      <td>1400</td>
      <td>0</td>
      <td>이지더원(가락마을10단지)</td>
      <td>전세</td>
      <td>107.698</td>
      <td>16800</td>
      <td>0</td>
      <td>4</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>29017</th>
      <td>202012</td>
      <td>6</td>
      <td>세종특별자치시 고운동</td>
      <td>1400</td>
      <td>0</td>
      <td>이지더원(가락마을10단지)</td>
      <td>전세</td>
      <td>107.698</td>
      <td>16800</td>
      <td>0</td>
      <td>4</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>29018</th>
      <td>202012</td>
      <td>28</td>
      <td>세종특별자치시 고운동</td>
      <td>1400</td>
      <td>0</td>
      <td>이지더원(가락마을10단지)</td>
      <td>전세</td>
      <td>84.986</td>
      <td>33000</td>
      <td>0</td>
      <td>7</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>29019</th>
      <td>202012</td>
      <td>28</td>
      <td>세종특별자치시 고운동</td>
      <td>1400</td>
      <td>0</td>
      <td>이지더원(가락마을10단지)</td>
      <td>월세</td>
      <td>72.497</td>
      <td>4000</td>
      <td>50</td>
      <td>14</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
  </tbody>
</table>
<p>329 rows × 13 columns</p>
</div>




```python
df_sejong.loc[df_sejong['단지명']=='이지더원(가락마을10단지)','단지명']='가락마을10단지(이지더원)'
```


```python
df_sejong.loc[df_sejong['단지명']=='가락마을10단지(이지더원)',"단지명"]
```




    1788     가락마을10단지(이지더원)
    1789     가락마을10단지(이지더원)
    1790     가락마을10단지(이지더원)
    1791     가락마을10단지(이지더원)
    1792     가락마을10단지(이지더원)
                  ...      
    29015    가락마을10단지(이지더원)
    29016    가락마을10단지(이지더원)
    29017    가락마을10단지(이지더원)
    29018    가락마을10단지(이지더원)
    29019    가락마을10단지(이지더원)
    Name: 단지명, Length: 329, dtype: object



## 시작 끝 포함 글자 인식

df.str.startswith("시작글자")
df.str.endswith("끝글자")
df.str.contains("포함글자")


```python
df_sejong[df_sejong['단지명'].str.endswith('(골드클래스)')].head()
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
      <th>전월세구분</th>
      <th>전용면적(㎡)</th>
      <th>보증금(만원)</th>
      <th>월세(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>시</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>296</th>
      <td>201701</td>
      <td>7</td>
      <td>세종특별자치시 고운동</td>
      <td>1386</td>
      <td>0</td>
      <td>가락마을17단지(골드클래스)</td>
      <td>월세</td>
      <td>59.9159</td>
      <td>10000</td>
      <td>20</td>
      <td>10</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>297</th>
      <td>201701</td>
      <td>9</td>
      <td>세종특별자치시 고운동</td>
      <td>1386</td>
      <td>0</td>
      <td>가락마을17단지(골드클래스)</td>
      <td>월세</td>
      <td>59.9159</td>
      <td>3000</td>
      <td>45</td>
      <td>13</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>298</th>
      <td>201701</td>
      <td>10</td>
      <td>세종특별자치시 고운동</td>
      <td>1386</td>
      <td>0</td>
      <td>가락마을17단지(골드클래스)</td>
      <td>월세</td>
      <td>59.9159</td>
      <td>5000</td>
      <td>30</td>
      <td>10</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>299</th>
      <td>201701</td>
      <td>14</td>
      <td>세종특별자치시 고운동</td>
      <td>1386</td>
      <td>0</td>
      <td>가락마을17단지(골드클래스)</td>
      <td>전세</td>
      <td>59.9809</td>
      <td>17000</td>
      <td>0</td>
      <td>6</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
    <tr>
      <th>300</th>
      <td>201701</td>
      <td>15</td>
      <td>세종특별자치시 고운동</td>
      <td>1386</td>
      <td>0</td>
      <td>가락마을17단지(골드클래스)</td>
      <td>월세</td>
      <td>59.9159</td>
      <td>4500</td>
      <td>40</td>
      <td>5</td>
      <td>2015</td>
      <td>세종특별자치시</td>
    </tr>
  </tbody>
</table>
</div>


