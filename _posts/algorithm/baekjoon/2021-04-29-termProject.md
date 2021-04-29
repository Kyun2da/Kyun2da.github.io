---
layout: post
title: '[백준 / Python] 9466 텀 프로젝트'
subtitle:
date: 2021-04-29 12:00:00
author: 'Kyun2da'
header-style: text
tags:
  - 알고리즘
  - dfs
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

이 문제는 백준 [9466 텀 프로젝트](https://www.acmicpc.net/problem/9466) 문제에 대한 풀이이며 `파이썬(Python)`으로 해결하였다.

## 2️⃣ 문제 설명

학생들이(s1, s2, ..., sr)이라 할 때, r=1이고 s1이 s1을 선택하는 경우나, s1이 s2를 선택하고, s2가 s3를 선택하고,..., sr-1이 sr을 선택하고, sr이 s1을 선택하는 경우에만 한 팀이 될 수 있다.

어느 프로젝트 팀에도 속하지 않는 학생들의 수를 계산하는 프로그램을 작성 하는 문제이다.

## 3️⃣ 풀이

예를 들어, 한 반에 7명의 학생들이 있다고 가정하고 선택의 결과는 다음과 같다고 가정하자.

| 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| --- | --- | --- | --- | --- | --- | --- |
| 3   | 1   | 3   | 7   | 3   | 4   | 6   |

![그림](/img/algorithm/9466graph.png)

그러면 다음과 같은 그래프로 나타낼 수 있는데 여기서 팀이 될 수 있는 것은 (3)과 (4,6,7) 뿐이다.

즉, `사이클을 형성`하는 것만 팀이 될 수 있다.

따라서 이 `사이클을 형성하는 번호를 제외한 나머지`가 어느 프로젝트 팀에도 속하지 않는 학생들의 수이다.

사이클을 판단하는 방법은 여러가지가 있겠지만 나는 `dfs`를 활용하여 사이클을 판단하였다.

그럼 아래 코드를 살펴보자

## 4️⃣ 코드

```python
import sys

sys.setrecursionlimit(10 ** 7)

input = sys.stdin.readline


def dfs(x):
    global ans
    vis[x] = True
    cycle.append(x)
    num = arr[x]

    if vis[num]:
        if num in cycle:
            ans += cycle[cycle.index(num):]
        return
    else:
        dfs(num)


t = int(input())

for _ in range(t):
    n = int(input())
    arr = [0] + list(map(int, input().split()))
    vis = [False] * (n + 1)
    ans = []

    for i in range(1, n + 1):
        if not vis[i]:
            cycle = []
            dfs(i)

    print(n - len(ans))
```

## 5️⃣ 마치며

코드 상으로 그렇게 큰 어려움은 없었지만 어떻게 해야 프로젝트의 일원이 아닌지를 생각하는 방법에서 `사이클을 떠올리는 게 어려웠던 문제`였다. 처음에는 그래프를 그려서 해야하나 고민 했었는데 사이클 판단은 단순 dfs로도 쉽게 해결할 수 있는 문제였다.
