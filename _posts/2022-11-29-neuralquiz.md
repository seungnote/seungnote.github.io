```python
import os
os.environ['KAGGLE_USERNAME'] = 'seungnote' 
os.environ['KAGGLE_KEY'] = 'bc254ae94554f39d41fcab91537514ad' 
```


```python
!kaggle datasets download -d datamunge/sign-language-mnist
```

    Downloading sign-language-mnist.zip to D:\anaconda\00.studying
    
    

    
      0%|          | 0.00/62.6M [00:00<?, ?B/s]
      3%|3         | 2.00M/62.6M [00:00<00:05, 11.0MB/s]
      6%|6         | 4.00M/62.6M [00:00<00:05, 11.4MB/s]
     10%|9         | 6.00M/62.6M [00:00<00:05, 10.3MB/s]
     13%|#2        | 8.00M/62.6M [00:00<00:05, 10.9MB/s]
     16%|#5        | 10.0M/62.6M [00:00<00:05, 11.0MB/s]
     19%|#9        | 12.0M/62.6M [00:01<00:04, 11.2MB/s]
     22%|##2       | 14.0M/62.6M [00:01<00:04, 11.3MB/s]
     26%|##5       | 16.0M/62.6M [00:01<00:04, 11.4MB/s]
     29%|##8       | 18.0M/62.6M [00:01<00:04, 11.5MB/s]
     32%|###1      | 20.0M/62.6M [00:01<00:03, 11.3MB/s]
     35%|###5      | 22.0M/62.6M [00:02<00:03, 11.2MB/s]
     38%|###8      | 24.0M/62.6M [00:02<00:03, 11.3MB/s]
     42%|####1     | 26.0M/62.6M [00:02<00:03, 11.3MB/s]
     45%|####4     | 28.0M/62.6M [00:02<00:03, 11.3MB/s]
     48%|####7     | 30.0M/62.6M [00:02<00:03, 11.2MB/s]
     51%|#####1    | 32.0M/62.6M [00:02<00:02, 11.3MB/s]
     54%|#####4    | 34.0M/62.6M [00:03<00:02, 11.4MB/s]
     58%|#####7    | 36.0M/62.6M [00:03<00:02, 11.5MB/s]
     61%|######    | 38.0M/62.6M [00:03<00:02, 11.5MB/s]
     64%|######3   | 40.0M/62.6M [00:03<00:02, 11.5MB/s]
     67%|######7   | 42.0M/62.6M [00:03<00:01, 11.6MB/s]
     70%|#######   | 44.0M/62.6M [00:04<00:01, 11.5MB/s]
     73%|#######3  | 46.0M/62.6M [00:04<00:01, 11.5MB/s]
     77%|#######6  | 48.0M/62.6M [00:04<00:01, 11.5MB/s]
     80%|#######9  | 50.0M/62.6M [00:04<00:01, 11.5MB/s]
     83%|########3 | 52.0M/62.6M [00:04<00:00, 11.5MB/s]
     86%|########6 | 54.0M/62.6M [00:04<00:00, 11.5MB/s]
     89%|########9 | 56.0M/62.6M [00:05<00:00, 9.39MB/s]
     93%|#########2| 58.0M/62.6M [00:05<00:00, 9.95MB/s]
     96%|#########5| 60.0M/62.6M [00:05<00:00, 10.4MB/s]
     99%|#########9| 62.0M/62.6M [00:05<00:00, 10.6MB/s]
    100%|##########| 62.6M/62.6M [00:05<00:00, 11.1MB/s]
    


```python
from tensorflow.keras.models import Model
from tensorflow.keras.layers import Input, Dense, Conv2D, MaxPooling2D, Flatten, Dropout
from tensorflow.keras.optimizers import Adam, SGD
from tensorflow.keras.preprocessing.image import ImageDataGenerator
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.preprocessing import OneHotEncoder
```


