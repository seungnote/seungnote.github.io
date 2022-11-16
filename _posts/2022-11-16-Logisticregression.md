---
title:  "[Python] 머신러닝_이진논리회귀 실습" 

categories:
  - Python
tags:
  - [Python,ADP,machine_learing]

toc: true
toc_sticky: true

date: 2022-11-16

---
## 이진 논리회귀(Logistic regression)
-0이냐 1이냐 구분하는 논리회귀


```python
import os
os.environ['KAGGLE_USERNAME'] = 'seungnote' # username
os.environ['KAGGLE_KEY'] = 'bc254ae94554f39d41fcab91537514ad' # key
```


```python
!kaggle datasets download -d heptapod/titanic
```

    Downloading titanic.zip to D:\anaconda\00.studying
    
    

    
      0%|          | 0.00/10.8k [00:00<?, ?B/s]
    100%|##########| 10.8k/10.8k [00:00<00:00, 11.1MB/s]
    


```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.optimizers import Adam, SGD
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt 
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
```


```python
df=pd.read_csv("D:/anaconda/00.studying/titanic/train_and_test2.csv")
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
      <th>Passengerid</th>
      <th>Age</th>
      <th>Fare</th>
      <th>Sex</th>
      <th>sibsp</th>
      <th>zero</th>
      <th>zero.1</th>
      <th>zero.2</th>
      <th>zero.3</th>
      <th>zero.4</th>
      <th>...</th>
      <th>zero.12</th>
      <th>zero.13</th>
      <th>zero.14</th>
      <th>Pclass</th>
      <th>zero.15</th>
      <th>zero.16</th>
      <th>Embarked</th>
      <th>zero.17</th>
      <th>zero.18</th>
      <th>2urvived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>22.0</td>
      <td>7.2500</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>38.0</td>
      <td>71.2833</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>26.0</td>
      <td>7.9250</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>35.0</td>
      <td>53.1000</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>35.0</td>
      <td>8.0500</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>



## 사용하는 컬럼만 가져오기 pd.read_csv(usecols=[ ])


```python
df = pd.read_csv("D:/anaconda/00.studying/titanic/train_and_test2.csv", usecols=[
  'Age', # 나이
  'Fare', # 승차 요금
  'Sex', # 성별
  'sibsp', # 타이타닉에 탑승한 형제자매, 배우자의 수
  'Parch', # 타이타니게 탑승한 부모, 자식의 수
  'Pclass', # 티켓 등급 (1, 2, 3등석)
  'Embarked', # 탑승국
  '2urvived' # 생존 여부 (0: 사망, 1: 생존)
])

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
      <th>Age</th>
      <th>Fare</th>
      <th>Sex</th>
      <th>sibsp</th>
      <th>Parch</th>
      <th>Pclass</th>
      <th>Embarked</th>
      <th>2urvived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>22.0</td>
      <td>7.2500</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>2.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>38.0</td>
      <td>71.2833</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>26.0</td>
      <td>7.9250</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>35.0</td>
      <td>53.1000</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>35.0</td>
      <td>8.0500</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2.0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



## 간단하게 데이터셋 미리보기 sns.countplot


