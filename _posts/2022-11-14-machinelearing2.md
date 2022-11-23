---
title:  "[Python] 머신러닝_논리회귀.다항논리회귀" 

categories:
  - Python
tags:
  - [Python,ADP,machine_learning]

toc: true
toc_sticky: true

date: 2022-11-14

---


## 논리회귀(Logistic regression) ~sigmoid Function

예시) 대학교 시험 전날 공부한 시간을 보고 Pass(1) Fail(0) 예측

만약에 선형회귀를 사용하면 이상하고 정확도가 낮음.
![1](https://user-images.githubusercontent.com/88616282/201675988-5d0cac5c-678e-457b-9a72-e8b9714f2720.png)

![2](https://user-images.githubusercontent.com/88616282/201676041-b359bcce-cd8d-492c-86fb-45203f0c85ec.png)

Logistic Function 곡선형태로 그리니깐 구분이 가능해 계산 자체는 선형 회귀와 똑같지만 출력에 sigmoid를 붙여서 H(x)는 0~1사이 값을 가지게끔함. 

![4](https://user-images.githubusercontent.com/88616282/201676310-b603b504-8cc6-4e1e-bcb3-b8174a81edc9.png)

-확률로써 구분을 하게됨

-초록색 선=임계치=Threshold ex)0.5기준으로 통과 확률을 봄 

-필요한거 (1)가설 (2)손실함수(최소화하는게 중요함/cross entropy라는걸 씀)
![6](https://user-images.githubusercontent.com/88616282/201676218-bada9335-06ba-4377-a73c-16f3e4c55c55.png)

**수학보다는 개념이 중요**
0일 확률 100% 1일때 확률 0%되게끔 만들어야함
![7](https://user-images.githubusercontent.com/88616282/201676425-3b5af2b7-7661-4b09-b232-142efa85caa0.png)

-Keras에서는 binary_crossentropy손실 함수를 씀 

## 다항논리회귀(Multinomial logistic regression)~Softmax Function

예시) 대학교 시험 전날 공부한 시간을 보고 성적 ABCD 예측

**One-hot encoding(0과1)**
컴퓨터 친화적으로 입력해줌. 배열을 0으로 채워줌 

**softmax**
![8](https://user-images.githubusercontent.com/88616282/201676562-e19f0ddc-aa5e-4b72-8432-1dad9134e841.png)

비슷한 가중치를 줘서 모든 값 확률 합했을때 1로 만들어줌.

결과값과 비교해서 차이를 줄여주는걸 cross entropy라고함 

확률분포 함수 그래프로 그림 

라벨이 0,1,2가 됨 

-Keras에서는 categorical_crossentropy손실 함수를 씀 
![9](https://user-images.githubusercontent.com/88616282/201676524-71741510-f480-4153-ace2-f06e24c79514.png)



## 차이점 정리 

**단항 논리 회귀**

(1)sigmoid를 써서, 0or1으로만 나눔

(2)cross entropy 확률분포 그래프 계산해서 최소화 

**다항 논리 회귀**

(1)softmax를 써서

(2)cross entropy 확률분포 그래프 계산해서 최소화 

## 머신러닝 모델_SVM
-Support Vertor Machine

-강아지와 고양이를 각 특징별로 분류를 한다 

-선을 긋는 것이 굉장히 중요하고 선 기준으로 거리가 최대가 되도록 구해야함

-margin이 클수록 좋다고보면됨 
![1](https://user-images.githubusercontent.com/88616282/202183568-907c6819-06d0-4f2b-8d20-e13a2bcc8794.png)

-문제점: 갑자기 충성심(강아지 특징)이 강한 고양이가 등장한다

->다리 길이나 울음소리 높낮이같은 특징Feature를 늘리면됨

->그리고 3차원으로 만들면됨

->결론: Feature가 늘수록 성능이 좋아진다 

## 머신러닝 모델_KNN
-k-Nearest Neighbors

-거리 기준으로 판단하는 것 예시의 경우 k=2

![image](https://user-images.githubusercontent.com/88616282/202184406-20c71063-cdd3-48d2-a46f-44957b413abd.png)

-직관적이고 쉬운데 성능도 괜찮음 

## 머신러닝 모델_의사결정나무(Decision Tree)
![image](https://user-images.githubusercontent.com/88616282/202184639-7dd4bb9f-4f3a-4ab5-852d-c144fd4f4d80.png)
-스무고개와 같음

## 머신러닝 모델_랜덤포레스트(Random Forest)
-위의 의사결정나무를 여러개를 모아둔거 
![image](https://user-images.githubusercontent.com/88616282/202184969-9eb76af5-3f47-48c9-8e22-ae04b96d9ad0.png)

(1)Majority Vote 

(2)평균

## 전처리(Preprocessing)

-너무 벗어난 값들은 지워주는 일 또는 단위 맞춰주기 (데이터 정제작업)

-코로나 확진자가 너무 많은 중국/미국 같은 경우 지워주는 작업(아웃라이어 제거)

-왜 전처리를 할까?

예를 들어서 부동산 데이터 분석을 한다고 보자(집 넓이/준공 연도/층수)->범위 단위가 다 달라 

학습속도를 빠르게하고 지역해local minimum에 빠지는걸 방지함

## 정규화(Normalization)
-데이터를 0에서 1사이로 만듬. 99퍼 모델이 사용함 

-예시: 100점만점에서 50점(A) & 500점 만점에서 50점(B) -> 0.5(A) & 0.1(B) -> A가 더 잘한거 

## 표준화(Standardization)
-데이터의 분포를 정규분포로 바꿔줌 

-데이터 평균은 0이고 표준편차는 1이 되도록 만들어줌 
![image](https://user-images.githubusercontent.com/88616282/202186635-a34eaf94-9080-4b84-8a1a-d582aa9da68e.png)

![image](https://user-images.githubusercontent.com/88616282/202186742-275455e7-f4a0-4465-aa66-3e4c7e27e729.png)