```python
train_df = pd.read_csv('D:/anaconda/00.studying/sign-language-mnist/sign_mnist_train/sign_mnist_train.csv')
test_df = pd.read_csv('D:/anaconda/00.studying/sign-language-mnist/sign_mnist_test/sign_mnist_test.csv')
train_df.head()
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
      <th>pixel1</th>
      <th>pixel2</th>
      <th>pixel3</th>
      <th>pixel4</th>
      <th>pixel5</th>
      <th>pixel6</th>
      <th>pixel7</th>
      <th>pixel8</th>
      <th>pixel9</th>
      <th>...</th>
      <th>pixel775</th>
      <th>pixel776</th>
      <th>pixel777</th>
      <th>pixel778</th>
      <th>pixel779</th>
      <th>pixel780</th>
      <th>pixel781</th>
      <th>pixel782</th>
      <th>pixel783</th>
      <th>pixel784</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
      <td>107</td>
      <td>118</td>
      <td>127</td>
      <td>134</td>
      <td>139</td>
      <td>143</td>
      <td>146</td>
      <td>150</td>
      <td>153</td>
      <td>...</td>
      <td>207</td>
      <td>207</td>
      <td>207</td>
      <td>207</td>
      <td>206</td>
      <td>206</td>
      <td>206</td>
      <td>204</td>
      <td>203</td>
      <td>202</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>155</td>
      <td>157</td>
      <td>156</td>
      <td>156</td>
      <td>156</td>
      <td>157</td>
      <td>156</td>
      <td>158</td>
      <td>158</td>
      <td>...</td>
      <td>69</td>
      <td>149</td>
      <td>128</td>
      <td>87</td>
      <td>94</td>
      <td>163</td>
      <td>175</td>
      <td>103</td>
      <td>135</td>
      <td>149</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>187</td>
      <td>188</td>
      <td>188</td>
      <td>187</td>
      <td>187</td>
      <td>186</td>
      <td>187</td>
      <td>188</td>
      <td>187</td>
      <td>...</td>
      <td>202</td>
      <td>201</td>
      <td>200</td>
      <td>199</td>
      <td>198</td>
      <td>199</td>
      <td>198</td>
      <td>195</td>
      <td>194</td>
      <td>195</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>211</td>
      <td>211</td>
      <td>212</td>
      <td>212</td>
      <td>211</td>
      <td>210</td>
      <td>211</td>
      <td>210</td>
      <td>210</td>
      <td>...</td>
      <td>235</td>
      <td>234</td>
      <td>233</td>
      <td>231</td>
      <td>230</td>
      <td>226</td>
      <td>225</td>
      <td>222</td>
      <td>229</td>
      <td>163</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13</td>
      <td>164</td>
      <td>167</td>
      <td>170</td>
      <td>172</td>
      <td>176</td>
      <td>179</td>
      <td>180</td>
      <td>184</td>
      <td>185</td>
      <td>...</td>
      <td>92</td>
      <td>105</td>
      <td>105</td>
      <td>108</td>
      <td>133</td>
      <td>163</td>
      <td>157</td>
      <td>163</td>
      <td>164</td>
      <td>179</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 785 columns</p>
</div>



## 라벨 분포 


```python
plt.figure(figsize=(16, 10))
sns.countplot(train_df['label'])
plt.show()
```

    D:\anaconda\lib\site-packages\seaborn\_decorators.py:36: FutureWarning: Pass the following variable as a keyword arg: x. From version 0.12, the only valid positional argument will be `data`, and passing other arguments without an explicit keyword will result in an error or misinterpretation.
      warnings.warn(
    


    
![png](output_5_1.png)
    


reshape부분이 달라짐 

왜? **x_train = x_train.reshape((-1, 28, 28, 1)) 

3차원으로 만들어주는거. 데이터셋 크기 -1 이미지 크기 28 그레이스케일 이미지 1**

//
dtrain=dtrain.astype(np.float32)
x_train=dtrain.drop(columns=['label'],axis=1).values
y_train=dtrain[['label']].values

dtest = dtest.astype(np.float32)
x_test = dtest.drop(columns=['label'], axis=1).values
y_test = dtest[['label']].values

print(x_train.shape, y_train.shape)
print(x_test.shape, y_test.shape)
//

## 전처리


```python
train_df = train_df.astype(np.float32)
x_train = train_df.drop(columns=['label'], axis=1).values
x_train = x_train.reshape((-1, 28, 28, 1))
y_train = train_df[['label']].values

