---
title: "Deep Learning: Understanding and Application of Machine Learning - 5"

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

다섯 번째 문제는 다음과 같다.

## 문제

다음 코드를 학습 데이터가 0과 1이 아닌 0과 1의 근삿값인 경우 (noise가 0.2 이내로 있는 경우)의 코드로 변경

* Ex. (-0.1, 1.1), (0.02, 1.1), ...

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

필자는 문제의 예시 데이터셋을 통하여 특정 범위 내에서 소수점이 있는 실수 값을 랜덤으로 생성해주는 함수만 찾아낼 수 있다면, 본 문제를 쉽게 풀이할 수 있을 것으로 생각하였다.

그래서 인터넷 검색을 진행하였고, 그 결과 다음의 함수를 발견할 수 있었다.

**numpy.random.uniform(low, high, size)**

위 함수에 대한 다음 설명을 참조하자.

> Draw samples from a uniform distribution. Samples are uniformly distributed over the half-open interval $$[\text{low, }\text{high})$$ (includes low, but excludes high). In other words, any value within the given interval is equally likely to be drawn by uniform.

또한, 매개변수들의 설명도 확인해보자.

* low: float, optional; Lower boundary of the output interval. All values generated will be greater than or equal to low. The default value is 0.
* high: float; Upper boundary of the output interval. All values generated will be less than high. The default value is 1.0.
* size: int or tuple of ints, optional; Output shape. If the given shape is, e.g., $$(m, n, k),$$ then $$m * n * k$$ samples are drawn. Default is None, in which case a single value is returned.

마지막으로 다음은 위 함수의 반환에 대한 설명이다.

* out: ndarray; Drawn samples, with shape size.

size의 경우에는 low와 high 값이 scalar인 경우에 별도로 지정하지 않으면, single value가 반환되므로 이러한 사실들을 종합하면, 다음과 같은 코드를 작성할 수 있다.

```python
import numpy as np 

epochs = 3  #Change and see the results
# Layers
inputLayerSize, hiddenLayerSize, outputLayerSize = 2,3,1
#Learning Rate
L = 0.1
#input
X = np.array([[random.uniform(-0.2, 0.2), random.uniform(-0.2, 0.2)], [random.uniform(-0.2, 0.2), random.uniform(0.8, 1.2)], [random.uniform(0.8, 1.2), random.uniform(-0.2, 0.2)], [random.uniform(0.8, 1.2),random.uniform(0.8, 1.2)]])
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