---
title: "Deep Learning: Understanding and Application of Machine Learning - 3"

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

세 번째 문제는 다음과 같다.

## 문제

다음의 코드에서 입력이 3인 XOR 문제로 변경

* 입력이 3, 출력이 1 -> 여기서 출력은 $$A+B+C$$

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

필자는 다음과 같이 inputLayerSize를 3으로 변경하고, 3개의 입력 값에 따른 1개의 결과 값을 설정해주었다.

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
Y = np.array([[0], [1], [1], [1], [2], [2], [2], [3]])
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

박사님의 첫 질문은 왜 필자가 Y 값을 그렇게 설정했는지였다.

박사님의 질문에 대한 답을 구성하던 중 필자가 실수를 한 것을 뒤늦게서야 알 수 있었다.

사실 필자는 단순히 A+B+C에 대한 산술연산을 진행하였고, 그 결과 값을 Y에 설정하였다.

그런데 과제 파일을 다시 열어서 확인해보니 입력 값에 따른 Y 값이 테이블에 표기되어 있었다.

(문제를 제대로 확인하지 않은 것이다.)

그러나 박사님께서는 실제로 원하는 성능이 나오지 않을 경우에는 필자의 풀이에서처럼 꼭 정답 값을 지정해주지 않아도 괜찮다고 말씀해주셨다.

즉, 필요에 따라서는 이러한 Trick도 유용하게 사용될 수 있다는 사실을 알 수 있었다. (물론 필자는 이러한 Trick을 의도해서 푼 것은 아니고 위에서 말했듯 단순 실수를 한 것이다.)

## 점검

> 그렇다면 테이블에 나와있는 정답 값은 무엇인가?

과제에 제시된 테이블은 다음과 같았다.

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

위 테이블로부터 정답 코드를 다음과 같이 작성할 수 있겠다.

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
Y = np.array([[0], [1], [1], [1], [0], [0], [0], [1]])
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

