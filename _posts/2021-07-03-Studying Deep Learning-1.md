---
title: "Deep Learning: Understanding and Application of Machine Learning - 1"

classes: wide

categories:
  - Deep-Learning
tags:
  - Deep Learning

toc: true
---

# Understanding and Application of Machine Learning

6월 중순부터 7월 초까지 3주간 진행된 임수종 박사님의 "기계학습의 이해와 응용" 이라는 강연에 참여하여 필자가 수행한 과제의 내용을 공개하고자 한다.

(본 포스팅은 박사님의 동의를 얻고 작성된 글이다.)

첫 번째 문제는 다음과 같다.

## 문제

다음의 코드에서 학습률과 epoch을 변경하면서 정답이 나오도록 조절

```python
import numpy as np 

epochs = 3  #Change and see the results
# Layers
inputLayerSize, hiddenLayerSize, outputLayerSize = 2,3,1
#Learning Rate
L = 0.1
#input
X = np.array([[0,0], [0,1], [1,0], [1,1]])
#Output
Y = np.array([[0], [1], [1], [0]])
#Activation 
def sigmoid(x): return 1/(1+ np.exp(-x))
# Derivative 
def sigmoid_(x): return x*(1-x)

hidden_Weights = np.random.uniform(size=(inputLayerSize,hiddenLayerSize))
print('----------------Hidden Layer Weights----------------')
print(hidden_Weights)
print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
Output_Weights = np.random.uniform(size=(hiddenLayerSize,outputLayerSize))
print('----------------Output Layer Weights----------------')
print(Output_Weights)
print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
for i in range(epochs):
	Hidden_result = sigmoid(np.dot(X,hidden_Weights))
	print('----------------Hidden Layer Output----------------')
	print(Hidden_result)
	print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
	Output = np.dot(Hidden_result,Output_Weights) 
	print('----------------Output----------------')
	print(Output)
	print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
	Error = Y - Output
	print('----------------Error----------------')
	print(Error)
	print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
	dZ = Error*L
	print('----------------Change in Error----------------')
	print(dZ)
	print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
	Output_Weights +=  Hidden_result.T.dot(dZ)
	print('----------------Change in Output_Weights----------------')
	print(Output_Weights)
	print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')

	dHidden_result = dZ.dot(Output_Weights.T) * sigmoid_(Hidden_result)
	print('----------------Change in Hidden result----------------')
	print(dHidden_result)
	print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
	hidden_Weights +=  X.T.dot(dHidden_result)
	print('----------------Change in Hidden Weights----------------')
	print(hidden_Weights)
	print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
print(Output)
```

## 풀이

필자는 위 문제를 풀이하기 위해서 다음과 같이 단순히 epoch과 학습률을 직접 수동으로 변경하는 방식을 택하지 않고 각각의 값들을 랜덤으로 설정하고 무한 반복문으로 구성하여 Output 값이 정답이 되는 값과의 거리가 0.1 미만일 때 무한 반복문을 탈출하게끔하여 그때의 가중치 값들과 epoch 값 그리고 학습률을 출력하게끔 했다.

