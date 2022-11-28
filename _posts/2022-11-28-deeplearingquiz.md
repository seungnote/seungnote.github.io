---
title:  "[Python] 머신러닝_딥러닝QUIZ" 

categories:
  - quiz
tags:
  - [Python,ADP,machine_learning,quiz]

toc: true
toc_sticky: true

date: 2022-11-28

---

# 손글씨 예측하는 머신러닝 만들기(0~9)

!kaggle datasets download -d oddrationale/mnist-in-csv

https://www.notion.so/3-9481644387f549cd9f350cba4131448b

답안지: https://colab.research.google.com/drive/1nwKvv72D5_v8x7zdGF-9JPCmBfKot-Zu?usp=sharing



## 캐글 key 가져오기


```python
import os
os.environ['KAGGLE_USERNAME'] = 'seungnote' 
os.environ['KAGGLE_KEY'] = 'bc254ae94554f39d41fcab91537514ad' 
```


```python
!kaggle datasets download -d oddrationale/mnist-in-csv
```

    Downloading mnist-in-csv.zip to D:\anaconda\00.studying
    
    

    
      0%|          | 0.00/15.2M [00:00<?, ?B/s]
      7%|6         | 1.00M/15.2M [00:00<00:01, 10.0MB/s]
     20%|#9        | 3.00M/15.2M [00:00<00:01, 11.1MB/s]
     33%|###2      | 5.00M/15.2M [00:00<00:01, 9.92MB/s]
     46%|####5     | 7.00M/15.2M [00:00<00:00, 10.6MB/s]
     59%|#####9    | 9.00M/15.2M [00:00<00:00, 10.9MB/s]
     72%|#######2  | 11.0M/15.2M [00:01<00:00, 11.1MB/s]
     85%|########5 | 13.0M/15.2M [00:01<00:00, 11.2MB/s]
     98%|#########8| 15.0M/15.2M [00:01<00:00, 10.2MB/s]
    100%|##########| 15.2M/15.2M [00:01<00:00, 10.6MB/s]
    

## 사용할 lib import하기


```python
from tensorflow.keras.models import Model
from tensorflow.keras.layers import Input, Dense
from tensorflow.keras.optimizers import Adam, SGD
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.preprocessing import OneHotEncoder
```

## 자료 체크


```python
dtrain=pd.read_csv("D:/anaconda/00.studying/mnist-in-csv/mnist_train.csv")

dtrain.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 60000 entries, 0 to 59999
    Columns: 785 entries, label to 28x28
    dtypes: int64(785)
    memory usage: 359.3 MB
    


```python
dtrain.head(2)
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
      <th>label</th>
      <th>1x1</th>
      <th>1x2</th>
      <th>1x3</th>
      <th>1x4</th>
      <th>1x5</th>
      <th>1x6</th>
      <th>1x7</th>
      <th>1x8</th>
      <th>1x9</th>
      <th>...</th>
      <th>28x19</th>
      <th>28x20</th>
      <th>28x21</th>
      <th>28x22</th>
      <th>28x23</th>
      <th>28x24</th>
      <th>28x25</th>
      <th>28x26</th>
      <th>28x27</th>
      <th>28x28</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 785 columns</p>
</div>




```python
dtest=pd.read_csv("D:/anaconda/00.studying/mnist-in-csv/mnist_test.csv")

dtest.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 10000 entries, 0 to 9999
    Columns: 785 entries, label to 28x28
    dtypes: int64(785)
    memory usage: 59.9 MB
    


```python
dtest.head(2)
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
      <th>label</th>
      <th>1x1</th>
      <th>1x2</th>
      <th>1x3</th>
      <th>1x4</th>
      <th>1x5</th>
      <th>1x6</th>
      <th>1x7</th>
      <th>1x8</th>
      <th>1x9</th>
      <th>...</th>
      <th>28x19</th>
      <th>28x20</th>
      <th>28x21</th>
      <th>28x22</th>
      <th>28x23</th>
      <th>28x24</th>
      <th>28x25</th>
      <th>28x26</th>
      <th>28x27</th>
      <th>28x28</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>0</td>
      <td>0</td>
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
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0</td>
      <td>0</td>
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
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 785 columns</p>
</div>



## 라벨 분포보기


