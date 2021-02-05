---
title: "Python 과제: 은행 문제"

classes: wide

categories:
  - Python
tags:
  - Programming
  - Python
---

# 질문

## 내용

### 실습

#### 은행의 계좌 정보를 표현하는 Account 클래스와 이 클래스를 활용하는 프로그램
+ 클래스 이름: Account
+ 속성: 
     + (1) 계좌소유주 이름(name): 공개,
     + (2) 계좌번호(accountNum: 000-0000-0000, 총 11자리 숫자와 2개의 '-'): 비공개,
     + (3) 잔고(balance): 비공개
    
+ 메소드:
     + (1) 입금(deposit) 메소드
          + 입력: 입금할 금액, 실행 후: 현재잔고+입금액
     + (2) 출금(withdraw) 메소드
          + 입력: 출금할 금액, 실행 후: 현재잔고-출금액
     + (3) 정보출력(print_accountInfo) 메소드
          + 소유주 이름, 계좌번호, 현재잔고 출력

#### 처리 시나리오

1. 소유주 이름, 계좌번호, 잔고의 입력을 받아 3개의 Account 인스턴스 user1, user2, user3를 생성하고 그 내용을 출력
+ 조건: 계좌번호는 000-0000-0000, 총 11자리 숫자와 2개의 '-'에 맞는 형식인지 검사하고, 틀린 형식이면 맞는 형식으로 입력 받아야 함.

입력 예) 