```python
import numpy as np 
import random

epochs = random.randrange(0, 10001)  # epochs에 대해 0~10000 사이(경곗값 포함)의 랜덤 값 초기값으로 설정
# Layers
inputLayerSize, hiddenLayerSize, outputLayerSize = 2,3,1
#Learning Rate
L = random.uniform(0, 1)    # Learning Rate에 대해서는 0과 1 사이의 랜덤한 실수 값을 초기값으로 설정
#input
X = np.array([[0,0], [0,1], [1,0], [1,1]])
#Output
Y = np.array([[0], [1], [1], [0]])

Output = np.dot(Hidden_result,Output_Weights) 
#Activation 
def sigmoid(x): return 1/(1+ np.exp(-x))
# Derivative 
def sigmoid_(x): return x*(1-x)

while True:
  epochs = random.randrange(0, 10001)       # epochs에 대해 0~10000 사이(경곗값 포함)의 랜덤 값 설정
  L = random.uniform(0, 1)          # Learning Rate에 대해 0과 1 사이의 랜덤한 실수 값 설정
  hidden_Weights = np.random.uniform(size=(inputLayerSize,hiddenLayerSize))
  print('----------------Hidden Layer Weights----------------')
  print(hidden_Weights)
  print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
  Output_Weights = np.random.uniform(size=(hiddenLayerSize,outputLayerSize))
  print('----------------Output Layer Weights----------------')
  print(Output_Weights)
  print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')

  for i in range(epochs):
    Hidden_result = sigmoid(np.dot(X,hidden_Weights))
    if(np.isnan(Hidden_result[0][0]) or np.isinf(Hidden_result[0][0])):
      break
    print('----------------Hidden Layer Output----------------')
    print(Hidden_result)
    print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
    Output = np.dot(Hidden_result,Output_Weights) 
    print('----------------Output----------------')
    print(Output)
    print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
    Error = Y - Output
    print('----------------Error----------------')
    print(Error)
    print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
    dZ = Error*L
    print('----------------Change in Error----------------')
    print(dZ)
    print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
    Output_Weights +=  Hidden_result.T.dot(dZ)
    print('----------------Change in Output_Weights----------------')
    print(Output_Weights)
    print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')

    dHidden_result = dZ.dot(Output_Weights.T) * sigmoid_(Hidden_result)
    print('----------------Change in Hidden result----------------')
    print(dHidden_result)
    print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
    hidden_Weights +=  X.T.dot(dHidden_result)
    print('----------------Change in Hidden Weights----------------')
    print(hidden_Weights)
    print('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')

  # 정답 값과 Output 값과의 차이가 0.1 미만일 때 무한 반복문 탈출
  if(abs(Output[0][0] - Y[0][0]) < 0.1 and abs(Output[3][0] - Y[3][0]) < 0.1 and abs(Output[1][0] - Y[1][0]) < 0.1 and abs(Output[2][0] - Y[2][0]) < 0.1):
    break

print(hidden_Weights)       # 그때의 hidden_Weights 값 출력  
print(Output_Weights)       # 그때의 Output_Weights 값 출력
print(Output)               # 그때의 Output 값 출력
print(epochs)               # 그때의 epochs 값 출력
print(L)                    # 그때의 Learning Rate 값 출력
```

## 피드백

> 박사님께서는 본인 의도를 뛰어넘는 재미있는 풀이를 진행했다고 말씀하셨으나, 실용성은 많이 떨어진다고 말씀하셨다. 특히, 필자의 코드에 의해서 랜덤하게 도출된 Learning Rate 값의 경우 큰 의미가 없다고 말씀하셨고, 보통은 0.1 단위로 수동으로 조정해야한다고 말씀해주셨다. 또한, epochs 역시 랜덤하게 설정하는 것이 아닌 자신의 서버가 어느정도의 자원과 시간 안에서 학습을 수행할지를 고려하여 그 안에서 최댓값을 고정값으로 해야 한다고도 말씀해주셨다. 마지막으로 학습이라는 것이 Loss를 줄이는 과정이기 때문에 실제로는 Output 값과 Y 값의 차이가 어느 특정 값 안으로 들어와야 하는지 그 특정 값을 조정해야하는 것이라고 말씀하셨다.

결론적으로 윗 내용을 정리해보자면,

* Learning Rate 값의 경우 랜덤하게 설정하지 말고, 0.1 단위로 수동 조정
* Epochs 역시 랜덤 설정 대신 자신의 서버의 자원과 학습에 투여될 시간 및 비용 등을 고려하여 그 안에서 Max 값으로 고정
* Output 값과 Y 값의 차이가 어떤 특정 값 안으로 들어와야 하는지 그 특정 값을 조정
