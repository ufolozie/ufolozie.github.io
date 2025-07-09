---
layout: post
title: "[Python] 반복문 정리"
description: "while 문 / for 문 / break 문"
tags: [Python]
---

## **조건 제어 반복문 - while 문**

- 먼저 조건식을 체크하여 참이면 반복할 문장을 실행하고,
다시 조건식을 체크하여 거짓이 될 때까지 계속 반복
- 반복문을 끝내는 조건이 반드시 존재해야 함

```python
i, hap = 0, 0
i = 1
while i < 11:
    hap = hap + i
    i = i + 1
    
print("1에서 10까지의 합:", hap)


[실행 결과]
1에서 10까지의 합: 55
```

여기서 `i = i + 1` 문장이 없다면, i값이 변하지 않아서 조건식(i<11)이 늘 참이기 때문에 while 문을 빠져나오지 못하고 무한 루프에 빠지게 된다.


while, for 반복문에서는 반복문 밖으로 무조건 탈출하기 위해 **break 문**을 사용할 수 있다.

```python
while True:
    inputchar = input("대문자 변환[종료는 q]: ")
    if inputchar == 'q':
        break
    print(inputchar.capitalize())
```

while 문에서 조건식을 `while True:` 와 같이 사용하면 True는 항상 참이기 때문에 무한 반복이 된다. 이때 블록 안에서 특정 조건 아래 break 문이 실행되게 하면 블록의 바깥으로 탈출한다.

<br>

## **횟수 제어 반복문 - for 문**

- 문장을 시작값부터 증가값만큼씩 증가하면서 끝값까지 반복

```python
for 변수 in range(시작값=0, 끝값+1, 증가값=1)
    문장
```

예컨대 range(1, 10)은 1부터 9까지의 값을 나타낸다. 끝값이 10이 아니라 9임에 유의한다.

```python
for i in range(5) # range(0, 5, 1)
    print(i)


[실행 결과]
0
1
2
3
4
```

<br>

### **예제**

```python
import random

number = [] # number 리스트 생성
for num in range(0, 10): # range(0, 9+1, 1). 아래 문장을 0부터 1만큼씩 증가하면서 9번 반복.
    number.append(random.randrange(0, 10)) # 0부터 9 사이의 수 중에서 임의의 수를 정하여 number 리스트 항목에 추가

print("생성된 리스트", number)

for num in range(0, 10):
    if num not in number:
        print(num, "숫자는 리스트에 없네요.")
  

[실행 결과]
생성된 리스트 [6, 5, 5, 4, 9, 5, 2, 7, 1, 4]
0 숫자는 리스트에 없네요.
3 숫자는 리스트에 없네요.
8 숫자는 리스트에 없네요.
```

위 코드는 시작값 0부터 끝값 9까지 증가값 1씩 증가하면서 리스트에 있는지 확인한다.

---

🎁 **Random 모듈**을 `import random` 문장으로 가져오면, random.함수()를 통해 해당 모듈에 존재하는 함수들을 가지고 와서 사용할 수 있다.  
**random()**: 0 이상 1 미만의 숫자 중 임의의 수 반환  
**randrange(a, b)**: a 이상 b 미만의 임의의 정수 반환  
**randrange(b)**: 0 이상 b 미만의 임의의 정수 반환  
**randint(a, b)**: a이상 b 이하의 임의의 정수 반환

---

<br>