test_df = test_df.astype(np.float32)
x_test = test_df.drop(columns=['label'], axis=1).values
x_test = x_test.reshape((-1, 28, 28, 1))
y_test = test_df[['label']].values

```


```python
print(x_train.shape, y_train.shape)
print(x_test.shape, y_test.shape)
```

    (27455, 28, 28, 1) (27455, 1)
    (7172, 28, 28, 1) (7172, 1)
    

## 데이터 미리보기 


```python
index=1
plt.title(str(y_train[index]))
plt.imshow(x_train[index].reshape((28,28)),cmap='gray')
plt.show()
```


    
![png](output_11_0.png)
    


## One-hot encoding


```python
encoder=OneHotEncoder()
y_train=encoder.fit_transform(y_train).toarray()
y_test=encoder.fit_transform(y_test).toarray()

print(y_train.shape)
```

    (27455, 24)
    

## 일반화 


```python
train_image_datagen = ImageDataGenerator(
  rescale=1./255, # 일반화
)

# 256개씩 작게 학습시킨다는거. shuffle 이미지 마구 섞어줌(랜덤성) 성능향상 도움줌 
train_datagen = train_image_datagen.flow(
    x=x_train,
    y=y_train,
    batch_size=256,
    shuffle=True
)

test_image_datagen = ImageDataGenerator(
  rescale=1./255
)

test_datagen = test_image_datagen.flow(
    x=x_test,
    y=y_test,
    batch_size=256,
    shuffle=False
)


index = 1

preview_img = train_datagen.__getitem__(0)[0][index]
preview_label = train_datagen.__getitem__(0)[1][index]

plt.imshow(preview_img.reshape((28, 28)))
plt.title(str(preview_label))
plt.show()

## 실행할때마다 다른 이미지가 나옴 
```


    
![png](output_15_0.png)
    


## 네트워크 구성 

필터 갯수 32개 커널 3, 스트라이드 1씩 움직임. padding=same은 인풋과 아웃풋이 동일 


```python
input = Input(shape=(28, 28, 1))

# 필터 갯수가 달라짐 
hidden = Conv2D(filters=32, kernel_size=3, strides=1, padding='same', activation='relu')(input)
hidden = MaxPooling2D(pool_size=2, strides=2)(hidden)

hidden = Conv2D(filters=64, kernel_size=3, strides=1, padding='same', activation='relu')(hidden)
hidden = MaxPooling2D(pool_size=2, strides=2)(hidden)

hidden = Conv2D(filters=32, kernel_size=3, strides=1, padding='same', activation='relu')(hidden)
hidden = MaxPooling2D(pool_size=2, strides=2)(hidden)

# 다시 1차원으로 만들어줘 

hidden = Flatten()(hidden)

hidden = Dense(512, activation='relu')(hidden)

# 30%의 노드를 랜덤으로 탈락시켜준다 
hidden = Dropout(rate=0.3)(hidden)

output = Dense(24, activation='softmax')(hidden)

model = Model(inputs=input, outputs=output)

model.compile(loss='categorical_crossentropy', optimizer=Adam(lr=0.001), metrics=['acc'])

