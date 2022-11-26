---
title:  "[Python] 머신러닝_딥러닝 MNIST 실습" 

categories:
  - Python
tags:
  - [Python,ADP,machine_learning]

toc: true
toc_sticky: true

date: 2022-11-26

---
## Sign Language MNIST(수화 알파벳) 실습

https://www.kaggle.com/datamunge/sign-language-mnist
![111](https://user-images.githubusercontent.com/88616282/204070025-0d5cf5be-7b30-4d5d-851c-a473cc7361de.png)



```python
import os
os.environ['KAGGLE_USERNAME'] = 'seungnote' # username
os.environ['KAGGLE_KEY'] = 'bc254ae94554f39d41fcab91537514ad' # key
```


```python
!kaggle datasets download -d datamunge/sign-language-mnist
```

    Downloading sign-language-mnist.zip to D:\anaconda\00.studying
    
    

    
      0%|          | 0.00/62.6M [00:00<?, ?B/s]
      2%|1         | 1.00M/62.6M [00:00<00:06, 10.2MB/s]
      3%|3         | 2.00M/62.6M [00:00<00:06, 10.0MB/s]
      6%|6         | 4.00M/62.6M [00:00<00:09, 6.15MB/s]
      8%|7         | 5.00M/62.6M [00:01<00:14, 4.22MB/s]
     10%|9         | 6.00M/62.6M [00:01<00:14, 3.99MB/s]
     13%|#2        | 8.00M/62.6M [00:01<00:09, 5.81MB/s]
     16%|#5        | 10.0M/62.6M [00:01<00:07, 7.20MB/s]
     19%|#9        | 12.0M/62.6M [00:01<00:06, 8.34MB/s]
     22%|##2       | 14.0M/62.6M [00:02<00:05, 9.27MB/s]
     24%|##3       | 15.0M/62.6M [00:02<00:05, 9.44MB/s]
     27%|##7       | 17.0M/62.6M [00:02<00:04, 10.2MB/s]
     30%|###       | 19.0M/62.6M [00:02<00:04, 10.5MB/s]
     34%|###3      | 21.0M/62.6M [00:02<00:04, 10.9MB/s]
     37%|###6      | 23.0M/62.6M [00:02<00:03, 11.0MB/s]
     40%|###9      | 25.0M/62.6M [00:03<00:03, 11.0MB/s]
     43%|####3     | 27.0M/62.6M [00:03<00:03, 11.4MB/s]
     46%|####6     | 29.0M/62.6M [00:03<00:03, 11.3MB/s]
     50%|####9     | 31.0M/62.6M [00:03<00:02, 11.3MB/s]
     53%|#####2    | 33.0M/62.6M [00:03<00:02, 11.5MB/s]
     56%|#####5    | 35.0M/62.6M [00:03<00:02, 11.4MB/s]
     59%|#####9    | 37.0M/62.6M [00:04<00:02, 11.4MB/s]
     62%|######2   | 39.0M/62.6M [00:04<00:02, 11.4MB/s]
     66%|######5   | 41.0M/62.6M [00:04<00:01, 11.6MB/s]
     69%|######8   | 43.0M/62.6M [00:04<00:01, 11.5MB/s]
     72%|#######1  | 45.0M/62.6M [00:04<00:01, 11.4MB/s]
     75%|#######5  | 47.0M/62.6M [00:05<00:01, 9.70MB/s]
     77%|#######6  | 48.0M/62.6M [00:05<00:01, 9.44MB/s]
     80%|#######9  | 50.0M/62.6M [00:05<00:01, 10.2MB/s]
     83%|########3 | 52.0M/62.6M [00:05<00:01, 10.5MB/s]
     86%|########6 | 54.0M/62.6M [00:05<00:00, 10.7MB/s]
     89%|########9 | 56.0M/62.6M [00:06<00:00, 10.9MB/s]
     93%|#########2| 58.0M/62.6M [00:06<00:00, 11.2MB/s]
     96%|#########5| 60.0M/62.6M [00:06<00:00, 11.2MB/s]
     99%|#########9| 62.0M/62.6M [00:06<00:00, 11.5MB/s]
    100%|##########| 62.6M/62.6M [00:06<00:00, 9.87MB/s]
    


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


```python
dtrain=pd.read_csv("D:/anaconda/00.studying/sign-language-mnist/sign_mnist_train.csv")

dtrain.head(5)
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




```python
dtest=pd.read_csv("D:/anaconda/00.studying/sign-language-mnist/sign_mnist_test.csv")

dtest.head(5)
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
      <td>6</td>
      <td>149</td>
      <td>149</td>
      <td>150</td>
      <td>150</td>
      <td>150</td>
      <td>151</td>
      <td>151</td>
      <td>150</td>
      <td>151</td>
      <td>...</td>
      <td>138</td>
      <td>148</td>
      <td>127</td>
      <td>89</td>
      <td>82</td>
      <td>96</td>
      <td>106</td>
      <td>112</td>
      <td>120</td>
      <td>107</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>126</td>
      <td>128</td>
      <td>131</td>
      <td>132</td>
      <td>133</td>
      <td>134</td>
      <td>135</td>
      <td>135</td>
      <td>136</td>
      <td>...</td>
      <td>47</td>
      <td>104</td>
      <td>194</td>
      <td>183</td>
      <td>186</td>
      <td>184</td>
      <td>184</td>
      <td>184</td>
      <td>182</td>
      <td>180</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10</td>
      <td>85</td>
      <td>88</td>
      <td>92</td>
      <td>96</td>
      <td>105</td>
      <td>123</td>
      <td>135</td>
      <td>143</td>
      <td>147</td>
      <td>...</td>
      <td>68</td>
      <td>166</td>
      <td>242</td>
      <td>227</td>
      <td>230</td>
      <td>227</td>
      <td>226</td>
      <td>225</td>
      <td>224</td>
      <td>222</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>203</td>
      <td>205</td>
      <td>207</td>
      <td>206</td>
      <td>207</td>
      <td>209</td>
      <td>210</td>
      <td>209</td>
      <td>210</td>
      <td>...</td>
      <td>154</td>
      <td>248</td>
      <td>247</td>
      <td>248</td>
      <td>253</td>
      <td>236</td>
      <td>230</td>
      <td>240</td>
      <td>253</td>
      <td>255</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>188</td>
      <td>191</td>
      <td>193</td>
      <td>195</td>
      <td>199</td>
      <td>201</td>
      <td>202</td>
      <td>203</td>
      <td>203</td>
      <td>...</td>
      <td>26</td>
      <td>40</td>
      <td>64</td>
      <td>48</td>
      <td>29</td>
      <td>46</td>
      <td>49</td>
      <td>46</td>
      <td>46</td>
      <td>53</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 785 columns</p>
</div>



## 라벨 분포 보기

주의사항: 9=J 25=z는 동작이 들어가기때문에 제외함

총 24개 라벨


```python
plt.figure(figsize=(16,10))
sns.countplot(dtrain['label'])
plt.snow()
# 0= A 1=B 
```

    D:\anaconda\lib\site-packages\seaborn\_decorators.py:36: FutureWarning: Pass the following variable as a keyword arg: x. From version 0.12, the only valid positional argument will be `data`, and passing other arguments without an explicit keyword will result in an error or misinterpretation.
      warnings.warn(
    


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    Input In [7], in <cell line: 3>()
          1 plt.figure(figsize=(16,10))
          2 sns.countplot(dtrain['label'])
    ----> 3 plt.snow()
    

    AttributeError: module 'matplotlib.pyplot' has no attribute 'snow'

![output_7_2](https://user-images.githubusercontent.com/88616282/204069848-dd0b77d3-21f3-4d8a-8ea8-daedab951b92.png)


## 데이터 전처리(입력 출력 나누기)


```python
dtrain = dtrain.astype(np.float32)
x_train = dtrain.drop(columns=['label'], axis=1).values
y_train = dtrain[['label']].values

dtest = dtest.astype(np.float32)
x_test = dtest.drop(columns=['label'], axis=1).values
y_test = dtest[['label']].values

print(x_train.shape, y_train.shape)
print(x_test.shape, y_test.shape)
```

    (27455, 784) (27455, 1)
    (7172, 784) (7172, 1)
    

## 데이터 미리보기(픽셀 -> 2차원으로 만들어야)


```python
index = 1
plt.title(str(y_train[index]))
plt.imshow(x_train[index].reshape((28, 28)), cmap='gray')
plt.show()

# 6=G 에 해당되는 라벨이라는거 
```

![output_11_0](https://user-images.githubusercontent.com/88616282/204069828-a3caceec-b9aa-4bf7-9dc9-1cf3b775e180.png)


## One-hot encoding


```python
encoder = OneHotEncoder()
y_train = encoder.fit_transform(y_train).toarray()
y_test = encoder.fit_transform(y_test).toarray()

print(y_train.shape)
```

    (27455, 24)
    


```python
# 제대로 됐는지 확인하는 방법
# 0과 1로 표현된거 체크 
index = 1
plt.title(str(y_train[index]))
plt.imshow(x_train[index].reshape((28, 28)), cmap='gray')
plt.show()
```


![output_14_0](https://user-images.githubusercontent.com/88616282/204024100-7e707691-f3d2-41c6-94f3-e6d41114642e.png)



## 일반화 Normalization

이미지 데이터 픽셀 0-255사이 정수8bit이다

이것을 255로 나누어 0-1 사이의 소수점 데이터 float32로 바꾸고 일반화 


```python
x_train = x_train / 255.
x_test = x_test / 255.
```

## 네트워크 구성

입력층

은닉층 3개 relu

출력층 softmax(다항논리회귀)

26개중에서 2개뺀 24개가 나와야함 



```python
input = Input(shape=(784,))
hidden = Dense(1024, activation='relu')(input)
hidden = Dense(512, activation='relu')(hidden)
hidden = Dense(256, activation='relu')(hidden)
output = Dense(24, activation='softmax')(hidden)

model = Model(inputs=input, outputs=output)

#acc 정확도를 0~1사이로 표현
model.compile(loss='categorical_crossentropy', optimizer=Adam(lr=0.001), metrics=['acc'])

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

1,466,136-> 학습시켜서 w&b를 부여할 것

loss는 떨어지고 acc는 올라가는걸 볼 수 있음 


```python
history = model.fit(
    x_train,
    y_train,
    validation_data=(x_test, y_test), # 검증 데이터를 넣어주면 한 epoch이 끝날때마다 자동으로 검증
    epochs=20 # epochs 복수형으로 쓰기!
)

#loss: 0.0132 - acc: 0.9963 - val_loss: 0.9069 - val_acc: 0.8352
```

    Epoch 1/20
    858/858 [==============================] - 11s 11ms/step - loss: 1.7704 - acc: 0.4192 - val_loss: 1.2189 - val_acc: 0.5750
    Epoch 2/20
    858/858 [==============================] - 9s 11ms/step - loss: 0.6509 - acc: 0.7710 - val_loss: 1.0843 - val_acc: 0.6293
    Epoch 3/20
    858/858 [==============================] - 9s 11ms/step - loss: 0.3024 - acc: 0.8947 - val_loss: 1.0043 - val_acc: 0.7034
    Epoch 4/20
    858/858 [==============================] - 9s 10ms/step - loss: 0.1765 - acc: 0.9391 - val_loss: 1.2293 - val_acc: 0.7362
    Epoch 5/20
    858/858 [==============================] - 8s 10ms/step - loss: 0.1296 - acc: 0.9590 - val_loss: 0.9269 - val_acc: 0.8030
    Epoch 6/20
    858/858 [==============================] - 9s 11ms/step - loss: 0.1157 - acc: 0.9620 - val_loss: 1.1897 - val_acc: 0.7369
    Epoch 7/20
    858/858 [==============================] - 10s 11ms/step - loss: 0.0992 - acc: 0.9672 - val_loss: 0.9136 - val_acc: 0.8107
    Epoch 8/20
    858/858 [==============================] - 9s 11ms/step - loss: 0.0713 - acc: 0.9784 - val_loss: 1.1433 - val_acc: 0.7727
    Epoch 9/20
    858/858 [==============================] - 8s 10ms/step - loss: 0.0327 - acc: 0.9891 - val_loss: 0.9604 - val_acc: 0.8346
    Epoch 10/20
    858/858 [==============================] - 8s 10ms/step - loss: 5.2972e-04 - acc: 1.0000 - val_loss: 1.0298 - val_acc: 0.8398
    Epoch 11/20
    858/858 [==============================] - 8s 9ms/step - loss: 2.8457e-04 - acc: 1.0000 - val_loss: 1.0790 - val_acc: 0.8385
    Epoch 12/20
    858/858 [==============================] - 8s 9ms/step - loss: 1.7864e-04 - acc: 1.0000 - val_loss: 1.1042 - val_acc: 0.8355
    Epoch 13/20
    858/858 [==============================] - 8s 9ms/step - loss: 0.1184 - acc: 0.9711 - val_loss: 1.1579 - val_acc: 0.6341
    Epoch 14/20
    858/858 [==============================] - 8s 9ms/step - loss: 0.0847 - acc: 0.9745 - val_loss: 0.9299 - val_acc: 0.8118
    Epoch 15/20
    858/858 [==============================] - 8s 9ms/step - loss: 0.0670 - acc: 0.9800 - val_loss: 0.8909 - val_acc: 0.8087
    Epoch 16/20
    858/858 [==============================] - 8s 9ms/step - loss: 0.0037 - acc: 0.9998 - val_loss: 0.9776 - val_acc: 0.8228
    Epoch 17/20
    858/858 [==============================] - 8s 10ms/step - loss: 8.1397e-04 - acc: 1.0000 - val_loss: 1.0458 - val_acc: 0.8197
    Epoch 18/20
    858/858 [==============================] - 9s 11ms/step - loss: 0.0462 - acc: 0.9927 - val_loss: 2.4127 - val_acc: 0.4314
    Epoch 19/20
    858/858 [==============================] - 9s 10ms/step - loss: 0.1494 - acc: 0.9525 - val_loss: 1.1035 - val_acc: 0.7375
    Epoch 20/20
    858/858 [==============================] - 8s 10ms/step - loss: 0.0132 - acc: 0.9963 - val_loss: 0.9069 - val_acc: 0.8352
    

## 학습 결과 그래프(plot)


```python
# loss 결과 
plt.figure(figsize=(16, 10))
plt.plot(history.history['loss'])
plt.plot(history.history['val_loss'])

#training loss가 파란색
#validation loss가 주황색 
```




    [<matplotlib.lines.Line2D at 0x23c0c270460>]




    
![output_22_1](https://user-images.githubusercontent.com/88616282/204024146-19aea3ed-a8fc-4b01-8504-88eb7bf7b83f.png)

    



```python
# acc 결과( 올라간다)
plt.figure(figsize=(16, 10))
plt.plot(history.history['acc'])
plt.plot(history.history['val_acc'])
```




    [<matplotlib.lines.Line2D at 0x23c0c2d3a90>]




    
![output_23_1](https://user-images.githubusercontent.com/88616282/204024118-5b3d576f-86c3-49ea-a94a-35f466f020e4.png)




```python

```
