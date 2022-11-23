---
title:  "[Python] 머신러닝_딥러닝개념" 

categories:
  - Python
tags:
  - [Python,ADP,machine_learning]

toc: true
toc_sticky: true

date: 2022-11-23

---
## 딥러닝이란?
: 머신러닝의 한 종류 
딥러닝(Deep learning)=Deep neural networks=Multilayer Perceptron(MLP)

![1](https://user-images.githubusercontent.com/88616282/203530847-d316877e-3e9e-4ccb-8474-89d4ec208292.png)
지금까지 선형회귀&논리회귀는 모두 1차 함수 y=ax+b

하지만 현실에서는 비선형일때 풀 수 있는 문제들이 더 많다 
![2](https://user-images.githubusercontent.com/88616282/203530864-420bb395-c3be-4840-b475-0e1dad9e402f.png)

사이에 비선형을 넣어야한다 


![3](https://user-images.githubusercontent.com/88616282/203530872-30342994-f48e-4abf-9136-246cac6aa544.png)

## 역전파 알고리즘
선형회귀로 AND OR는 풀지만 XOR는 안됨  
![image](https://user-images.githubusercontent.com/88616282/203531666-c11e145b-bd18-49f2-b3d3-9fb2814f2f68.png)

->이것을 나중에 역전파Backpropagation 알고리즘 발견함 XOR해결함 
![image](https://user-images.githubusercontent.com/88616282/203532417-4489e923-ec35-4e84-bf79-94f1c17ad276.png)

1)많은 이미지들을 MLP에 넣고
2) 정답값과 비교해서 틀리면 weight&bias 고치고 (이걸 반복)

## MLP(Multi Layer Perceptron)
딥 러닝 구조: 입력층/**은닉층**/출력층 = Input/Hidden/Output

![image](https://user-images.githubusercontent.com/88616282/203532836-4cedd774-2820-4f52-bf08-c374236bd2f0.png)
![image](https://user-images.githubusercontent.com/88616282/203533013-2142dc9c-ed05-4c59-9e26-3dc37807fc82.png)

보편적으로 아래와 같이 노드의 개수가 점점 늘어나다가 줄어드는 방식으로 구성:

입력층의 노드 개수 4개-> 첫 번째 은닉층 노드 개수 8개->두 번째 은닉층 노드 개수 16개->세 번째 은닉층 노드개수 8개->출력층 노드개수 3개

## 네트워크의 Width너비와 깊이Depth
Baseline model=완성한 적당한 연산량을 가진, 적당한 정확도의 딥러닝 모델

ex) 입력층 4 첫번째 은닉층 8 두 번째 은닉층 4 출력층 1

이것의 성능은 어떻게 테스트 하냐?

**1)네트워크의 너비를 늘리는 방법**

=네트워크의 은닉층의 개수를 그대로 두고 은닉층의 노드 개수를 늘리는 방법

ex) 입력층 4 첫번째 은닉층 8x2=16 두 번째 은닉층 4x2=8 출력층 1

**2)네트워크의 깊이를 늘리는 방법**

=네트워크의 은닉층의 개수를 늘리는 방법

ex) 입력층 4 첫번째 은닉층 8 두 번째 은닉층 8 세 번째 은닉층 8 네 번째 은닉층 8 출력층 1

**3)너비와 깊이를 전부 늘리는 방법 1번과 2번 합친거**

ex) 입력층 4 첫번째 은닉층 8 두 번째 은닉층 16 세 번째 은닉층 16 네 번째 은닉층 8 출력층 1


## 딥러닝에서 사용되는 용어
★Batch size 배치 사이즈

-데이터셋을 작은 단위로 쪼개서 학습을 시키는데 쪼개는 단위를 배치(Batch)

-1,000만개의 데이터셋을 1,000개 씩으로 쪼개어 10,000번을 반복 과정을 Iteration(이터레이션)

★에폭 epoch