model.summary()
```

    Model: "model"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     input_1 (InputLayer)        [(None, 28, 28, 1)]       0         
                                                                     
     conv2d (Conv2D)             (None, 28, 28, 32)        320       
                                                                     
     max_pooling2d (MaxPooling2D  (None, 14, 14, 32)       0         
     )                                                               
                                                                     
     conv2d_1 (Conv2D)           (None, 14, 14, 64)        18496     
                                                                     
     max_pooling2d_1 (MaxPooling  (None, 7, 7, 64)         0         
     2D)                                                             
                                                                     
     conv2d_2 (Conv2D)           (None, 7, 7, 32)          18464     
                                                                     
     max_pooling2d_2 (MaxPooling  (None, 3, 3, 32)         0         
     2D)                                                             
                                                                     
     flatten (Flatten)           (None, 288)               0         
                                                                     
     dense (Dense)               (None, 512)               147968    
                                                                     
     dropout (Dropout)           (None, 512)               0         
                                                                     
     dense_1 (Dense)             (None, 24)                12312     
                                                                     
    =================================================================
    Total params: 197,560
    Trainable params: 197,560
    Non-trainable params: 0
    _________________________________________________________________
    

    D:\anaconda\lib\site-packages\keras\optimizers\optimizer_v2\adam.py:114: UserWarning: The `lr` argument is deprecated, use `learning_rate` instead.
      super().__init__(name, **kwargs)
    

## 학습 


```python
history = model.fit(
    train_datagen,
    validation_data=test_datagen, # 검증 데이터를 넣어주면 한 epoch이 끝날때마다 자동으로 검증
    epochs=20 # epochs 복수형으로 쓰기!
)
```

    Epoch 1/20
    108/108 [==============================] - 18s 148ms/step - loss: 2.2054 - acc: 0.3378 - val_loss: 1.1366 - val_acc: 0.6647
    Epoch 2/20
    108/108 [==============================] - 15s 135ms/step - loss: 0.6092 - acc: 0.7972 - val_loss: 0.5285 - val_acc: 0.8277
    Epoch 3/20
    108/108 [==============================] - 14s 132ms/step - loss: 0.2212 - acc: 0.9315 - val_loss: 0.3618 - val_acc: 0.8939
    Epoch 4/20
    108/108 [==============================] - 13s 122ms/step - loss: 0.0965 - acc: 0.9739 - val_loss: 0.2702 - val_acc: 0.9162
    Epoch 5/20
    108/108 [==============================] - 13s 121ms/step - loss: 0.0501 - acc: 0.9880 - val_loss: 0.2553 - val_acc: 0.9269
    Epoch 6/20
    108/108 [==============================] - 14s 125ms/step - loss: 0.0249 - acc: 0.9951 - val_loss: 0.2759 - val_acc: 0.9257
    Epoch 7/20
    108/108 [==============================] - 14s 130ms/step - loss: 0.0204 - acc: 0.9955 - val_loss: 0.2625 - val_acc: 0.9340
    Epoch 8/20
    108/108 [==============================] - 15s 135ms/step - loss: 0.0137 - acc: 0.9976 - val_loss: 0.2482 - val_acc: 0.9393
    Epoch 9/20
    108/108 [==============================] - 16s 147ms/step - loss: 0.0091 - acc: 0.9985 - val_loss: 0.2721 - val_acc: 0.9368
    Epoch 10/20
    108/108 [==============================] - 14s 126ms/step - loss: 0.0076 - acc: 0.9985 - val_loss: 0.2466 - val_acc: 0.9451
    Epoch 11/20
    108/108 [==============================] - 15s 138ms/step - loss: 0.0086 - acc: 0.9982 - val_loss: 0.2417 - val_acc: 0.9491
    Epoch 12/20
    108/108 [==============================] - 16s 144ms/step - loss: 0.0058 - acc: 0.9991 - val_loss: 0.2411 - val_acc: 0.9492
    Epoch 13/20
    108/108 [==============================] - 14s 128ms/step - loss: 0.0045 - acc: 0.9992 - val_loss: 0.2416 - val_acc: 0.9532
    Epoch 14/20
    108/108 [==============================] - 14s 128ms/step - loss: 0.0032 - acc: 0.9994 - val_loss: 0.2473 - val_acc: 0.9437
    Epoch 15/20
    108/108 [==============================] - 14s 127ms/step - loss: 0.0032 - acc: 0.9995 - val_loss: 0.2708 - val_acc: 0.9460
    Epoch 16/20
    108/108 [==============================] - 14s 127ms/step - loss: 0.0052 - acc: 0.9988 - val_loss: 0.2656 - val_acc: 0.9481
    Epoch 17/20
    108/108 [==============================] - 14s 130ms/step - loss: 0.0032 - acc: 0.9994 - val_loss: 0.2509 - val_acc: 0.9495
    Epoch 18/20
    108/108 [==============================] - 16s 145ms/step - loss: 0.0065 - acc: 0.9980 - val_loss: 0.2777 - val_acc: 0.9396
    Epoch 19/20
    108/108 [==============================] - 16s 151ms/step - loss: 0.0057 - acc: 0.9985 - val_loss: 0.2523 - val_acc: 0.9555
    Epoch 20/20
    108/108 [==============================] - 17s 158ms/step - loss: 0.0055 - acc: 0.9986 - val_loss: 0.2766 - val_acc: 0.9361
    

## 학습 결과 그래프


```python
fig, axes = plt.subplots(1, 2, figsize=(20, 6))
axes[0].plot(history.history['loss'])
axes[0].plot(history.history['val_loss'])
axes[1].plot(history.history['acc'])
axes[1].plot(history.history['val_acc'])
```




    [<matplotlib.lines.Line2D at 0x2a205fb0d30>]




    
![png](output_21_1.png)
    


# 이미지 증강 기법
## 학습데이터 증강하기 


```python
train_image_datagen = ImageDataGenerator(
  rescale=1./255, # 일반화
  rotation_range=10,  # 랜덤하게 이미지를 회전 (단위: 도, 0-180)
  zoom_range=0.1, # 랜덤하게 이미지 확대 (%)
  width_shift_range=0.1,  # 랜덤하게 이미지를 수평으로 이동 (%)
  height_shift_range=0.1,  # 랜덤하게 이미지를 수직으로 이동 (%)
)

