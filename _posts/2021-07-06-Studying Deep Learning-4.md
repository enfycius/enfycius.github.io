---
title: "Deep Learning: Understanding and Application of Machine Learning - 4"

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

네 번째 문제는 다음과 같다.

## 문제

다음의 코드에서 입력이 3인 XOR 문제로 변경

* 입력이 3, 출력이 2 -> 여기서 첫번째 출력은 $$A+B$$, 두번째 출력은 $$A+B+C$$

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

입력이 3이고 출력이 2이기 때문에 필자는 다음의 코드에서와 같이 inputLayerSize를 3으로 outputLayerSize를 2로 변경하였다.

또한, 입력 값에 따른 출력 값도 지정해주었다.

```python
import numpy as np 

epochs = 3  #Change and see the results
# Layers
inputLayerSize, hiddenLayerSize, outputLayerSize = 3,3,2
#Learning Rate
L = 0.1
#input
X = np.array([[0, 0, 0], [0, 0, 1], [0, 1, 0], [1, 0, 0], [0, 1, 1], [1, 1, 0], [1, 0, 1], [1, 1, 1]])
#Output
Y = np.array([[0, 0], [0, 1], [1, 1], [1, 1], [1, 2], [2, 2], [1, 2], [2, 3]])
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

## 피드백

본 코드 역시 이전 포스팅에서와 같이 필자가 실수하였는데, 어떤 부분에서 실수하였는지는 다음 링크를 통해 확인해보자.

[Reference](https://enfycius.github.io/deep-learning/Studying-Deep-Learning-3/)

## 점검

이전 포스팅에서와 같이 테이블에 명시되어 있었던 정답 값은 다음과 같았다.


| A | B | C | A+B | A+B+C |
|---|---|---|-----|-------|
| 0 | 0 | 0 | 0   | 0     |
| 0 | 0 | 1 | 0   | 1     |
| 0 | 1 | 0 | 1   | 1     |
| 0 | 1 | 1 | 1   | 0     |
| 1 | 0 | 0 | 1   | 1     |
| 1 | 0 | 1 | 1   | 0     |
| 1 | 1 | 0 | 0   | 0     |
| 1 | 1 | 1 | 0   | 1     |

위 테이블로부터 정답 코드를 다음과 같이 수정해볼 수 있겠다.

```python
import numpy as np 

epochs = 3  #Change and see the results
# Layers
inputLayerSize, hiddenLayerSize, outputLayerSize = 3,3,1
#Learning Rate
L = 0.1
#input
X = np.array([[0, 0, 0], [0, 0, 1], [0, 1, 0], [1, 0, 0], [0, 1, 1], [1, 1, 0], [1, 0, 1], [1, 1, 1]])
#Output
Y = np.array([[0, 0], [0, 1], [1, 1], [1, 1], [1, 0], [0, 0], [1, 0], [0, 1]])
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