-1천만개의 데이터셋을 1천개 단위의 배치로 쪼개면, 1만개의 배치가 되고, 이 1만개의 배치를 100에폭을 돈다고 하면 1만 * 100 = 100만번의 이터레이션을 돈다 

-한번의 에폭 과정: 100단위 한번씩 b&w을 조정하게됨
![image](https://user-images.githubusercontent.com/88616282/203535725-05f7e571-9574-4616-8dce-d65f514999ad.png)

★Activation functions (활성화 함수)

![image](https://user-images.githubusercontent.com/88616282/203536433-dcf521bf-bcd9-4ae8-a65f-14d7e95f353f.png)
-뉴런끼리 연결되어 있음. 근데 뉴런은 특정 임계치Threshold를 넘어야지만 신호를 전달하게됨

-활성화 함수는 비선형 함수이다. 
![image](https://user-images.githubusercontent.com/88616282/203536865-35645b67-7d42-490b-af23-0b208f1262a9.png)
![image](https://user-images.githubusercontent.com/88616282/203536898-dcf13937-4064-4f04-b045-707dad8b481f.png)

-보통은 ReLU라는 활성화 함수를 잘 씀. 빠르고, 비용도 적고, 구현 간단
![image](https://user-images.githubusercontent.com/88616282/203537122-c0aadf1d-7184-434c-99c9-ad2ebc2532ee.png)

**선형 회귀보다는 밀도 또는 FC레이어로 쓰게될 것**

★Overfitting, Underfitting (과적합, 과소적합)

![image](https://user-images.githubusercontent.com/88616282/203537348-899b615a-eda7-4d8c-9d9f-299dd629cf34.png)

-모델이 복잡할수록 Test error 올라가(에러가 난다는거) 그래서 최적점 best fit을 정함 

-overfitting ex)한번 보면 외우는 사람. 문제를 이해하는게 아니라 정답을 외워버리는 경우 

-실제에서는 overfitting 사례가 많고 모델을 더 간단하게 만들어야하는 경우가 많음 

## 딥러닝에서 사용되는 스킬

★Data augmentation (데이터 증강기법)

-Overfitting 해결방법 1)데이터 개수를 늘리면 됨 근데 실제로는 어렵기때문에 **원본을 여러 가지 방법으로 복사를 함**

![image](https://user-images.githubusercontent.com/88616282/203538250-d954230b-ee21-4ace-99eb-42053cf6c4b6.png)

★Dropout (드랍아웃)

-마찬가지로 overfitting해결방법. 각 노드들이 이어진 선을 빼서 없애버린다는 의미. 각 배치마다 랜덤한 노드를 끊어버림

![image](https://user-images.githubusercontent.com/88616282/203538894-a2e298b8-884f-49ee-a98b-c63258d8b5bb.png)
![image](https://user-images.githubusercontent.com/88616282/203539040-cb53d86e-41f6-4398-9c95-49d525134886.png)

★Ensemble (앙상블) ~랜덤포레스트

-여러개의 딥러닝 모델을 만들어 각각 학습시킨 후 각각의 모델에서 나온 출력을 기반으로 투표를 하는 방법(실제 투표한다는게 아니라 평균값을 내거나 최고값을 뽑아내기도하고 선택에 따라 달라짐)

![image](https://user-images.githubusercontent.com/88616282/203539200-c1b3861e-1569-496e-8ce3-d984d36dc71a.png)

★Learning rate decay (Learning rate schedules)

-local minimum에 빠르게 도달하고 싶을 때 사용

-global minimum 도달은 어려움(완전 정답이라는 뜻임)

-처음에 lr을 크게했다가 줄이는게 좋은 방법임 

![image](https://user-images.githubusercontent.com/88616282/203539661-f47ab5dd-b9e2-43da-a0a6-3341cd9f0ac0.png)

-에러가 한번씩 팍팍 줄어

![image](https://user-images.githubusercontent.com/88616282/203540125-c5bc6e48-f8ae-462f-9a8d-44537c65e8d3.png)