```python
# 간단하게 데이터셋 미리보기
sns.countplot(x='Sex',hue='2urvived',data=df)
# 0남자 1여자 
```




    <AxesSubplot:xlabel='Sex', ylabel='count'>




    ![output_8_1](https://user-images.githubusercontent.com/88616282/202196434-55a995f5-9cbf-40c2-8afc-13d91e0522c2.png)




```python
sns.countplot(x=df['2urvived'])
# 사망이 천명 가까이 생존은 250명쯤 
```




    <AxesSubplot:xlabel='2urvived', ylabel='count'>




    
![output_9_1](https://user-images.githubusercontent.com/88616282/202196448-bb7b9f20-505b-46af-970d-22b5dd8271b5.png)



## 비어있는 행 확인 후 행 제거


```python
print(df.isnull().sum())
```

    Age         0
    Fare        0
    Sex         0
    sibsp       0
    Parch       0
    Pclass      0
    Embarked    2
    2urvived    0
    dtype: int64
    


```python
print(len(df))
df=df.dropna()
print(len(df))
# 두개가 삭제된것 확인 
```

    1309
    1307
    

## X Y 데이터 분할


```python
x_data = df.drop(columns=['2urvived'], axis=1)
x_data = x_data.astype(np.float32)

x_data.head(5)
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
      <th>Age</th>
      <th>Fare</th>
      <th>Sex</th>
      <th>sibsp</th>
      <th>Parch</th>
      <th>Pclass</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>22.0</td>
      <td>7.250000</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>38.0</td>
      <td>71.283302</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>26.0</td>
      <td>7.925000</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>35.0</td>
      <td>53.099998</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>35.0</td>
      <td>8.050000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
y_data = df[['2urvived']]
y_data = y_data.astype(np.float32)

y_data.head(5)
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
      <th>2urvived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



##  표준화
-지금 x데이터만 단위가 다르기때문에 x만하면됨 


```python
#정의하고
scaler = StandardScaler()
#호출 
x_data_scaled = scaler.fit_transform(x_data)
#표준화 전
print(x_data.values[0])
#표준화 후 
print(x_data_scaled[0])
```

    [22.    7.25  0.    1.    0.    3.    2.  ]
    [-0.58026063 -0.5018386  -0.74189967  0.48027176 -0.44540733  0.8404475
      0.6229398 ]
    

## 학습/검증 데이터 분할 
학습데이터 80 검증 데이터 20


```python
x_train, x_val, y_train, y_val = train_test_split(x_data, y_data, test_size=0.2, random_state=2021)

print(x_train.shape, x_val.shape)
print(y_train.shape, y_val.shape)
```

    (1045, 7) (262, 7)
    (1045, 1) (262, 1)
    

## 모델 학습

논리회귀(Logistic regression) ~sigmoid


```python
# sigmoid를 넣어줘야해
model = Sequential([
  Dense(1, activation='sigmoid')
])

#loss만 봐서는 잘 몰라서 metrics를 쓰게됨. 정확도를 0~1사이로 나타내줌
model.compile(loss='binary_crossentropy', optimizer=Adam(lr=0.01), metrics=['acc'])

#학습 
model.fit(
    x_train,
    y_train,
    validation_data=(x_val, y_val), # 검증 데이터를 넣어주면 한 epoch이 끝날때마다 자동으로 검증
    epochs=20 # epochs 복수형으로 쓰기!20번 반복학습
)

# val_acc 78%의 정확도를 갖는 생존여부를 예측하는 모델을 만듬 
```

    D:\anaconda\lib\site-packages\keras\optimizers\optimizer_v2\adam.py:114: UserWarning: The `lr` argument is deprecated, use `learning_rate` instead.
      super().__init__(name, **kwargs)
    

    Epoch 1/20
    33/33 [==============================] - 2s 10ms/step - loss: 3.5775 - acc: 0.7301 - val_loss: 0.8924 - val_acc: 0.7176
    Epoch 2/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.9229 - acc: 0.6813 - val_loss: 0.6815 - val_acc: 0.6756
    Epoch 3/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.6789 - acc: 0.7005 - val_loss: 0.5861 - val_acc: 0.7595
    Epoch 4/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.6083 - acc: 0.7397 - val_loss: 0.5392 - val_acc: 0.7748
    Epoch 5/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.5659 - acc: 0.7407 - val_loss: 0.5006 - val_acc: 0.7977
    Epoch 6/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.5450 - acc: 0.7368 - val_loss: 0.4766 - val_acc: 0.7939
    Epoch 7/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.5233 - acc: 0.7464 - val_loss: 0.4513 - val_acc: 0.7977
    Epoch 8/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.5080 - acc: 0.7560 - val_loss: 0.4529 - val_acc: 0.8053
    Epoch 9/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.5024 - acc: 0.7598 - val_loss: 0.4435 - val_acc: 0.8015
    Epoch 10/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.4930 - acc: 0.7589 - val_loss: 0.4541 - val_acc: 0.7939
    Epoch 11/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.5073 - acc: 0.7656 - val_loss: 0.4668 - val_acc: 0.7863
    Epoch 12/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.4886 - acc: 0.7636 - val_loss: 0.4544 - val_acc: 0.7901
    Epoch 13/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.5009 - acc: 0.7617 - val_loss: 0.4396 - val_acc: 0.7748
    Epoch 14/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.4949 - acc: 0.7617 - val_loss: 0.4339 - val_acc: 0.7786
    Epoch 15/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.4858 - acc: 0.7703 - val_loss: 0.4820 - val_acc: 0.7748
    Epoch 16/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.4966 - acc: 0.7770 - val_loss: 0.4720 - val_acc: 0.7710
    Epoch 17/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.4872 - acc: 0.7789 - val_loss: 0.4376 - val_acc: 0.8015
    Epoch 18/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.5061 - acc: 0.7550 - val_loss: 0.4412 - val_acc: 0.8168
    Epoch 19/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.4865 - acc: 0.7742 - val_loss: 0.4857 - val_acc: 0.7824
    Epoch 20/20
    33/33 [==============================] - 0s 2ms/step - loss: 0.4838 - acc: 0.7799 - val_loss: 0.4367 - val_acc: 0.7863
    




    <keras.callbacks.History at 0x227501f0be0>




```python

```
