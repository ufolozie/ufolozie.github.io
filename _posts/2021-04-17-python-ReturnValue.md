---
layout: post
title: "[Python] 반환값으로의 튜플"
description: "함수에서 값 한 개 이상 반환하기"
tags: [Python]
---

파이썬 함수에서는 결괏값 여러 개를 쉼표로 구분하여 반환할 수 있다.
```python
def f():
    return True, False
```

```python
x, y = f()
print(x)
print(y)


[실행 결과]
True
False
```

이는 사실상 결괏값을 튜플로 반환하는 방법이다. 위 예제에서는 반환된 튜플이 (True, False)로 되는 셈이다.

이때 결괏값을 튜플로 반환한다는 것은 어떤 의미인가?

<br>

**엄밀하게 말해서 함수는 값 하나만 반환할 수 있지만, 값이 튜플이면 값을 여러 개 반환한 것과 같다**. 예를 들어 두 정수를 나눈 후에 몫과 나머지를 계산하고 싶다면 x / y를 계산하고 x % y를 계산하는 것으로는 부족하다. 이를 계산하는 더 나은 방법은 둘을 동시에 계산하는 것이다.

내장 함수 divmod는 인수 두 개를 받아서 값이 두 개(몫과 나머지)인 튜플을 반환한다. 즉, 결과를 튜플로 저장할 수 있다.

```python
t = divmod(7, 3)
t


[실행 결과]
(2, 1)
```

아니면 튜플 할당문을 사용해 원소들을 따로따로 저장할 수도 있다.

```python
quot, rem = divmod(7, 3)
quot
rem


[실행 결과]
2
1
```

<br>

처음 예제로 다시 돌아가보면, 이렇게 다시 쓸 수 있다.

```python
def f():
    return True, False
```

```python
t = f()
print(t)


[실행 결과]
(True, False) # 튜플로 반환
```

<br>