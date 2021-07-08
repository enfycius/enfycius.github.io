---
title: "Deep Learning: Understanding and Application of Machine Learning - 6"

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

여섯 번째 문제는 다음과 같다.

## 문제

다음 코드의 (2, 3, 1)인 신경망 구조를 (2, 2, 1)로 변경하여 XOR에 적용시켜라.

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

위 문제는 다음과 같이 단순히 hiddenLayerSize를 2로 변경하면 된다.

```python
import numpy as np 

epochs = 3  #Change and see the results
# Layers
inputLayerSize, hiddenLayerSize, outputLayerSize = 2,2,1
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