train_datagen = train_image_datagen.flow(
    x=x_train,
    y=y_train,
    batch_size=256,
    shuffle=True
)
```

## 검증데이터 일반화하기 


```python
test_image_datagen = ImageDataGenerator(
  rescale=1./255
)

test_datagen = test_image_datagen.flow(
    x=x_test,
    y=y_test,
    batch_size=256,
    shuffle=False
)
```

## 이미지 확인하기


```python
index = 1

preview_img = train_datagen.__getitem__(0)[0][index]
preview_label = train_datagen.__getitem__(0)[1][index]

plt.imshow(preview_img.reshape((28, 28)))
plt.title(str(preview_label))
plt.show()
```


    
![png](output_27_0.png)
    


## 네트워크 구성하기


```python
input = Input(shape=(28, 28, 1))

hidden = Conv2D(filters=32, kernel_size=3, strides=1, padding='same', activation='relu')(input)
hidden = MaxPooling2D(pool_size=2, strides=2)(hidden)

hidden = Conv2D(filters=64, kernel_size=3, strides=1, padding='same', activation='relu')(hidden)
hidden = MaxPooling2D(pool_size=2, strides=2)(hidden)

hidden = Conv2D(filters=32, kernel_size=3, strides=1, padding='same', activation='relu')(hidden)
hidden = MaxPooling2D(pool_size=2, strides=2)(hidden)

hidden = Flatten()(hidden)

hidden = Dense(512, activation='relu')(hidden)

hidden = Dropout(rate=0.3)(hidden)

output = Dense(24, activation='softmax')(hidden)

model = Model(inputs=input, outputs=output)

model.compile(loss='categorical_crossentropy', optimizer=Adam(lr=0.001), metrics=['acc'])

