## 선형회귀 실습

-최근 Tensorflow보다 Keras를 사용함 

-Tensorflow는 소숫점을 주로 씀 


```python
import tensorflow as tf

# 버젼 v1으로 실행 

tf.compat.v1.disable_eager_execution()

# 사용할 데이터셋 설정
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


```python
# 가설과 옵티마이저를 정의해야함
# 가설 Y=Wx+b ~선형회귀
# matmul=matrix multiplication 곱하기 의미 
hypothesis=tf.matmul(X,W)+b

# cost Function
# 가설에서 정답값Y 를 빼고 
# 제곱 square를 한다 
# 그걸 다시 평균을 낸다 
cost=tf.reduce_mean(tf.square(hypothesis-Y))

# 0.01 스텝씩 간다는거
# cost는 최소화되는 방향으로 
optimizer=tf.compat.v1.train.GradientDescentOptimizer(learning_rate=0.01).minimize(cost)
```


```python
# Session= 저장소
# sess.run을 통해서 초기화를 시켜준다

with tf.compat.v1.Session() as sess:
    sess.run(tf.compat.v1.global_variables_initializer())
    
    # 50번동안 반복 학습 시킴 
    # 데이터셋 넣어준다=feeding 
    # 각 스텝별로 Cost(loss)를 표현해줌 
    
    for step in range(50):
        c, W_, b_, _ = sess.run([cost, W, b, optimizer], feed_dict={X: x_data, Y: y_data})
        print('Step: %2d\t loss: %.2f\t' % (step, c))
     
    # step이 늘어날수록 loss가 줄어드는걸 확인할수있음
    # 좋다는뜻임
    
    # 검증을 해봄 
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
    

```

```
