```python
import pandas as pd
```

DataFrame 읽기
df = pd.read_csv(filepath)

filepath : 파일 경로 ('p1/p2/file.csv' 형태)

%pwd :경로 확인


```python
%pwd
```




    'D:\\anaconda\\★studying'




```python
iris_data=pd.read_csv("D:/anaconda/00.studying/data/iris.csv")
```

다른 폴더의 있는 경우 그냥 pd.read_csv('../data/iris.csv')가 안 먹힘. 따라서 전체 주소를 가져오는데 대신 \는 /로 변경을 해준다. 


```python
iris_data
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
      <th>sepal length</th>
      <th>sepal width</th>
      <th>petal length</th>
      <th>petal width</th>
      <th>target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>145</th>
      <td>6.7</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.3</td>
      <td>Iris-virginica</td>
    </tr>
    <tr>
      <th>146</th>
      <td>6.3</td>
      <td>2.5</td>
      <td>5.0</td>
      <td>1.9</td>
      <td>Iris-virginica</td>
    </tr>
    <tr>
      <th>147</th>
      <td>6.5</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.0</td>
      <td>Iris-virginica</td>
    </tr>
    <tr>
      <th>148</th>
      <td>6.2</td>
      <td>3.4</td>
      <td>5.4</td>
      <td>2.3</td>
      <td>Iris-virginica</td>
    </tr>
    <tr>
      <th>149</th>
      <td>5.9</td>
      <td>3.0</td>
      <td>5.1</td>
      <td>1.8</td>
      <td>Iris-virginica</td>
    </tr>
  </tbody>
</table>
<p>150 rows × 5 columns</p>
</div>



## DATAFRAME저장

-데이터안에 한국어가 있다면 encoding해줘야함 
-header=True 컬럼이 저장이 됨 

**df.to_csv(filepath, header=True, index=True, encoding='utf-8')


```python
iris_data.to_csv("example.csv", header=True, index=False, encoding='utf-8')
```


```python
pd.read_csv("example.csv")
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
      <th>sepal length</th>
      <th>sepal width</th>
      <th>petal length</th>
      <th>petal width</th>
      <th>target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>145</th>
      <td>6.7</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.3</td>
      <td>Iris-virginica</td>
    </tr>
    <tr>
      <th>146</th>
      <td>6.3</td>
      <td>2.5</td>
      <td>5.0</td>
      <td>1.9</td>
      <td>Iris-virginica</td>
    </tr>
    <tr>
      <th>147</th>
      <td>6.5</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.0</td>
      <td>Iris-virginica</td>
    </tr>
    <tr>
      <th>148</th>
      <td>6.2</td>
      <td>3.4</td>
      <td>5.4</td>
      <td>2.3</td>
      <td>Iris-virginica</td>
    </tr>
    <tr>
      <th>149</th>
      <td>5.9</td>
      <td>3.0</td>
      <td>5.1</td>
      <td>1.8</td>
      <td>Iris-virginica</td>
    </tr>
  </tbody>
</table>
<p>150 rows × 5 columns</p>
</div>



## DataFrame 선언

df=pd.DataFrame(data)

pandas의 기본 객체
Series는 리스트와 비슷하지만 인덱스 값을 가지고 있음 
index는 기본적으로 0부터 자동으로 생성


```python
list_1=[1,1,1,1]
list_1
```




    [1, 1, 1, 1]




```python
# 데이터 프레임 선언
pd.DataFrame(list_1)
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Series 형식
Series_1=pd.Series([1,1,1,1])
Series_1
```




    0    1
    1    1
    2    1
    3    1
    dtype: int64




```python
# 인덱스를 지정선언해서 넣을수도 있음
Series_2=pd.Series([1,1,1,1], index=['2022-11-06',2,"dd",43])
```


```python
Series_2
```




    2022-11-06    1
    2             1
    dd            1
    43            1
    dtype: int64



## DataFrame 출력
df.head(n) #처음 n개만 출력되고 미지정하면 5개가 출력됨
df.tail(n) #마지막 n개만 출력되고 미지정하면 5개만 출력됨 