```python
plt.figure(figsize=(16,10))
sns.countplot(dtrain['label'])
plt.show()
```

    D:\anaconda\lib\site-packages\seaborn\_decorators.py:36: FutureWarning: Pass the following variable as a keyword arg: x. From version 0.12, the only valid positional argument will be `data`, and passing other arguments without an explicit keyword will result in an error or misinterpretation.
      warnings.warn(
    


![output_12_1](https://user-images.githubusercontent.com/88616282/204263053-21c4183b-9da9-4bf4-9538-7cdba41b0932.png)



## 데이터전처리(입력 출력 나누기)

**axis=0 위/행

**axis=1 옆/열 



```python
dtrain=dtrain.astype(np.float32)
x_train=dtrain.drop(columns=['label'],axis=1).values
y_train=dtrain[['label']].values

dtest = dtest.astype(np.float32)
x_test = dtest.drop(columns=['label'], axis=1).values
y_test = dtest[['label']].values

print(x_train.shape, y_train.shape)
print(x_test.shape, y_test.shape)
```

    (60000, 784) (60000, 1)
    (10000, 784) (10000, 1)
    

## 데이터 미리보기


```python
index=1
plt.title(str(y_train[index]))
plt.imshow(x_train[index].reshape((28,28)),cmap='gray')
plt.show()
```


    
    
![output_16_0](https://user-images.githubusercontent.com/88616282/204263139-3a6cd3c2-17a5-44ba-9709-c2cc194c3926.png)

## One-hot encoding(2차원 만들기)-> 진행생략


```python
encoder=OneHotEncoder()
y_train=encoder.fit_transform(y_train).toarray()
y_test=encoder.fit_transform(y_test).toarray()

print(y_train.shape)
```

    (60000, 10)
    


```python
index=1
plt.title(str(y_train[index]))
plt.imshow(x_train[index].reshape((28,28)),cmap='gray')
plt.show()
```


![output_19_0](https://user-images.githubusercontent.com/88616282/204263115-ac64ee7d-671c-4fb8-af02-60eef8ea15e6.png)

    


## 일반화 -> 진행생략

0~1까지의 소숫점으로 만들어 보림 


```python
x_train = x_train / 255.
x_test = x_test / 255.
```

## 네트워크 구성(입력층/은닉층/출력층)

(60000, 784) (60000, 1)
(10000, 784) (10000, 1)

기존: model.compile(loss='categorical_crossentropy', optimizer=Adam(lr=0.001), metrics=['acc'])

변경: model.compile(loss='sparse_categorical_crossentropy', optimizer=Adam(lr=0.001), metrics=['acc'])




```python
input = Input(shape=(784,))

# 노드 갯수 1024, 512 
hidden = Dense(1024, activation='relu')(input)
hidden = Dense(512, activation='relu')(hidden)
hidden = Dense(256, activation='relu')(hidden)
output = Dense(24, activation='softmax')(hidden)

model = Model(inputs=input, outputs=output)

#acc 정확도를 0~1사이로 표현
model.compile(loss='sparse_categorical_crossentropy', optimizer=Adam(lr=0.001), metrics=['acc'])

model.summary()
```

    Model: "model"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     input_1 (InputLayer)        [(None, 784)]             0         
                                                                     
     dense (Dense)               (None, 1024)              803840    
                                                                     
     dense_1 (Dense)             (None, 512)               524800    
                                                                     
     dense_2 (Dense)             (None, 256)               131328    
                                                                     
     dense_3 (Dense)             (None, 24)                6168      
                                                                     
    =================================================================
    Total params: 1,466,136
    Trainable params: 1,466,136
    Non-trainable params: 0
    _________________________________________________________________
    

    D:\anaconda\lib\site-packages\keras\optimizers\optimizer_v2\adam.py:114: UserWarning: The `lr` argument is deprecated, use `learning_rate` instead.
      super().__init__(name, **kwargs)
    

## 학습


```python
history = model.fit(
    x_train,
    y_train,
    validation_data=(x_test, y_test), # 검증 데이터를 넣어주면 한 epoch이 끝날때마다 자동으로 검증
    epochs=20 # epochs 복수형으로 쓰기!
)
```

    Epoch 1/20
    1875/1875 [==============================] - 20s 10ms/step - loss: 1.0101 - acc: 0.9115 - val_loss: 0.2656 - val_acc: 0.9375
    Epoch 2/20
    1875/1875 [==============================] - 18s 10ms/step - loss: 0.1871 - acc: 0.9498 - val_loss: 0.2230 - val_acc: 0.9409
    Epoch 3/20
    1875/1875 [==============================] - 19s 10ms/step - loss: 0.1466 - acc: 0.9594 - val_loss: 0.1675 - val_acc: 0.9537
    Epoch 4/20
    1875/1875 [==============================] - 19s 10ms/step - loss: 0.1232 - acc: 0.9661 - val_loss: 0.1902 - val_acc: 0.9521
    Epoch 5/20
    1875/1875 [==============================] - 19s 10ms/step - loss: 0.1125 - acc: 0.9693 - val_loss: 0.1237 - val_acc: 0.9661
    Epoch 6/20
    1875/1875 [==============================] - 18s 9ms/step - loss: 0.0944 - acc: 0.9753 - val_loss: 0.1211 - val_acc: 0.9691
    Epoch 7/20
    1875/1875 [==============================] - 17s 9ms/step - loss: 0.0841 - acc: 0.9779 - val_loss: 0.1176 - val_acc: 0.9720
    Epoch 8/20
    1875/1875 [==============================] - 18s 9ms/step - loss: 0.0800 - acc: 0.9792 - val_loss: 0.1306 - val_acc: 0.9747
    Epoch 9/20
    1875/1875 [==============================] - 19s 10ms/step - loss: 0.0741 - acc: 0.9827 - val_loss: 0.1392 - val_acc: 0.9700
    Epoch 10/20
    1875/1875 [==============================] - 20s 11ms/step - loss: 0.0645 - acc: 0.9847 - val_loss: 0.1238 - val_acc: 0.9727
    Epoch 11/20
    1875/1875 [==============================] - 19s 10ms/step - loss: 0.0718 - acc: 0.9840 - val_loss: 0.1289 - val_acc: 0.9722
    Epoch 12/20
    1875/1875 [==============================] - 20s 10ms/step - loss: 0.0608 - acc: 0.9858 - val_loss: 0.1552 - val_acc: 0.9751
    Epoch 13/20
    1875/1875 [==============================] - 19s 10ms/step - loss: 0.0550 - acc: 0.9883 - val_loss: 0.1532 - val_acc: 0.9738
    Epoch 14/20
    1875/1875 [==============================] - 20s 10ms/step - loss: 0.0595 - acc: 0.9881 - val_loss: 0.1713 - val_acc: 0.9751
    Epoch 15/20
    1875/1875 [==============================] - 18s 10ms/step - loss: 0.0555 - acc: 0.9885 - val_loss: 0.1493 - val_acc: 0.9758
    Epoch 16/20
    1875/1875 [==============================] - 18s 10ms/step - loss: 0.0476 - acc: 0.9895 - val_loss: 0.1764 - val_acc: 0.9766
    Epoch 17/20
    1875/1875 [==============================] - 18s 10ms/step - loss: 0.0421 - acc: 0.9909 - val_loss: 0.1507 - val_acc: 0.9766
    Epoch 18/20
    1875/1875 [==============================] - 17s 9ms/step - loss: 0.0528 - acc: 0.9901 - val_loss: 0.1812 - val_acc: 0.9752
    Epoch 19/20
    1875/1875 [==============================] - 16s 9ms/step - loss: 0.0544 - acc: 0.9899 - val_loss: 0.1327 - val_acc: 0.9773
    Epoch 20/20
    1875/1875 [==============================] - 16s 9ms/step - loss: 0.0392 - acc: 0.9922 - val_loss: 0.1588 - val_acc: 0.9751
    

## 학습결과 그래프


```python
plt.figure(figsize=(16, 10))
plt.plot(history.history['loss'])
plt.plot(history.history['val_loss'])
```




    [<matplotlib.lines.Line2D at 0x23e6797b3a0>]




![output_27_1](https://user-images.githubusercontent.com/88616282/204263183-8af8e60c-4e5a-42e5-9290-c421a0401a60.png)

    



```python
plt.figure(figsize=(16, 10))
plt.plot(history.history['acc'])
plt.plot(history.history['val_acc'])
```




    [<matplotlib.lines.Line2D at 0x23e679e0880>]




    
![output_28_1](https://user-images.githubusercontent.com/88616282/204263206-036b5f9a-4179-4c17-90e7-259b6e5f57e1.png)