![ass_py0](https://github.com/enfycius/enfycius.github.io/blob/main/assets/images/python/assignment/ass_py0.png?raw=true)

!! 잘못된 계좌의 입력 예, 계좌번호: 123-4567이면, 다시 입력 요구

2. user1에서 user2로 해당 금액을 이체하는 경우:
+ 이체는 사용자의 잔고에서 이체금액 만큼 출금해서 다른 사용자의 잔고에 입금하면 됨
+ 조건: 이체시, 현재 잔고가 출금할 금액보다 많은지를 확인하고, 현재 잔고가 출금액보다 적은 경우, 출금액을 새로 입력 받아야 함.

# 답변

## 내용

문제에서 제시된 조건들을 모두 만족시키는 코드를 작성하기 전에, 먼저 문제에 주어진 Account 클래스의 속성에 대한 조건을 살펴볼 필요가 있다.

조건은 다음과 같으며,

+ 클래스 이름: Account
+ 속성: 
     + (1) 계좌소유주 이름(name): 공개,
     + (2) 계좌번호(accountNum: 000-0000-0000, 총 11자리 숫자와 2개의 '-'): 비공개,
     + (3) 잔고(balance): 비공개

여기에서 눈여겨 보아야 할 점은, 멤버 변수 name과는 달리  멤버변수 accountNum, balance 등이 공개가 아닌 **비공개**라는 점이다.

이는 **정보 은닉(Information Hiding)**의 개념으로서, 이를 구현하기 위해서는 **접근 제어자(Access Modifier)**에 대한 개념을 사전에 숙지하고 있어야 한다.

그런데 타 언어와는 다르게 Python의 경우에는 별도의 접근 제어자를 사용하고 있지는 않아서 이러한 요구사항을 충족시키기 위해서는 Python만의 **작명법(naming)**을 알고 있어야 한다. :cry::cry:

먼저 **public(공개)**이다.

이것은 클래스의 외부에서도 접근할 수 있으며, 일반적으로 접근 제어자들 중 가장 넓은 범위(scope)를 가진다.

public의 경우에는 별도의 작명법이 존재하지는 않으나, 접미사에 2개 이상의 underscore를 사용하게 되면 public이 된다. 

또한 파이썬에서는 클래스 내의 모든 멤버들에 기본적으로 public을 부여한다.

두 번째는 **private(비공개)**이다.

private의 경우에는 public과는 달리 별도의 작명법이 존재하고 있으며, 다음처럼 접두사로서 두 개의 underscore를 변수 혹은 메소드 앞에 붙여주면 된다.

```python
self.__accountNum
```

```python
def __inFunc(self):
    pass
```

또한 접미사는 밑줄 한 개까지 허용된다.

다음을 살펴보자.

```python
self.__accountNum_
```

```python
def __inFunc_(self):
    pass
```

이 때 접미사를 2개 이상 사용하게 되면 public이 됨에 주의하자.

파이썬은 이것에 대해 타 언어와 대비되는 특징도 지니고 있는데,

접두사로 두 개의 underscore를 가지는 모든 멤버들을 다음으로 변경해서

```python
_object._class__variable
```

클래스의 외부에서도 이에 접근이 가능하다는 점이다.

물론 권고할 만한 사항은 아니므로, 가급적 그러한 사용을 자제하는 것이 좋겠다.

세 번째는 **protected**이다.

protected의 경우에는 private과는 달리 해당 클래스를 상속하는 하위 클래스에서도 접근이 가능하다.

protected의 경우에도 private과 마찬가지로 별도의 작명법이 존재하고 있으며, 다음처럼 접두사로서 한 개의 underscore를 변수 혹은 메소드 앞에 붙여주면 된다.

```python
self._accountNum
```

```python
def _inFunc(self):
    pass
```

이 역시 private과 마찬가지로 접미사로 underscore 1개까지 허용된다.

그러므로 위의 정보들을 종합해보았을 때,

공개 처리된 멤버 변수에는 public의 작명법을,

비공개 처리된 멤버 변수에는 private의 작명법에 따라 작성해주면 된다.

또한 문제에서 이와 관련된 조건이 별도로 주어져 있지는 않으나, 개인적으로 인스턴스를 생성할 때 값들을 전달하여 이를 멤버 변수에 저장하고 싶기 때문에 필자는 생성자(Constructor)를 최대한 이용해보려 한다.

그러므로 필자의 경우에는 Account 클래스의 생성자(Constructor)를 다음과 같이 작성하였다.

```python
class Account:
    def __init__(self, name, accountNum, balance):
        self.name = name
        self.__accountNum = accountNum
        self.__balance = balance
```

위의 코드를 이해하기 위해서는 먼저 **생성자**에 대한 이해와 **self**에 대한 이해가 선행되어야 하지만, 이에 대한 설명을 본 강좌에서 진행한다면 너무 길어져 프로그램의 논리 흐름에 집중하기 어렵기 때문에 이에 대해서는 따로 강좌로 빼내어 설명할 계획이다.

여기까지 속성에 대한 작성을 완료하였다면, 메소드에 대한 조건으로 내려가보자.

메소드에 대한 조건은 다음과 같다.

+ 메소드:
     + (1) 입금(deposit) 메소드
          + 입력: 입금할 금액, 실행 후: 현재잔고+입금액
     + (2) 출금(withdraw) 메소드
          + 입력: 출금할 금액, 실행 후: 현재잔고-출금액
     + (3) 정보출력(print_accountInfo) 메소드
          + 소유주 이름, 계좌번호, 현재잔고 출력

이 역시도 이미 주어진 조건으로 미루어 보아 독자분들께서 충분히 해결할 수 있을 것으로 판단하여 그나마 의미가 있을 법한 withdraw 메소드에 대해서만 설명을 하려 한다.

먼저 필자의 경우에는 withdraw 메소드를 작성하기 위해서 처리 시나리오 하에 있는 다음의 조건도 참고를 해보았는데, 이는 다음과 같다.

2. user1에서 user2로 해당 금액을 이체하는 경우:
+ 이체는 사용자의 잔고에서 이체금액 만큼 출금해서 다른 사용자의 잔고에 입금하면 됨
+ 조건: 이체시, 현재 잔고가 출금할 금액보다 많은지를 확인하고, 현재 잔고가 출금액보다 적은 경우, 출금액을 새로 입력 받아야 함.

이 중 조건 부분만 읽어보면,

> 조건: 이체시, 현재 잔고가 출금할 금액보다 많은지를 확인하고, 현재 잔고가 출금액보다 적은 경우, 출금액을 새로 입력 받아야 함.

이라고 작성이 되어있다.

즉, 현재 잔고가 출금할 금액보다 많은지/많지 않은지를 프로그램이 판단하게끔 하여 그에 맞는 로직을 실행하게끔 흐름을 분기시켜주면 되겠다.

필자는 이를 withdraw 메소드에서 처리하게끔 로직을 작성하였으며, 잔고가 출금액보다 적은 경우에는 1을 반환하고, 그렇지 않은 경우에는 **현재잔고-출금액**을 수행한 후 0을 반환하게끔 하였다.

즉, 코드는 다음과 같다.

```python
def withdraw(self, amount):
        if(self.__balance < amount):
            return 1
        else:
            self.__balance -= amount
            return 0
```

이렇게 하였을 경우의 장점은 다음과 같이 조건문을 구성할 수 있다는 점이다.

```python
if(~.withdraw(amount)):     # ~ 인스턴스의 amount를 인자로 받는 withdraw 메소드를 호출한 후, 잔고보다 출금액이 더 많다면 아래의 구문 실행
    print("재입력")
else:       # 그렇지 않다면(잔고가 출금액보다 더 많거나 같다면) 아래의 구문 실행
    ~.deposit(amount)
```

그러므로 문제에서 주어진 Account 클래스에 대한 조건들을 이용하여 아래와 같은 코드를 작성할 수 있다.

```python
class Account:
    def __init__(self, name, accountNum, balance):
        self.name = name
        self.__accountNum = accountNum
        self.__balance = balance

    def deposit(self, amount):
        self.__balance += amount
    
    def withdraw(self, amount):
        if(self.__balance < amount):
            return 1
        else:
            self.__balance -= amount
            return 0

    def print_accountInfo(self):
        return "{:>10} {:>10} {:>10}".format(self.name, self.__accountNum, self.__balance)
    
```

여기까지 Account 클래스에 대한 코드는 모두 작성하였다.

지금부터는 이를 이용하여 문제에 명시되어 있는 시나리오를 처리하는 코드를 작성해볼 것이다.

먼저 처리 시나리오 1번은 다음과 같으며,

1. 소유주 이름, 계좌번호, 잔고의 입력을 받아 3개의 Account 인스턴스 user1, user2, user3를 생성하고 그 내용을 출력
+ 조건: 계좌번호는 000-0000-0000, 총 11자리 숫자와 2개의 '-'에 맞는 형식인지 검사하고, 틀린 형식이면 맞는 형식으로 입력 받아야 함.

입력 예) 

