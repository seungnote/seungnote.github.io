---
title:  "[Python] 머신러닝_선형회귀 with Tensorflow&Keras" 

categories:
  - Python
tags:
  - [Python,ADP,machine_learning]

toc: true
toc_sticky: true

date: 2022-11-08

---

## 머신러닝이란?

1. 회귀(연속적 문제 해결시)
-사람의 얼굴 사진을 보고 몇살인지 예측하는거
-Input(얼굴사진)&Output(나이예측) 중요

2. 분류(비연속적 문제)
-전달 공부시간을 가지고 과목 이수여부 또는 성적을 예측한다 

3. 회귀&분류

(1)지도학습(회귀/분류)
-Input사과 사진/ Output 사과/ 라벨링(annotation=정답 입력하는 작업)

(2)비지도학습(군집/차원축소/시각화/연관규칙)
-알아서 같은거끼리 묶는것
-Input 엄청 많음 / 알아서 분류함 / 명칭만 입력해줌

(3)강화학습(알파고)
-경우의 수 확률을 보상받으면서 학습을 한다
-게임 방향키처럼 행동은 목록이 정해져있어야함

## 선형회귀(Tensorflow)
**H(x)=Wx + b(가설)**

-Weight와 Bias를 알아야봐야하는데 이걸 기계로 시킨다 

-ex)커피 마신 잔 수로(Input) 시험점수를(Output) 예측할 수 있을까? 

-점과 직선의 거리는 짧아야함(=mean squared error=평균제곱 오차)

-cost Function(손실함수) 값이 작아야함 