```python
iris_data.tail(3)
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
      <th>sepal length</th>
      <th>sepal width</th>
      <th>petal length</th>
      <th>petal width</th>
      <th>target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>147</th>
      <td>6.5</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.0</td>
      <td>Iris-virginica</td>
    </tr>
    <tr>
      <th>148</th>
      <td>6.2</td>
      <td>3.4</td>
      <td>5.4</td>
      <td>2.3</td>
      <td>Iris-virginica</td>
    </tr>
    <tr>
      <th>149</th>
      <td>5.9</td>
      <td>3.0</td>
      <td>5.1</td>
      <td>1.8</td>
      <td>Iris-virginica</td>
    </tr>
  </tbody>
</table>
</div>



## DataFrame 요약/통계정보 확인★★

df.info() # 총 데이터 건수와 데이터 타입, Null건수 확인
df.describe() # 숫자형 컬럼들의 n-percentile분포도, 평균값, 최댓값, 최솟값 확인
df['컬럼명'].min() 또는 df['컬럼명'].max() # 해당 컬럼의 min, max 값을 확인

.size : 개수 반환
.shape : 튜플형태로 shape반환
.unique(): 유일한 값만 ndarray로 반환
.count() : NaN을 제외한 개수를 반환
.mean(): NaN을 제외한 평균
.value_counts(): NaN을 제외하고 각 값들의 빈도를 반



```python
iris_data.info()
# rangeindex가 보이는데 150개의 indext가 있고 0~149개라는거 
#0~4 총 5개의 타겟값이 있다는거 
# non-null은 null이 하나도 없다는거 
# object=문자열 
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 150 entries, 0 to 149
    Data columns (total 5 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   sepal length  150 non-null    float64
     1   sepal width   150 non-null    float64
     2   petal length  150 non-null    float64
     3   petal width   150 non-null    float64
     4   target        150 non-null    object 
    dtypes: float64(4), object(1)
    memory usage: 6.0+ KB
    


```python
iris_data.describe()
# EBA를 하라고해서 무조건 그래프를 보는건아니고 
# 먼저 데이터에 null값이 있는지 확인하고
# 데이터의 기초통계량 (describe)를 보는게 좋음 
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
      <th>sepal length</th>
      <th>sepal width</th>
      <th>petal length</th>
      <th>petal width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>150.000000</td>
      <td>150.000000</td>
      <td>150.000000</td>
      <td>150.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>5.843333</td>
      <td>3.054000</td>
      <td>3.758667</td>
      <td>1.198667</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.828066</td>
      <td>0.433594</td>
      <td>1.764420</td>
      <td>0.763161</td>
    </tr>
    <tr>
      <th>min</th>
      <td>4.300000</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>0.100000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>5.100000</td>
      <td>2.800000</td>
      <td>1.600000</td>
      <td>0.300000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>5.800000</td>
      <td>3.000000</td>
      <td>4.350000</td>
      <td>1.300000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>6.400000</td>
      <td>3.300000</td>
      <td>5.100000</td>
      <td>1.800000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>7.900000</td>
      <td>4.400000</td>
      <td>6.900000</td>
      <td>2.500000</td>
    </tr>
  </tbody>
</table>
</div>




```python
iris_data['sepal length'].min()
# 범주 하나의 값만 살펴볼 수 있음 
```




    4.3




```python
iris_data['sepal length'].size
# 데이터의 총 갯수 
```




    150




```python
iris_data['sepal length'].shape
# 열이 없다는걸 확인할 수 있다. 
```




    (150,)




```python
iris_data[['sepal length']].shape
# [ ]로 한번 더 감싸주면 dataframe화 할수가 있음. 
# Series->Dataframe
# 열이 생김(dataframe특징 )
```




    (150, 1)




```python
iris_data[['sepal length']]
# 만약에 []를 없애면 표 없이 그냥 값만 나오게됨 
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
      <th>sepal length</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>145</th>
      <td>6.7</td>
    </tr>
    <tr>
      <th>146</th>
      <td>6.3</td>
    </tr>
    <tr>
      <th>147</th>
      <td>6.5</td>
    </tr>
    <tr>
      <th>148</th>
      <td>6.2</td>
    </tr>
    <tr>
      <th>149</th>
      <td>5.9</td>
    </tr>
  </tbody>
</table>
<p>150 rows × 1 columns</p>
</div>




```python
iris_data['target'].unique()
# 중복을 제거하고 유일한 값만 
```




    array(['Iris-setosa', 'Iris-versicolor', 'Iris-virginica'], dtype=object)




```python
iris_data['target'].count()
# 현재 데이터 값 
```




    150




```python
iris_data['target'].value_counts()
# unique값 별로 데이터의 개수를 보여준다. 
# 범주형 데이터를 확인할때 많이 씀 
```




    Iris-setosa        50
    Iris-versicolor    50
    Iris-virginica     50
    Name: target, dtype: int64



## DataFrame 인덱스 확인, 추가, 리셋

df.index      # 인덱스 확인
df.set_index(keys,drop=True,append=False,inplace=True)  # 인덱스 추가 
df.reset_index(drop=False,inplace=False) # 인덱스 리셋


```python
iris_data.index
# 10~150까지 1단위로 증가한다는거 
```




    RangeIndex(start=0, stop=150, step=1)




```python
iris_data.set_index('target',drop=True,append=False,inplace=True)
# Target을 index로 두고 데이터를 보고싶을때 
# inplace=True를 하지않으면 값이 고정되지 않음 
```


```python
iris_data
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
      <th>sepal length</th>
      <th>sepal width</th>
      <th>petal length</th>
      <th>petal width</th>
    </tr>
    <tr>
      <th>target</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Iris-setosa</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>Iris-setosa</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>Iris-setosa</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>Iris-setosa</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>Iris-setosa</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Iris-virginica</th>
      <td>6.7</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.3</td>
    </tr>
    <tr>
      <th>Iris-virginica</th>
      <td>6.3</td>
      <td>2.5</td>
      <td>5.0</td>
      <td>1.9</td>
    </tr>
    <tr>
      <th>Iris-virginica</th>
      <td>6.5</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>Iris-virginica</th>
      <td>6.2</td>
      <td>3.4</td>
      <td>5.4</td>
      <td>2.3</td>
    </tr>
    <tr>
      <th>Iris-virginica</th>
      <td>5.9</td>
      <td>3.0</td>
      <td>5.1</td>
      <td>1.8</td>
    </tr>
  </tbody>
</table>
<p>150 rows × 4 columns</p>
</div>




```python
iris_data.reset_index(inplace=True)
# 데이터를 다시 원상복구 시키는법 
```


```python
iris_data.head()
# index가 0~4로 표시되어서 복구된거를 알수있음 
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
      <th>target</th>
      <th>sepal length</th>
      <th>sepal width</th>
      <th>petal length</th>
      <th>petal width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Iris-setosa</td>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Iris-setosa</td>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Iris-setosa</td>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Iris-setosa</td>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Iris-setosa</td>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>
</div>



## DataFrame 컬럼명 확인, 변경 

df.values[:5] #value확인 

df.columns    # 컬럼명 확인
df.columns = ['new1,'new2'] #컬럼명 변경 되지만 갯수는 같아야함 
df.rename( { 'old1':'new1', 'old2':'new2' }, axis='columns' ,inplace=True) 
df.columns = df.columns.str.replace('기존문자', '대체할 문자')    # 컬럼명 특정문자 대체
df.drop(['컬럼명'],axis=1,inplace=True)


```python
iris_data.columns
# 1차원 배열의 형식으로. 5개의 컬럼이 있는걸 확인함 
```




    Index(['target', 'sepal length', 'sepal width', 'petal length', 'petal width'], dtype='object')




```python
iris_data.columns=['a','b','c','d','e']
iris_data.head()

#컬럼값 이름을 변경해봄 
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
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Iris-setosa</td>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Iris-setosa</td>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Iris-setosa</td>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Iris-setosa</td>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Iris-setosa</td>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>
</div>




```python
iris_data.columns = ['Target','sepal%%length', 'sepal%%width', 'petal%%length', 'Petal%%width']
iris_data.head(1)
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
      <th>Target</th>
      <th>sepal%%length</th>
      <th>sepal%%width</th>
      <th>petal%%length</th>
      <th>Petal%%width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Iris-setosa</td>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>
</div>




```python
iris_data.rename({"Target":"target", "Petal%%width" : 'petal_width'},axis='columns',inplace=True)
iris_data.head(1)
# 이 문자열이 어디에 있는지 지정하기 axis='columns' 또는 axis=1로 해도됨
# 마찬가지로 inplace=True여야 반영됨 
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
      <th>target</th>
      <th>sepal%%length</th>
      <th>sepal%%width</th>
      <th>petal%%length</th>
      <th>petal_width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Iris-setosa</td>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>
</div>




```python
iris_data.columns=iris_data.columns.str.replace('%%','_')
iris_data.head(1)
# 컬럼내에 특정한 문자를 다른걸로 변환하는거 
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
      <th>target</th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Iris-setosa</td>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>
</div>



## DataFrame컬럼 타입 변경


```python
iris_data.info()
# object는 문자형
# float는 소숫점 표시하는거 
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 150 entries, 0 to 149
    Data columns (total 5 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   target        150 non-null    object 
     1   sepal_length  150 non-null    float64
     2   sepal_width   150 non-null    float64
     3   petal_length  150 non-null    float64
     4   petal_width   150 non-null    float64
    dtypes: float64(4), object(1)
    memory usage: 6.0+ KB
    


```python
iris_data['sepal_lenght']=iris_data['sepal_length'].astype(int)
```


```python
iris_data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 150 entries, 0 to 149
    Data columns (total 6 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   target        150 non-null    object 
     1   sepal_length  150 non-null    float64
     2   sepal_width   150 non-null    float64
     3   petal_length  150 non-null    float64
     4   petal_width   150 non-null    float64
     5   sepal_lenght  150 non-null    int32  
    dtypes: float64(4), int32(1), object(1)
    memory usage: 6.6+ KB
    
