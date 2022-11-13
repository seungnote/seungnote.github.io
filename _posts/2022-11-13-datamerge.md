데이터 결합

->머신러닝, 통계분석, 라이브러리에서 요구하는 데이터 형식이 있는데 그렇게 만드는 방법중 하나 

**R과 다른점: 결합하려는 데이터프레임의 행/열 개수가 안맞아도 NaN값이 채워짐 

## 행결합: 데이터프레임 붙이기  pd.concat()



```python
import pandas as pd
customer1=pd.DataFrame({'id':['c01','c02','c03','c04'],
                       'last_name':['Lee','Kim','Choi','Park']},
                      index=[0,1,2,3])
customer1
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
      <th>id</th>
      <th>last_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
    </tr>
  </tbody>
</table>
</div>




```python
customer2=pd.DataFrame({'id':['c05','c06','c07'],
                       'Last_name':['Lim','Bae','Kim'],
                       'age':['23','34','45']},
                      index=[0,1,2])
customer2
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
      <th>id</th>
      <th>Last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.concat([customer1,customer2])
# last_name 을 일치 시켜줘야함 
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
      <th>id</th>
      <th>last_name</th>
      <th>Last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>c05</td>
      <td>NaN</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c06</td>
      <td>NaN</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c07</td>
      <td>NaN</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 열의 값 바꾸기 
customer2.columns=['id','last_name','age']
customer2
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
      <th>id</th>
      <th>last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.concat([customer1,customer2])
# 이제 결합 성공 
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
      <th>id</th>
      <th>last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 인덱스가 1,2,3,0,1,2로 되기때문에 다시 재배열해줌
# 꼭 새로운 이름으로 저장해주는게 좋음 
customer=pd.concat([customer1,customer2]).reset_index(drop=True)
customer
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
      <th>id</th>
      <th>last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>6</th>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 처음부터 index순서 맞춰주는 방법도 있음 
result=pd.concat([customer1,customer2],ignore_index=True)
result
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
      <th>id</th>
      <th>last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>6</th>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
result.reset_index()
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
      <th>index</th>
      <th>id</th>
      <th>last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>c01</td>
      <td>Lee</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>c02</td>
      <td>Kim</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>c03</td>
      <td>Choi</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>c04</td>
      <td>Park</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>



## 열결합
pd.concat([df1,df2...], axis=1)

df1->기준 df2-> 두번째 
**axix=1은 열 방향으로 데이터프레임을 붙임 


```python
result2=pd.concat([customer2,customer1],axis=1)
result2
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
      <th>id</th>
      <th>last_name</th>
      <th>age</th>
      <th>id</th>
      <th>last_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
      <td>c01</td>
      <td>Lee</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
      <td>c02</td>
      <td>Kim</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
      <td>c03</td>
      <td>Choi</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>c04</td>
      <td>Park</td>
    </tr>
  </tbody>
</table>
</div>



## 시리즈 열결합

시리즈가 여러개 모여있는게 데이터프레임이라고함 
시리즈끼리 열로 붙이면 데이터프레임이됨 


```python
# grade 7개 행
# grade2는 6개의 행을 가짐 

grade=pd.Series(['A','B','C','A','D','C','B'],name='grade')
grade2=pd.Series(['A','B','C','A','D','C'],name='grade')
```


```python
# 열로 붙여보기 
result3=pd.concat([grade,grade2],axis=1)
result3
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
      <th>grade</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>C</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A</td>
      <td>A</td>
    </tr>
    <tr>
      <th>4</th>
      <td>D</td>
      <td>D</td>
    </tr>
    <tr>
      <th>5</th>
      <td>C</td>
      <td>C</td>
    </tr>
    <tr>
      <th>6</th>
      <td>B</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 그냥 grade만 출력하면 데이터프레임은 아니지만 합쳐지면서 됨 
grade
```




    0    A
    1    B
    2    C
    3    A
    4    D
    5    C
    6    B
    Name: grade, dtype: object



## 시리즈 행결합

시리즈를 행으로 묶으면 그냥 시리즈가됨 


```python
sr1=pd.Series(['e0','e1','e2','c3'], name='e')
sr2=pd.Series(['g0','g1','g2','g3'], name='g')

# 열 방향으로 연결하면 데이터프레임됨
result4=pd.concat([sr1,sr2],axis=1)
print(result4)
print(type(result4))

# 행방향으로 연결하면 시리즈 유지 
result5=pd.concat([sr1,sr2],ignore_index=True)
print(result5)
print(type(result5))
```

        e   g
    0  e0  g0
    1  e1  g1
    2  e2  g2
    3  c3  g3
    <class 'pandas.core.frame.DataFrame'>
    0    e0
    1    e1
    2    e2
    3    c3
    4    g0
    5    g1
    6    g2
    7    g3
    dtype: object
    <class 'pandas.core.series.Series'>
    

## Merge: 존재하는 고유값 기준으로 병합

디폴트 값
pd.merge(df_left,df_right,how='inner',on=None) 

how에는 inner,outer,left,right이 들어갈수있다 


```python
id_name=pd.DataFrame({'ID':['c01','c02','c03','c04','c05','c06','c07'],
                     'last_name':['Lee','Kim','Choi','Park','Lim','Bae','Kim']})
id_number=pd.DataFrame({'id':['c03','c04','c05','c06','c07','c08','c09'],
                     'number':[3,1,0,7,3,4,1]})
```


```python
id_name
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
      <th>ID</th>
      <th>last_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c05</td>
      <td>Lim</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c06</td>
      <td>Bae</td>
    </tr>
    <tr>
      <th>6</th>
      <td>c07</td>
      <td>Kim</td>
    </tr>
  </tbody>
</table>
</div>




```python
id_number
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
      <th>id</th>
      <th>number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c03</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c04</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c05</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c06</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c07</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c08</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>c09</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# ID 와 id 맞추기
id_number.columns=['ID','number']
id_number
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
      <th>ID</th>
      <th>number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c03</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c04</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c05</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c06</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c07</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c08</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>c09</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.concat([id_name,id_number],axis=1)
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
      <th>ID</th>
      <th>last_name</th>
      <th>ID</th>
      <th>number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
      <td>c03</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
      <td>c04</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
      <td>c05</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
      <td>c06</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c05</td>
      <td>Lim</td>
      <td>c07</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c06</td>
      <td>Bae</td>
      <td>c08</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>c07</td>
      <td>Kim</td>
      <td>c09</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 교집합
pd.merge(id_name,id_number,how='inner',on='ID')
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
      <th>ID</th>
      <th>last_name</th>
      <th>number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c03</td>
      <td>Choi</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c04</td>
      <td>Park</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c05</td>
      <td>Lim</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c06</td>
      <td>Bae</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c07</td>
      <td>Kim</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 왼쪽으로 붙임 
pd.merge(id_name,id_number,how='left',on='ID')
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
      <th>ID</th>
      <th>last_name</th>
      <th>number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c05</td>
      <td>Lim</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c06</td>
      <td>Bae</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>c07</td>
      <td>Kim</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 모든값 outer
pd.merge(id_name,id_number,how='outer',on='ID')
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
      <th>ID</th>
      <th>last_name</th>
      <th>number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c05</td>
      <td>Lim</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c06</td>
      <td>Bae</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>c07</td>
      <td>Kim</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>c08</td>
      <td>NaN</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>c09</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>