![ass_py0](https://github.com/enfycius/enfycius.github.io/blob/main/assets/images/python/assignment/ass_py0.png?raw=true)

!! 잘못된 계좌의 입력 예, 계좌번호: 123-4567이면, 다시 입력 요구

1번 조건에 의하여 기본적으로 반복의 횟수를 3회로 제한하여도 되지만, 잘못된 계좌가 사용자로부터 입력되었을 경우 즉, 마지막 !! 에 명시되어 있는 조건에 대비하여 필자의 경우에는 기본 구성을 무한 Loop로 하였다.

그리하여 기본적으로 큰 틀은 무한반복이며,

```python
while True:     # 무한 반복
```

특정 조건 즉, 정상적으로 3회를 입력하였을 경우에는 이를 탈출하게끔 구성하였다.

```python
i = 0   # 정상적으로 입력한 횟수를 담는 변수

while True:
    if(i == 3):     # 그 값이 3이라면(3회 모두 올바르게 입력하였다면)
        break       # 탈출
```

또한, 계좌의 형식이 올바른 경우에는 인스턴스를 생성하여 곧바로 List 자료구조에 담기 위해 별도의 List 자료구조도 선언을 하였다.

```python
my_objects = []     # List
```

여기까지가 기본 설정인 셈이고, 지금부터는 올바른 계좌 번호의 형식인지를 따지는 로직을 작성해보자.

먼저 사용자로부터 이름, 계좌번호, 잔고를 입력받기 위해서 적절히 출력문을 구성해준 후 이것들을 각각 변수 name, accountNum, balance에 담아주는 입력문도 작성을 해준다.

```python
i = 0

number_count = 0

my_objects = []

while True:

    if(i == 3):
        break

    print("{:>10} {:>10} {:>10}".format("이름", "계좌번호", "잔고"))
    print("user{}: ".format(i+1), end='')

    name, accountNum, balance = input().split(' ')
```

그 후 accountNum이 숫자로 구성된 11자리의 계좌번호 형식을 만족하는지 검사하는 구문을 작성해주면 되는데, 이때 알아야 할 사실이 한 가지 있다.

바로 input의 반환형이 'str' 이라는 점이다.

즉, 숫자를 입력하여도 문자열로 반환된다는 것이다.

그러므로 accountNum 변수에 들어간 값은 숫자가 아닌 문자열이다.

그리하여 필자는 우선 문자열에 대해 반복문을 구성하였으며, 반복을 진행하면서 문자열의 문자 하나하나가 숫자인지를 판단하는 조건식을 구성하고, 만약 숫자라면 그 숫자의 개수를 count해주는 별도의 변수를 마련하여 이를 처리하였다.

```python
i = 0

number_count = 0        # 계좌 번호의 숫자 갯수를 저장하는 변수

my_objects = []

while True:

    if(i == 3):
        break

    print("{:>10} {:>10} {:>10}".format("이름", "계좌번호", "잔고"))
    print("user{}: ".format(i+1), end='')

    name, accountNum, balance = input().split(' ')

    for k in accountNum:    # accountNum 문자열에 대해서 반복문을 구성한 후
        if(k.isnumeric()):  # isnumeric() 함수를 이용하여 k에 담긴 문자가 숫자인지를 판단한다. 만약 그러하다면 isnumeric() 함수는 True를, 반대의 경우에는 False를 반환하여 해당 조건문의 실행 여부를 결정한다.        
            number_count = number_count + 1     # k가 숫자라면 number_count의 값을 1만큼 증가
```

이렇게 count 해준 number_count의 값이 계좌번호의 숫자의 개수 11과 일치하고, accountNum의 길이가 13과 일치하며, 4번째와 9번째 문자가 '-'로 같다면, Account 클래스의 인스턴스를 생성하여 이를 리스트에 담아주고, i의 값을 1만큼 count 해주었다. 조건을 만족하지 않았을 경우에는 재입력을 요구하였다.

```python
i = 0

number_count = 0

my_objects = []

while True:

    number_count = 0

    if(i == 3):
        break

    print("{:>10} {:>10} {:>10}".format("이름", "계좌번호", "잔고"))
    print("user{}: ".format(i+1), end='')

    name, accountNum, balance = input().split(' ')

    for k in accountNum:
        if(k.isnumeric()):
            number_count = number_count + 1

    if(len(accountNum) == 13 and number_count == 11 and accountNum[3] == '-' and accountNum[8] == '-'):     # accountNum의 길이가 13이고 number_count의 값이 11이며, accountNum[3] 즉, 4번째 문자가 '-'이고, accountNum[8] 즉, 9번째 문자가 '-'이라면,
        my_objects.append(Account(name, accountNum, int(balance)))
        i = i + 1
    else:
        print("재입력")
```

조건문에서 accountNum의 길이가 13이 아닐 경우 단축평가(short circuit)에 의하여 나머지 조건은 검사하지 않으므로, 뒤의 조건 식에서의 값에 대한 인덱스 참조 시 다음 에러가 발생할 걱정은 하지 않아도 되겠다.

```shell
IndexError: list index out of range
```

![ass_py0](https://github.com/enfycius/enfycius.github.io/blob/main/assets/images/python/assignment/ass_py0.png?raw=true)

이렇게 3회 모두 정상적으로 입력을 한 후에는 위의 그림에서와 같이 사용자로부터 입력받은 정보들을 모두 출력하게끔 작성하였다.

또한 이를 위해서는 Account 클래스 내의 멤버 함수 print_accountInfo()를 사전에 작성해놓았으니, 이를 활용하면 되겠다.

즉,

```python
i = 0

number_count = 0

my_objects = []

while True:

    number_count = 0

    if(i == 3):
        break

    print("{:>10} {:>10} {:>10}".format("이름", "계좌번호", "잔고"))
    print("user{}: ".format(i+1), end='')

    name, accountNum, balance = input().split(' ')

    for k in accountNum:
        if(k.isnumeric()):
            number_count = number_count + 1

    if(len(accountNum) == 13 and number_count == 11 and accountNum[3] == '-' and accountNum[8] == '-'):
        my_objects.append(Account(name, accountNum, int(balance)))
        i = i + 1
    else:
        print("재입력")

for b in my_objects:    # List에 저장된 인스턴스들을 순차적으로 b에 담은 후,
    print(b.print_accountInfo())    # 해당 인스턴스의 print_accountInfo() 메소드를 호출한다.    
```

여기까지 완료하였다면, 마지막으로 출금과 입금에 대한 처리를 진행해보자.

두 번째 처리 시나리오는 다음과 같으며,

2. user1에서 user2로 해당 금액을 이체하는 경우:
+ 이체는 사용자의 잔고에서 이체금액 만큼 출금해서 다른 사용자의 잔고에 입금하면 됨
+ 조건: 이체시, 현재 잔고가 출금할 금액보다 많은지를 확인하고, 현재 잔고가 출금액보다 적은 경우, 출금액을 새로 입력 받아야 함.

먼저 위의 처리 시나리오 중 user1에서 user2로 해당 금액을 이체한다는 내용이 있는데, 이로 미루어보아 프로그램 사용자로부터 두 명의 사람을 입력받아 첫 번째에 입력한 사람으로부터 두 번째에 입력한 사람에게 금액을 이체해주면 된다는 것을 알 수 있다.

> 그런데 만약에 사용자로부터 입력받은 user1과 user2가 프로그램 상 존재하지 않는 사용자라면?

그래서 이에 대한 처리도 해줘야 한다.

이는 마치 계좌번호를 잘못 입력하였을 경우 다시 입력받게끔 하는것과 비슷한 방식으로 처리를 해주면 되겠다.

즉, 잘못 입력할 경우를 대비하여 무한 반복문으로 구성을 해준 후,

```python
while True:
```

프로그램 상 존재하는 사람을 2회 모두 입력하였을 경우 반복문을 탈출하게끔 구성을 해주면 된다.

2회 처리를 위해 먼저 위에서 사용했었던 변수 i를 0으로 설정한 후, 조건문을 작성해준다.


```python
i = 0

while True:
    if(i == 2):
        break
```

프로그램 사용자로부터 두 사람의 이름을 입력받도록 적절한 출력문을 구성해주고, 첫 번째 입력한 사람의 이름을 담는 변수 name1, 두 번째 입력한 사람의 이름을 담는 변수 name2를 이용하여 input문도 구성을 해준다.

```python
i = 0

while True:

    if(i == 2):
        break

    i = 0

    print("사용자 이름 입력: ", end='')

    name1, name2 = input().split(' ')
```

그 후 위에서 Account의 인스턴스를 담았던 List인 my_objects에서 해당 인스턴스의 인덱스 값과 인스턴스를 순차적으로 idx와 b에 담아 인스턴스 b가 가지고 있는 멤버 변수인 name이 사용자가 입력한 첫 번째 사람의 이름과 같은지 또는 두 번째 사람의 이름과 같은지를 검사한 후, 만약에 그러하다면(같다면) i를 count해주고, 인덱스 값을 담는 별도의 리스트를 마련하여 해당 인스턴스의 인덱스 값을 저장해준다.

순차적으로 인덱스 값과 리스트의 값을 변수에 저장하여 이를 처리하기 위해서는 별도의 처리 없이 다음과 같이 enumerate를 이용하면 된다.

```python
for idx, b in enumerate(my_objects):    # idx에는 인덱스 값이, b에는 List인 my_objects의 값이 저장된다. 
```

이 때, 리스트의 길이는 다음과 같이 2로 제한한다.
(프로그램 사용자로부터 입력받는 사람의 수는 2명이기 때문.)

```python
my_list = [0, 0]
```

위의 내용을 종합하여 다음의 코드를 작성할 수 있다.

```python
i = 0

my_list = [0, 0]

while True:

    if(i == 2):
        break

    print("사용자 이름 입력: ", end='')

    name1, name2 = input().split(' ')

    for idx, b in enumerate(my_objects):
        if(b.name == name1):
            i = i + 1
            my_list[0] = idx
        elif(b.name == name2):
            i = i + 1
            my_list[1] = idx
```

필자는 위의 계좌번호가 잘못 입력되었을 경우의 처리와는 다른 방식으로 i의 값이 2회가 아니었을 경우에는 사용자로부터 처음부터 두 사람을 다시 입력하게끔 로직을 작성하였다.

즉,

```python
i = 0

my_list = [0, 0]

while True:

    if(i == 2):
        break

    i = 0       # 처음부터 다시 입력받아야 하므로 i의 값을 0으로 설정

    print("사용자 이름 입력: ", end='')

    name1, name2 = input().split(' ')

    for idx, b in enumerate(my_objects):
        if(b.name == name1):
            i = i + 1
            my_list[0] = idx
        elif(b.name == name2):
            i = i + 1
            my_list[1] = idx

    if(i != 2):
        print("사용자가 없습니다.")
        print("다시 입력")
        continue    # 아래 구문 실행 없이 다시 반복문의 조건부로 거슬러 올라간다.
```

만약 i가 2라면(즉, 프로그램 사용자가 입력한 사람이 모두 프로그램 상 존재하는 사용자였다면),

프로그램 사용자로부터 출금액을 입력받은 후, 정수 값으로 변환하여 이를 amount라는 출금액을 담는 변수에 저장해준 후,

첫 번째 입력한 사람에게서 사용자로부터 입력받은 출금액을 두 번째 입력한 사람에게 이체해주는 로직을 작성해주면 된다.

이 때 위의 Account 클래스의 withdraw 메소드에 대해 설명했던 바와 같이 출금액이 잔고보다 더 많다면 재입력을, 그렇지 않다면 이체를 해주면 되겠다.

즉,


```python
i = 0

my_list = [0, 0]

while True:

    if(i == 2):     # 이곳에 의하여
        break       # 바깥쪽 반복문도 탈출

    i = 0

    print("사용자 이름 입력: ", end='')

    name1, name2 = input().split(' ')

    for idx, b in enumerate(my_objects):
        if(b.name == name1):
            i = i + 1
            my_list[0] = idx
        elif(b.name == name2):
            i = i + 1
            my_list[1] = idx

    if(i != 2):
        print("사용자가 없습니다.")
        print("다시 입력")
        continue

    while True:
        amount = int(input('출금액: '))

        if(my_objects[my_list[0]].withdraw(amount)):    # my_objects List에서 my_list[0]에 담긴 인덱스값에 해당하는 인스턴스에 대하여 amount를 인자로 받는 withdraw 메소드를 호출한 후, True라면, 즉 잔고보다 출금액이 더 많다면, 
            print("재입력")
        else:       # 그렇지 않다면
            my_objects[my_list[1]].deposit(amount)      # 두 번째 객체에 이체를 해주면 된다.
            break   # 그 후 안쪽 반복문 탈출, 그 후 바깥쪽 반복문으로 거슬러 올라가나
```

> else 구문을 실행할 때는 if문에 의하여 이미 다음 구문이 실행되므로, 첫 번째 사용자로부터 출금이 이루어진 상태다.


```python
my_objects[my_list[0]].withdraw(amount)
```

이제 정말 마지막으로 첫 번째 입력한 사람의 정보와 두 번째 입력한 사람의 정보를 출력해주면 끝이다.

이를 위해 위에서 작성해둔 Account 클래스 내의 print_accountInfo() 메소드를 이용하여 반환 값을 출력만 해주면 된다.


```python
print(my_objects[my_list[0]].print_accountInfo())
print(my_objects[my_list[1]].print_accountInfo())
```

다음은 최종 코드이다.

```python
class Account:
    def __init__(self, name, accountNum, balance):
        self.name = name
        self.__accountNum = accountNum
        self.__balance = balance

    def deposit(self, amount):
        self.__balance += amount

    def withdraw(self, amount):
        if(self.__balance < amount):
            return 1
        else:
            self.__balance -= amount
            return 0

    def print_accountInfo(self):
        return "{:>10} {:>10} {:>10}".format(self.name, self.__accountNum, self.__balance)

i = 0

number_count = 0

my_objects = []

while True:

    number_count = 0

    if(i == 3):
        break

    print("{:>10} {:>10} {:>10}".format("이름", "계좌번호", "잔고"))
    print("user{}: ".format(i+1), end='')

    name, accountNum, balance = input().split(' ')

    for k in accountNum:
        if(k.isnumeric()):
            number_count = number_count + 1

    if(len(accountNum) == 13 and number_count == 11 and accountNum[3] == '-' and accountNum[8] == '-'):
        my_objects.append(Account(name, accountNum, int(balance)))
        i = i + 1
    else:
        print("재입력")

for b in my_objects:
    print(b.print_accountInfo())

i = 0

my_list = [0, 0]

while True:

    if(i == 2):
        break

    i = 0

    print("사용자 이름 입력: ", end='')

    name1, name2 = input().split(' ')

    for idx, b in enumerate(my_objects):
        if(b.name == name1):
            i = i + 1
            my_list[0] = idx
        elif(b.name == name2):
            i = i + 1
            my_list[1] = idx

    if(i != 2):
        print("사용자가 없습니다.")
        print("다시 입력")
        continue

    while True:
        amount = int(input('출금액: '))

        if(my_objects[my_list[0]].withdraw(amount)):
            print("재입력")
        else:
            my_objects[my_list[1]].deposit(amount)
            break

print(my_objects[my_list[0]].print_accountInfo())
print(my_objects[my_list[1]].print_accountInfo())
```