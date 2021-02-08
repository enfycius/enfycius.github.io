---
title: "Python 과제: Differently print contents of Dictionaries in List by conditions"

classes: wide

categories:
  - Python
tags:
  - Programming
  - Python

toc: true
---

# 질문

## 내용

### 문제

딕셔너리와 리스트를 조합하여 다음 코드의 변수 pets처럼 다양한 정보를 축적할 수 있습니다. 

이를 실행결과처럼 출력되도록 빈칸에 반복문과 print() 함수를 조합해 보세요.

```python
# 딕셔너리를 선언합니다.

pets = [
    {"name" : "구름", "age" : 5},
    {"name" : "초코", "age" : 3},
    {"name" : "아지", "age" : 1},
    {"name" : "호랑이", "age" : 1}
]

print("# 우리 동네 애완 동물들")
```

### 실행결과

```shell
# 우리 동네 애완 동물들

구름 5살
초코 3살
아지 1살
호랑이 1살
```

* 단, 숫자와 문자열 사이에 빈칸이 없게 출력하세요.

# 답변

## 내용

먼저 문제에 주어진 pets를 보면, 그 자체는 List인데 내용물로서 Dictionary를 지니고 있음을 알 수 있다.

그래서 필자는 이중 반복문을 이용하여 바깥쪽 반복문은 리스트를 기준으로 안쪽 내용물 즉, 딕셔너리 항목 하나하나에 대해서 순차적으로 접근하는 반복문으로 구성하였고,

안쪽 반복문은 딕셔너리를 기준으로 안쪽 내용물 즉, Key와 Value pairs 하나하나에 대해서 바깥쪽 반복문과 동일한 방식으로 순차적으로 접근하는 반복문으로 구성하였다.

특히 안쪽 반복문 내에서 key 값이 name일 경우와 age일 경우에 대해서 흐름을 분기시켜 그에 따른 적절한 출력이 이뤄지도록 작성하였다.

### 코드

먼저 필자는 한글이 깨질것을 우려하여 아래에 나오는 모든 문자열들이 UTF-8 형식이라는 것을 명시해주는 주석을 삽입하였다.

```python
# -*- coding: utf-8 -*-
```

그 후 pets를 선언하고, 내용물을 삽입하였으며, 적절한 출력문도 구성해주었다.

```python
pets = [
    {"name": "구름", "age": 5},
    {"name": "초코", "age": 3},
    {"name": "아지", "age": 1},
    {"name": "호랑이", "age": 1}
]

print("# 우리 동네 애완 동물들")
```

마지막으로 이 문제의 핵심이 되는 아래 코드를 작성하였다.

```python
for i in pets:
    for key, value in i.items():
        if(key == "name"):
            print("%s" % (value), end=' ')
        else:
            print("%s살" % (value))
```

필자가 위에서 설명한 것처럼 먼저 pets 내의 내용물인 딕셔너리 항목 하나하나에 대해서 접근하는 반복문은 바깥쪽 반복문이다.

즉, 다음 구문이다.

```python
for i in pets:
```

그 후 i에 들어간 값(List인 pets의 내용물)의 자료형이 dictionary이므로, Key와 Value 쌍들(pairs)을 리턴해주는 items() 함수를 호출하여

이 값들을 각각 변수 key와 value에 담았다.

즉, 이러한 설명은 다음의 구문으로 확인할 수 있다.

```python
for key, value in i.items():
```

이렇게 함으로써 key 값이 name일 경우와 age일 경우에 흐름을 분기시킬 수 있는데

이 역시 코드로 보이면 다음과 같다.

```python
if(key == "name"):      # key값이 name이면 아래 구문 실행
    print("%s" % (value), end=' ')
else:                   # key값이 name이 아니면(즉, 이 경우에는 age이면) 아래 구문 실행
    print("%s살" % (value))         
```

#### 전체 코드

전체 코드를 보이면 다음과 같다.

```python
# -*- coding: utf-8 -*-
pets = [
    {"name": "구름", "age": 5},
    {"name": "초코", "age": 3},
    {"name": "아지", "age": 1},
    {"name": "호랑이", "age": 1}
]

print("# 우리 동네 애완 동물들")

for i in pets:
    for key, value in i.items():
        if(key == "name"):
            print("%s" % (value), end=' ')
        else:
            print("%s살" % (value))
```
