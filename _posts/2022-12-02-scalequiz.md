---
title:  "[Python] 데이터전처리-표준화.정규화QUIZ" 

categories:
  - quiz
tags:
  - [Python,ADP,quiz,class101]

toc: true
toc_sticky: true

date: 2022-12-02

---

```python
import pandas as pd 
from sklearn.model_selection import train_test_split
X = pd.read_csv('D:/anaconda/00.studying/data/빅분기_X_train.csv',encoding='cp949')
y = pd.read_csv('D:/anaconda/00.studying/data/빅분기_y_train.csv',encoding='cp949')
```


```python
X
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
      <th>cust_id</th>
      <th>총구매액</th>
      <th>최대구매액</th>
      <th>환불금액</th>
      <th>주구매상품</th>
      <th>주구매지점</th>
      <th>내점일수</th>
      <th>내점당구매건수</th>
      <th>주말방문비율</th>
      <th>구매주기</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>68282840</td>
      <td>11264000</td>
      <td>6860000.0</td>
      <td>기타</td>
      <td>강남점</td>
      <td>19</td>
      <td>3.894737</td>
      <td>0.527027</td>
      <td>17</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2136000</td>
      <td>2136000</td>
      <td>300000.0</td>
      <td>스포츠</td>
      <td>잠실점</td>
      <td>2</td>
      <td>1.500000</td>
      <td>0.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3197000</td>
      <td>1639000</td>
      <td>NaN</td>
      <td>남성 캐주얼</td>
      <td>관악점</td>
      <td>2</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>16077620</td>
      <td>4935000</td>
      <td>NaN</td>
      <td>기타</td>
      <td>광주점</td>
      <td>18</td>
      <td>2.444444</td>
      <td>0.318182</td>
      <td>16</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>29050000</td>
      <td>24000000</td>
      <td>NaN</td>
      <td>보석</td>
      <td>본  점</td>
      <td>2</td>
      <td>1.500000</td>
      <td>0.000000</td>
      <td>85</td>
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
    </tr>
    <tr>
      <th>3495</th>
      <td>3495</td>
      <td>3175200</td>
      <td>3042900</td>
      <td>NaN</td>
      <td>골프</td>
      <td>본  점</td>
      <td>1</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3496</th>
      <td>3496</td>
      <td>29628600</td>
      <td>7200000</td>
      <td>6049600.0</td>
      <td>시티웨어</td>
      <td>부산본점</td>
      <td>8</td>
      <td>1.625000</td>
      <td>0.461538</td>
      <td>40</td>
    </tr>
    <tr>
      <th>3497</th>
      <td>3497</td>
      <td>75000</td>
      <td>75000</td>
      <td>NaN</td>
      <td>주방용품</td>
      <td>창원점</td>
      <td>1</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3498</th>
      <td>3498</td>
      <td>1875000</td>
      <td>1000000</td>
      <td>NaN</td>
      <td>화장품</td>
      <td>본  점</td>
      <td>2</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>39</td>
    </tr>
    <tr>
      <th>3499</th>
      <td>3499</td>
      <td>263101550</td>
      <td>34632000</td>
      <td>5973000.0</td>
      <td>기타</td>
      <td>본  점</td>
      <td>38</td>
      <td>2.421053</td>
      <td>0.467391</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
<p>3500 rows × 10 columns</p>
</div>




```python
y
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
      <th>cust_id</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3495</th>
      <td>3495</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3496</th>
      <td>3496</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3497</th>
      <td>3497</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3498</th>
      <td>3498</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3499</th>
      <td>3499</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>3500 rows × 2 columns</p>
</div>



## 빅분기 X_train, 빅분기 y_train 데이터의 cust_id를 인덱스로 설정하세요 



