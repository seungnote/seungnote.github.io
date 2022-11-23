---
title:  "[Python] 머신러닝_딥러닝" 

categories:
  - Python
tags:
  - [Python,ADP,machine_learing]

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

## 딥러닝에서 사용되는 개념
- 배치 사이즈와 에폭
- 활성화 함수
- 과적합과 과소적합
- 데이터 증강
- 드랍아웃
- 앙상블
- 학습률 조정

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
    - 입력층의 노드 개수 4개
    - 첫 번째 은닉층 노드 개수 8개
    - 두 번째 은닉층 노드 개수 16개
    - 세 번째 은닉층 노드개수 8개
    - 출력층 노드개수 3개


