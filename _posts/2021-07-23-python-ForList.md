---
layout: post
title: "[Python] 반복문을 활용한 리스트 요소 출력"
description: "리스트에서 for 문 사용하기"
tags: [Python]
---

- 리스트 내 각각의 항목을 순서대로 꺼내서 변수에 할당한 후,
  문장을 반복해서 실행
- 모든 항목을 순회할 때까지 반복

```python
for 변수  in 리스트:
    문장
```

```python
four_seasons = ['spring', 'summer', 'fall', 'winter']
for season in four_seasons:
    print(season)  


[실행 결과]
spring
summer
fall
winter
```

<br>