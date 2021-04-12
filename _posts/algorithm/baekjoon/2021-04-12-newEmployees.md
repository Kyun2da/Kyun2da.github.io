---
layout: post
title: '[백준 / Python] 1946 신입 사원'
subtitle: 정렬
date: 2021-04-12 16:00:00
author: 'Kyun2da'
header-style: text
tags:
  - 알고리즘
  - 정렬
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

이 문제는 백준 [1946 신입 사원](https://www.acmicpc.net/problem/1946) 문제에 대한 풀이이며 `파이썬(Python)`으로 해결하였다.

## 2️⃣ 문제 설명

진영 주식회사는 신입사원을 뽑는다. 어떤 지원자 A의 성적이 다른 어떤 지원자 B의 성적에 비해 서류 심사 결과와 면접 성적이 모두 떨어진다면 결코 A는 선발되지 않는다. 이러한 조건을 만족시켜 신입 사원을 선발할 때, 뽑을 수 있는 최대 신입 사원수를 구하는 문제이다.

## 3️⃣ 풀이

정렬 문제라는 것은 바로 알았지만 어떻게 해야 시간을 최대로 줄일 수 있을지를 고민했던 문제였던것 같다. 풀이는 다음과 같다. 서류 성적의 순위를 토대로 면접 성적을 정렬한다. 이렇게 되면 면접 성적이 서류 성적으로 정렬이 되었기 때문에 자신의 앞의 사람이 서류 성적이 더 높은 것을 알 수 있다. `따라서 신입 사원 조건을 만족하려면 앞의 모든 사람들보다 면접 성적은 우수해야 한다.` 이것을 코드로 구현하였다. 구글링 결과 하나의 배열을 다른 배열의 원소 순서로 정렬하는 숏코드를 찾을 수 있어서 이를 코드에 활용했다.

## 4️⃣ 코드

```python
import sys

input = sys.stdin.readline

t = int(input())

for _ in range(t):
    n = int(input())
    doc_score = []
    interview_score = []

    for i in range(n):
        a, b = map(int, input().split())
        doc_score.append(a)
        interview_score.append(b)

    # 면접 성적을 서류 성적 기준으로 정렬한다.
    interview_score = [x for _, x in sorted(zip(interview_score, doc_score))]

    # 앞의 가장 우수 순위를 저장한채 순회하며 조건을 만족하는 신입 사원을 찾는다.
    min_rank = 1e9
    ans = 0
    for x in interview_score:
        if x < min_rank:
            min_rank = x
            ans += 1
    print(ans)
```

## 5️⃣ 마치며

정렬 문제였는데 정렬된 두개의 배열을 활용한다는 것이 익숙하지 않아서 나름 고전했던 것 같다. 그리고 확실히 파이썬이 숏코딩에 최적화 된 언어라는 것을 느낀다. 좀 더 익숙해지도록 하자.

- 배열을 다른 하나의 배열로 정렬하기

```python
[x for _, x in sorted(zip(Y, X))] # Y의 배열로 X를 정렬한다.
```