```python
X.set_index('cust_id',drop=True,append=False,inplace=True)
X
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
      <th>총구매액</th>
      <th>최대구매액</th>
      <th>환불금액</th>
      <th>주구매상품</th>
      <th>주구매지점</th>
      <th>내점일수</th>
      <th>내점당구매건수</th>
      <th>주말방문비율</th>
      <th>구매주기</th>
    </tr>
    <tr>
      <th>cust_id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>68282840</td>
      <td>11264000</td>
      <td>6860000.0</td>
      <td>기타</td>
      <td>강남점</td>
      <td>19</td>
      <td>3.894737</td>
      <td>0.527027</td>
      <td>17</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2136000</td>
      <td>2136000</td>
      <td>300000.0</td>
      <td>스포츠</td>
      <td>잠실점</td>
      <td>2</td>
      <td>1.500000</td>
      <td>0.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3197000</td>
      <td>1639000</td>
      <td>NaN</td>
      <td>남성 캐주얼</td>
      <td>관악점</td>
      <td>2</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16077620</td>
      <td>4935000</td>
      <td>NaN</td>
      <td>기타</td>
      <td>광주점</td>
      <td>18</td>
      <td>2.444444</td>
      <td>0.318182</td>
      <td>16</td>
    </tr>
    <tr>
      <th>4</th>
      <td>29050000</td>
      <td>24000000</td>
      <td>NaN</td>
      <td>보석</td>
      <td>본  점</td>
      <td>2</td>
      <td>1.500000</td>
      <td>0.000000</td>
      <td>85</td>
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
    </tr>
    <tr>
      <th>3495</th>
      <td>3175200</td>
      <td>3042900</td>
      <td>NaN</td>
      <td>골프</td>
      <td>본  점</td>
      <td>1</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3496</th>
      <td>29628600</td>
      <td>7200000</td>
      <td>6049600.0</td>
      <td>시티웨어</td>
      <td>부산본점</td>
      <td>8</td>
      <td>1.625000</td>
      <td>0.461538</td>
      <td>40</td>
    </tr>
    <tr>
      <th>3497</th>
      <td>75000</td>
      <td>75000</td>
      <td>NaN</td>
      <td>주방용품</td>
      <td>창원점</td>
      <td>1</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3498</th>
      <td>1875000</td>
      <td>1000000</td>
      <td>NaN</td>
      <td>화장품</td>
      <td>본  점</td>
      <td>2</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>39</td>
    </tr>
    <tr>
      <th>3499</th>
      <td>263101550</td>
      <td>34632000</td>
      <td>5973000.0</td>
      <td>기타</td>
      <td>본  점</td>
      <td>38</td>
      <td>2.421053</td>
      <td>0.467391</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
<p>3500 rows × 9 columns</p>
</div>




```python
y.set_index('cust_id',drop=True,append=False,inplace=True)
y
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
      <th>gender</th>
    </tr>
    <tr>
      <th>cust_id</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>3495</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3496</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3497</th>
      <td>0</td>
    </tr>
    <tr>
      <th>3498</th>
      <td>0</td>
    </tr>
    <tr>
      <th>3499</th>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>3500 rows × 1 columns</p>
</div>



## X_train과 y_train데이터를 y값을 기준으로 층화추출하여 7:3으로 데이터를 나누세요 (X_train, X_val, y_train,y_val)



```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, shuffle=True, stratify=y, random_state=1004)
```


```python
y.value_counts()
```




    gender
    0         2184
    1         1316
    dtype: int64




```python
y_train['gender'].value_counts()
```




    0    1529
    1     921
    Name: gender, dtype: int64



## X_train과 X_val의 수치형 변수들만 StandardScaler를 이용하여 표준화 시키세요. 


```python
X_train.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 2450 entries, 1136 to 1473
    Data columns (total 9 columns):
     #   Column   Non-Null Count  Dtype  
    ---  ------   --------------  -----  
     0   총구매액     2450 non-null   int64  
     1   최대구매액    2450 non-null   int64  
     2   환불금액     845 non-null    float64
     3   주구매상품    2450 non-null   object 
     4   주구매지점    2450 non-null   object 
     5   내점일수     2450 non-null   int64  
     6   내점당구매건수  2450 non-null   float64
     7   주말방문비율   2450 non-null   float64
     8   구매주기     2450 non-null   int64  
    dtypes: float64(3), int64(4), object(2)
    memory usage: 191.4+ KB
    


```python
from sklearn.preprocessing import StandardScaler
```


```python
scaler = StandardScaler()
```


```python
X_train.head()
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
      <th>총구매액</th>
      <th>최대구매액</th>
      <th>환불금액</th>
      <th>주구매상품</th>
      <th>주구매지점</th>
      <th>내점일수</th>
      <th>내점당구매건수</th>
      <th>주말방문비율</th>
      <th>구매주기</th>
    </tr>
    <tr>
      <th>cust_id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1136</th>
      <td>85405340</td>
      <td>17050000</td>
      <td>750000.0</td>
      <td>가공식품</td>
      <td>노원점</td>
      <td>34</td>
      <td>1.823529</td>
      <td>0.241935</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1779</th>
      <td>92570650</td>
      <td>20213000</td>
      <td>27758000.0</td>
      <td>기타</td>
      <td>본  점</td>
      <td>28</td>
      <td>2.142857</td>
      <td>0.250000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1456</th>
      <td>21774000</td>
      <td>9205000</td>
      <td>NaN</td>
      <td>화장품</td>
      <td>본  점</td>
      <td>8</td>
      <td>1.125000</td>
      <td>0.222222</td>
      <td>27</td>
    </tr>
    <tr>
      <th>2980</th>
      <td>560540800</td>
      <td>30000000</td>
      <td>18276400.0</td>
      <td>트래디셔널</td>
      <td>본  점</td>
      <td>50</td>
      <td>1.960000</td>
      <td>0.448980</td>
      <td>7</td>
    </tr>
    <tr>
      <th>614</th>
      <td>143259270</td>
      <td>11750000</td>
      <td>621000.0</td>
      <td>기타</td>
      <td>부평점</td>
      <td>55</td>
      <td>5.654545</td>
      <td>0.450161</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