![화면 캡처 2022-11-14 220725](https://user-images.githubusercontent.com/88616282/201667958-a5841d84-ec52-406a-b130-9a52e0424a9d.png)


-최근 Tensorflow보다 Keras를 사용함 

-Tensorflow는 소숫점을 주로 씀 

-버젼 v1으로 실행한다 

-사용할 데이터셋 설정(x_data, y_data)

-데이터셋 넣어줄 공간 생성(X,Y placeholder)

-Weight& Bias 설정 

```python
import tensorflow as tf

# 버젼 v1으로 실행 

tf.compat.v1.disable_eager_execution()

# 입력 x_data
# 출력 y_data
# 각각 대응이 됨. [1,1] 넣으면 [10]이 나와야함 ...

x_data=[[1,1],[2,2],[3,3]]
y_data=[[10],[20],[30]]

# x&y를 넣어줄 공간을 만드는법
# placeholder 씀. 이건 데이터의 형태를 지정해줘야함(소숫점 float)
# 32bit 소숫점 

#x_data를 보면 [1,1] 이렇게 값이 두개라서 
X=tf.compat.v1.placeholder(tf.float32, shape=[None,2])
Y=tf.compat.v1.placeholder(tf.float32, shape=[None,1])

# Weight와 Bias를 설정 
# 손실함수는 랜덤으로 점시 시작되기 때문에 random.normal으로 이니셜 시킴
# shape는 행렬

W=tf.Variable(tf.random.normal(shape=(2, 1)), name='W')
b=tf.Variable(tf.random.normal(shape=(1,)), name='b')

```

-가설과 옵티마이저 정의

-hypothesis Y=Wx+b 

-cost function
1. 가설(hypothesis)에서 정답값Y를 뺌
2. 제곱 square 함
3. 다시 평균을 냄 mean

-optimizer 스텝 단위& cost 최소화 


```python
# 가설 Y=Wx+b ~선형회귀
# matmul=matrix multiplication 곱하기 의미 
hypothesis=tf.matmul(X,W)+b

# cost Function
cost=tf.reduce_mean(tf.square(hypothesis-Y))

# 0.01 스텝씩 간다는거
# cost는 최소화되는 방향으로 
optimizer=tf.compat.v1.train.GradientDescentOptimizer(learning_rate=0.01).minimize(cost)
```

-Session= 저장소

-sess.run을 통해서 초기화를 시켜준다

-반복 학습 range(50)=50번
1. 공간에 데이터 셋 넣어줌
2. step별 cost 표시 

-좋은 모델은? step이 늘수록 loss/cost가 줄어들때 

-추가 검증을 해봐서 규칙에 맞는지 봄 


```python
with tf.compat.v1.Session() as sess:
    sess.run(tf.compat.v1.global_variables_initializer())
    
    # 데이터셋 넣어준다=feeding 
    
    for step in range(50):
        c, W_, b_, _ = sess.run([cost, W, b, optimizer], feed_dict={X: x_data, Y: y_data})
        print('Step: %2d\t loss: %.2f\t' % (step, c))
     
    # 아까전에 [1,1]은 [10] [2,2]는 [20]이 나왔듯이 [4,4]는 [40]이여야함
    # 검증시 39.1이 나오기때문에 학습이 잘됐다는걸 알수있음. 
    
    print(sess.run(hypothesis, feed_dict={X: [[4, 4]]}))
    
```

    Step:  0	 loss: 594.53	
    Step:  1	 loss: 376.75	
    Step:  2	 loss: 238.78	
    Step:  3	 loss: 151.37	
    Step:  4	 loss: 96.00	
    Step:  5	 loss: 60.91	
    Step:  6	 loss: 38.69	
    Step:  7	 loss: 24.60	
    Step:  8	 loss: 15.68	
    Step:  9	 loss: 10.03	
    Step: 10	 loss: 6.45	
    Step: 11	 loss: 4.18	
    Step: 12	 loss: 2.74	
    Step: 13	 loss: 1.83	
    Step: 14	 loss: 1.25	
    Step: 15	 loss: 0.88	
    Step: 16	 loss: 0.65	
    Step: 17	 loss: 0.50	
    Step: 18	 loss: 0.41	
    Step: 19	 loss: 0.35	
    Step: 20	 loss: 0.31	
    Step: 21	 loss: 0.28	
    Step: 22	 loss: 0.27	
    Step: 23	 loss: 0.26	
    Step: 24	 loss: 0.25	
    Step: 25	 loss: 0.24	
    Step: 26	 loss: 0.24	
    Step: 27	 loss: 0.24	
    Step: 28	 loss: 0.24	
    Step: 29	 loss: 0.23	
    Step: 30	 loss: 0.23	
    Step: 31	 loss: 0.23	
    Step: 32	 loss: 0.23	
    Step: 33	 loss: 0.23	
    Step: 34	 loss: 0.23	
    Step: 35	 loss: 0.23	
    Step: 36	 loss: 0.22	
    Step: 37	 loss: 0.22	
    Step: 38	 loss: 0.22	
    Step: 39	 loss: 0.22	
    Step: 40	 loss: 0.22	
    Step: 41	 loss: 0.22	
    Step: 42	 loss: 0.22	
    Step: 43	 loss: 0.22	
    Step: 44	 loss: 0.21	
    Step: 45	 loss: 0.21	
    Step: 46	 loss: 0.21	
    Step: 47	 loss: 0.21	
    Step: 48	 loss: 0.21	
    Step: 49	 loss: 0.21	
    [[39.108223]]
    

## 선형회귀(Keras)

-선형회귀의 경우 출력이 1개여서 dense=1이됨 

-fit:가설의 정답값을 맞춘다! 

-반복학습 횟수 epochs 100번 


```python
import numpy as np
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.optimizers import Adam, SGD

x_data = np.array([[1], [2], [3]])
y_data = np.array([[10], [20], [30]])

# 순차적 
model = Sequential([
  Dense(1)
])

# 수식 안써도됨 
model.compile(loss='mean_squared_error', optimizer=SGD(lr=0.1))

model.fit(x_data, y_data, epochs=100) # epochs 복수형

```

    Train on 3 samples
    Epoch 1/100
    3/3 [==============================] - 0s 28ms/sample - loss: 536.4362
    Epoch 2/100
    3/3 [==============================] - 0s 470us/sample - loss: 8.5149
    Epoch 3/100
    3/3 [==============================] - 0s 1ms/sample - loss: 2.1087
    Epoch 4/100
    3/3 [==============================] - 0s 665us/sample - loss: 1.9368
    Epoch 5/100
    3/3 [==============================] - 0s 664us/sample - loss: 1.8439
    Epoch 6/100
    3/3 [==============================] - 0s 332us/sample - loss: 1.7563
    Epoch 7/100
    3/3 [==============================] - 0s 332us/sample - loss: 1.6729
    Epoch 8/100
    3/3 [==============================] - 0s 333us/sample - loss: 1.5935
    Epoch 9/100
    3/3 [==============================] - 0s 1ms/sample - loss: 1.5178
    Epoch 10/100
    3/3 [==============================] - 0s 999us/sample - loss: 1.4457
    Epoch 11/100
    3/3 [==============================] - 0s 664us/sample - loss: 1.3770
    Epoch 12/100
    3/3 [==============================] - 0s 665us/sample - loss: 1.3116
    Epoch 13/100
    3/3 [==============================] - 0s 665us/sample - loss: 1.2493
    Epoch 14/100
    3/3 [==============================] - 0s 665us/sample - loss: 1.1899
    Epoch 15/100
    3/3 [==============================] - 0s 1ms/sample - loss: 1.1334
    Epoch 16/100
    3/3 [==============================] - 0s 593us/sample - loss: 1.0796
    Epoch 17/100
    3/3 [==============================] - 0s 996us/sample - loss: 1.0283
    Epoch 18/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.9795
    Epoch 19/100
    3/3 [==============================] - 0s 664us/sample - loss: 0.9329
    Epoch 20/100
    3/3 [==============================] - 0s 998us/sample - loss: 0.8886
    Epoch 21/100
    3/3 [==============================] - 0s 2ms/sample - loss: 0.8464
    Epoch 22/100
    3/3 [==============================] - 0s 991us/sample - loss: 0.8062
    Epoch 23/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.7679
    Epoch 24/100
    3/3 [==============================] - 0s 998us/sample - loss: 0.7314
    Epoch 25/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.6967
    Epoch 26/100
    3/3 [==============================] - 0s 996us/sample - loss: 0.6636
    Epoch 27/100
    3/3 [==============================] - 0s 664us/sample - loss: 0.6321
    Epoch 28/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.6021
    Epoch 29/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.5735
    Epoch 30/100
    3/3 [==============================] - 0s 2ms/sample - loss: 0.5462
    Epoch 31/100
    3/3 [==============================] - 0s 998us/sample - loss: 0.5203
    Epoch 32/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.4956
    Epoch 33/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.4720
    Epoch 34/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.4496
    Epoch 35/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.4282
    Epoch 36/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.4079
    Epoch 37/100
    3/3 [==============================] - 0s 664us/sample - loss: 0.3885
    Epoch 38/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.3701
    Epoch 39/100
    3/3 [==============================] - 0s 1000us/sample - loss: 0.3525
    Epoch 40/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.3357
    Epoch 41/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.3198
    Epoch 42/100
    3/3 [==============================] - 0s 332us/sample - loss: 0.3046
    Epoch 43/100
    3/3 [==============================] - 0s 667us/sample - loss: 0.2901
    Epoch 44/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.2764
    Epoch 45/100
    3/3 [==============================] - 0s 2ms/sample - loss: 0.2632
    Epoch 46/100
    3/3 [==============================] - 0s 663us/sample - loss: 0.2507
    Epoch 47/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.2388
    Epoch 48/100
    3/3 [==============================] - 0s 667us/sample - loss: 0.2275
    Epoch 49/100
    3/3 [==============================] - 0s 2ms/sample - loss: 0.2167
    Epoch 50/100
    3/3 [==============================] - 0s 2ms/sample - loss: 0.2064
    Epoch 51/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.1966
    Epoch 52/100
    3/3 [==============================] - 0s 2ms/sample - loss: 0.1872
    Epoch 53/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.1783
    Epoch 54/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.1699
    Epoch 55/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.1618
    Epoch 56/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.1541
    Epoch 57/100
    3/3 [==============================] - 0s 996us/sample - loss: 0.1468
    Epoch 58/100
    3/3 [==============================] - 0s 664us/sample - loss: 0.1398
    Epoch 59/100
    3/3 [==============================] - 0s 329us/sample - loss: 0.1332
    Epoch 60/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.1269
    Epoch 61/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.1208
    Epoch 62/100
    3/3 [==============================] - 0s 664us/sample - loss: 0.1151
    Epoch 63/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.1096
    Epoch 64/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.1044
    Epoch 65/100
    3/3 [==============================] - 0s 2ms/sample - loss: 0.0995
    Epoch 66/100
    3/3 [==============================] - 0s 998us/sample - loss: 0.0947
    Epoch 67/100
    3/3 [==============================] - 0s 332us/sample - loss: 0.0902
    Epoch 68/100
    3/3 [==============================] - 0s 2ms/sample - loss: 0.0859
    Epoch 69/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.0819
    Epoch 70/100
    3/3 [==============================] - 0s 996us/sample - loss: 0.0780
    Epoch 71/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.0743
    Epoch 72/100
    3/3 [==============================] - 0s 2ms/sample - loss: 0.0707
    Epoch 73/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.0674
    Epoch 74/100
    3/3 [==============================] - 0s 664us/sample - loss: 0.0642
    Epoch 75/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.0611
    Epoch 76/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.0582
    Epoch 77/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.0555
    Epoch 78/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.0528
    Epoch 79/100
    3/3 [==============================] - 0s 471us/sample - loss: 0.0503
    Epoch 80/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.0479
    Epoch 81/100
    3/3 [==============================] - 0s 2ms/sample - loss: 0.0457
    Epoch 82/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.0435
    Epoch 83/100
    3/3 [==============================] - 0s 664us/sample - loss: 0.0414
    Epoch 84/100
    3/3 [==============================] - 0s 664us/sample - loss: 0.0395
    Epoch 85/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.0376
    Epoch 86/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.0358
    Epoch 87/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.0341
    Epoch 88/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.0325
    Epoch 89/100
    3/3 [==============================] - 0s 664us/sample - loss: 0.0309
    Epoch 90/100
    3/3 [==============================] - 0s 772us/sample - loss: 0.0295
    Epoch 91/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.0281
    Epoch 92/100
    3/3 [==============================] - 0s 997us/sample - loss: 0.0267
    Epoch 93/100
    3/3 [==============================] - 0s 333us/sample - loss: 0.0255
    Epoch 94/100
    3/3 [==============================] - 0s 332us/sample - loss: 0.0242
    Epoch 95/100
    3/3 [==============================] - 0s 333us/sample - loss: 0.0231
    Epoch 96/100
    3/3 [==============================] - 0s 1ms/sample - loss: 0.0220
    Epoch 97/100
    3/3 [==============================] - 0s 996us/sample - loss: 0.0210
    Epoch 98/100
    3/3 [==============================] - 0s 333us/sample - loss: 0.0200
    Epoch 99/100
    3/3 [==============================] - 0s 333us/sample - loss: 0.0190
    Epoch 100/100
    3/3 [==============================] - 0s 665us/sample - loss: 0.0181
    




    <keras.callbacks.History at 0x28ecfc24580>



**테스트 데이터 예측하기

-4는 40에 가깝고 5는 50에 가까움 


```python
y_pred=model.predict([[4]])
print(y_pred)
```

    [[39.736607]]
    

    D:\anaconda\lib\site-packages\keras\engine\training_v1.py:2356: UserWarning: `Model.state_updates` will be removed in a future version. This property should not be used in TensorFlow 2.0, as `updates` are applied automatically.
      updates=self.state_updates,
    