model.summary()
```

    Model: "model_1"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     input_2 (InputLayer)        [(None, 28, 28, 1)]       0         
                                                                     
     conv2d_3 (Conv2D)           (None, 28, 28, 32)        320       
                                                                     
     max_pooling2d_3 (MaxPooling  (None, 14, 14, 32)       0         
     2D)                                                             
                                                                     
     conv2d_4 (Conv2D)           (None, 14, 14, 64)        18496     
                                                                     
     max_pooling2d_4 (MaxPooling  (None, 7, 7, 64)         0         
     2D)                                                             
                                                                     
     conv2d_5 (Conv2D)           (None, 7, 7, 32)          18464     
                                                                     
     max_pooling2d_5 (MaxPooling  (None, 3, 3, 32)         0         
     2D)                                                             
                                                                     
     flatten_1 (Flatten)         (None, 288)               0         
                                                                     
     dense_2 (Dense)             (None, 512)               147968    
                                                                     
     dropout_1 (Dropout)         (None, 512)               0         
                                                                     
     dense_3 (Dense)             (None, 24)                12312     
                                                                     
    =================================================================
    Total params: 197,560
    Trainable params: 197,560
    Non-trainable params: 0
    _________________________________________________________________
    

## 모델 학습시키기


```python
history = model.fit(
    train_datagen,
    validation_data=test_datagen, # 검증 데이터를 넣어주면 한 epoch이 끝날때마다 자동으로 검증
    epochs=20 # epochs 복수형으로 쓰기!
)
```

    Epoch 1/20
    108/108 [==============================] - 20s 175ms/step - loss: 2.4638 - acc: 0.2536 - val_loss: 1.1797 - val_acc: 0.6383
    Epoch 2/20
    108/108 [==============================] - 18s 168ms/step - loss: 1.0798 - acc: 0.6453 - val_loss: 0.5753 - val_acc: 0.8091
    Epoch 3/20
    108/108 [==============================] - 18s 162ms/step - loss: 0.6384 - acc: 0.7878 - val_loss: 0.2789 - val_acc: 0.9179
    Epoch 4/20
    108/108 [==============================] - 18s 168ms/step - loss: 0.4642 - acc: 0.8457 - val_loss: 0.2382 - val_acc: 0.9233
    Epoch 5/20
    108/108 [==============================] - 19s 175ms/step - loss: 0.3437 - acc: 0.8859 - val_loss: 0.1614 - val_acc: 0.9442
    Epoch 6/20
    108/108 [==============================] - 19s 173ms/step - loss: 0.2686 - acc: 0.9131 - val_loss: 0.1105 - val_acc: 0.9671
    Epoch 7/20
    108/108 [==============================] - 20s 182ms/step - loss: 0.2266 - acc: 0.9256 - val_loss: 0.0839 - val_acc: 0.9778
    Epoch 8/20
    108/108 [==============================] - 19s 179ms/step - loss: 0.1793 - acc: 0.9441 - val_loss: 0.0835 - val_acc: 0.9766
    Epoch 9/20
    108/108 [==============================] - 19s 173ms/step - loss: 0.1561 - acc: 0.9482 - val_loss: 0.0499 - val_acc: 0.9872
    Epoch 10/20
    108/108 [==============================] - 17s 156ms/step - loss: 0.1304 - acc: 0.9584 - val_loss: 0.0447 - val_acc: 0.9847
    Epoch 11/20
    108/108 [==============================] - 17s 155ms/step - loss: 0.1155 - acc: 0.9617 - val_loss: 0.0512 - val_acc: 0.9834
    Epoch 12/20
    108/108 [==============================] - 18s 167ms/step - loss: 0.1087 - acc: 0.9647 - val_loss: 0.0466 - val_acc: 0.9828
    Epoch 13/20
    108/108 [==============================] - 19s 175ms/step - loss: 0.0928 - acc: 0.9696 - val_loss: 0.0330 - val_acc: 0.9915
    Epoch 14/20
    108/108 [==============================] - 20s 190ms/step - loss: 0.0802 - acc: 0.9742 - val_loss: 0.0280 - val_acc: 0.9915
    Epoch 15/20
    108/108 [==============================] - 20s 189ms/step - loss: 0.0727 - acc: 0.9765 - val_loss: 0.0248 - val_acc: 0.9915
    Epoch 16/20
    108/108 [==============================] - 18s 162ms/step - loss: 0.0686 - acc: 0.9773 - val_loss: 0.0121 - val_acc: 0.9972
    Epoch 17/20
    108/108 [==============================] - 19s 175ms/step - loss: 0.0590 - acc: 0.9815 - val_loss: 0.0208 - val_acc: 0.9953
    Epoch 18/20
    108/108 [==============================] - 17s 160ms/step - loss: 0.0612 - acc: 0.9813 - val_loss: 0.0149 - val_acc: 0.9934
    Epoch 19/20
    108/108 [==============================] - 16s 146ms/step - loss: 0.0475 - acc: 0.9852 - val_loss: 0.0179 - val_acc: 0.9927
    Epoch 20/20
    108/108 [==============================] - 16s 145ms/step - loss: 0.0481 - acc: 0.9840 - val_loss: 0.0255 - val_acc: 0.9911
    


```python
fig, axes = plt.subplots(1, 2, figsize=(20, 6))
axes[0].plot(history.history['loss'])
axes[0].plot(history.history['val_loss'])
axes[1].plot(history.history['acc'])
axes[1].plot(history.history['val_acc'])
```




    [<matplotlib.lines.Line2D at 0x2a21208bc40>]




    
![png](output_32_1.png)
    