scaler.fit(X_train.iloc[:,[0,1,2,5,6,7]])
```




<style>#sk-container-id-1 {color: black;background-color: white;}#sk-container-id-1 pre{padding: 0;}#sk-container-id-1 div.sk-toggleable {background-color: white;}#sk-container-id-1 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-1 label.sk-toggleable__label-arrow:before {content: "▸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-1 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-1 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-1 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "▾";}#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-1 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-1 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-1 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-1 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-1 div.sk-item {position: relative;z-index: 1;}#sk-container-id-1 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-1 div.sk-item::before, #sk-container-id-1 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-1 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-1 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-1 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-1 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-1 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-1 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-1 div.sk-label-container {text-align: center;}#sk-container-id-1 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-1 div.sk-text-repr-fallback {display: none;}</style><div id="sk-container-id-1" class="sk-top-container"><div class="sk-text-repr-fallback"><pre>StandardScaler()</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden><div class="sk-item"><div class="sk-estimator sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-1" type="checkbox" checked><label for="sk-estimator-id-1" class="sk-toggleable__label sk-toggleable__label-arrow">StandardScaler</label><div class="sk-toggleable__content"><pre>StandardScaler()</pre></div></div></div></div></div>




```python
scaler.mean_
```




    array([9.52130713e+07, 2.03305629e+07, 2.48880231e+07, 1.93097959e+01,
           2.84451506e+00, 3.03264308e-01])




```python

scaler.var_
```




    array([2.86750704e+16, 1.14340599e+15, 2.53053269e+15, 7.39868516e+02,
           3.76202129e+00, 8.24892380e-02])




```python
scaler.transform(X_train.iloc[:,[0,1,2,5,6,7]])
```




    array([[-0.05791837, -0.09701707, -0.4798392 ,  0.54007062, -0.52639168,
            -0.21353349],
           [-0.0156045 , -0.00347672,  0.0570522 ,  0.31948664, -0.36175522,
            -0.18545461],
           [-0.43368553, -0.3290196 ,         nan, -0.41579331, -0.88653392,
            -0.28217073],
           ...,
           [ 1.23953851,  0.04153384,         nan,  0.13566665,  0.39399016,
            -0.38471312],
           [-0.46493638, -0.43412014,         nan, -0.41579331, -0.17762234,
            -0.35954363],
           [-0.53007902, -0.51607071,         nan, -0.63637729, -0.43540837,
            -0.18545461]])




```python
pd.DataFrame(scaler.transform(X_train.iloc[:,[0,1,2,5,6,7]]),
            columns=X_train.columns[[0,1,2,5,6,7]]
            +'-scaled')
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
      <th>총구매액-scaled</th>
      <th>최대구매액-scaled</th>
      <th>환불금액-scaled</th>
      <th>내점일수-scaled</th>
      <th>내점당구매건수-scaled</th>
      <th>주말방문비율-scaled</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.057918</td>
      <td>-0.097017</td>
      <td>-0.479839</td>
      <td>0.540071</td>
      <td>-0.526392</td>
      <td>-0.213533</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.015604</td>
      <td>-0.003477</td>
      <td>0.057052</td>
      <td>0.319487</td>
      <td>-0.361755</td>
      <td>-0.185455</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.433686</td>
      <td>-0.329020</td>
      <td>NaN</td>
      <td>-0.415793</td>
      <td>-0.886534</td>
      <td>-0.282171</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.747936</td>
      <td>0.285957</td>
      <td>-0.131432</td>
      <td>1.128295</td>
      <td>-0.456031</td>
      <td>0.507349</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.283731</td>
      <td>-0.253756</td>
      <td>-0.482404</td>
      <td>1.312115</td>
      <td>1.448773</td>
      <td>0.511461</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2445</th>
      <td>-0.537467</td>
      <td>-0.483244</td>
      <td>NaN</td>
      <td>-0.673141</td>
      <td>-0.435408</td>
      <td>-1.055900</td>
    </tr>
    <tr>
      <th>2446</th>
      <td>-0.544553</td>
      <td>-0.512522</td>
      <td>NaN</td>
      <td>-0.673141</td>
      <td>-0.950980</td>
      <td>2.425881</td>
    </tr>
    <tr>
      <th>2447</th>
      <td>1.239539</td>
      <td>0.041534</td>
      <td>NaN</td>
      <td>0.135667</td>
      <td>0.393990</td>
      <td>-0.384713</td>
    </tr>
    <tr>
      <th>2448</th>
      <td>-0.464936</td>
      <td>-0.434120</td>
      <td>NaN</td>
      <td>-0.415793</td>
      <td>-0.177622</td>
      <td>-0.359544</td>
    </tr>
    <tr>
      <th>2449</th>
      <td>-0.530079</td>
      <td>-0.516071</td>
      <td>NaN</td>
      <td>-0.636377</td>
      <td>-0.435408</td>
      <td>-0.185455</td>
    </tr>
  </tbody>
</table>
<p>2450 rows × 6 columns</p>
</div>


