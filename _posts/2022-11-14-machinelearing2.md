## 논리회귀(Logistic regression) ~sigmoid Function

예시) 대학교 시험 전날 공부한 시간을 보고 Pass(1) Fail(0) 예측

만약에 선형회귀를 사용하면 이상하고 정확도가 낮음.

Logistic Function 곡선형태로 그리니깐 구분이 가능해 계산 자체는 선형 회귀와 똑같지만 출력에 sigmoid를 붙여서 H(x)는 0~1사이 값을 가지게끔함. 

-확률로써 구분을 하게됨

-초록색 선=임계치=Threshold ex)0.5기준으로 통과 확률을 봄 

-필요한거 (1)가설 (2)손실함수(최소화하는게 중요함/cross entropy라는걸 씀)

**수학보다는 개념이 중요**
0일 확률 100% 1일때 확률 0%되게끔 만들어야함

-Keras에서는 binary_crossentropy손실 함수를 씀 

## 다항논리회귀(Multinomial logistic regression)~Softmax Function

예시) 대학교 시험 전날 공부한 시간을 보고 성적 ABCD 예측

**One-hot encoding(0과1)**
컴퓨터 친화적으로 입력해줌. 배열을 0으로 채워줌 

**softmax**

비슷한 가중치를 줘서 모든 값 확률 합했을때 1로 만들어줌.

결과값과 비교해서 차이를 줄여주는걸 cross entropy라고함 

확률분포 함수 그래프로 그림 

라벨이 0,1,2가 됨 

-Keras에서는 categorical_crossentropy손실 함수를 씀 

## 차이점 정리 

**단항 논리 회귀**

(1)sigmoid를 써서, 0or1으로만 나눔

(2)cross entropy 확률분포 그래프 계산해서 최소화 

**다항 논리 회귀**

(1)softmax를 써서

(2)cross entropy 확률분포 그래프 계산해서 최소화 
