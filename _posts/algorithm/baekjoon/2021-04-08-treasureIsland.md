---
layout: post
title: '[백준 / Python] 2589 보물섬'
subtitle: bfs
date: 2021-04-08 15:00:00
author: 'Kyun2da'
header-style: text
tags:
  - 알고리즘
  - bfs
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

이 문제는 백준 [보물섬](https://www.acmicpc.net/problem/2589) 문제에 대한 풀이이며 `파이썬(Python)`으로 해결하였다.

## 2️⃣ 문제 설명

보물 지도가 주어지고 각 칸은 육지(L)과 바다(W)로 표시되어 있다. 보물은 서로 간에 최단 거리로 이동하는데 있어 가장 긴 시간이 걸리는 육지 두 곳에 묻혀있다. 보물이 묻혀 있는 두 곳 간의 최단 거리로 이동하는 시간을 구하는 문제이다.

## 3️⃣ 풀이

이 문제를 풀기위해서는 두가지를 알아야 한다고 생각했다.

1. 어떤 땅이 보물이 묻혀 있는 곳인지 즉, 어떤 두개의 땅이 가장 멀리 있는지
2. 두 보물이 묻혀 있는 곳의 최단거리를 어떻게 구해야할지

2번째 의문에는 `bfs`로 최단거리를 해결하면 된다고 생각해서 쉽게 접근할 수 있었지만 첫 번째는 어떻게 찾아야할지 고민을 하던 중 `가로와 세로의 크기가 최대 50`이라는 점에 주목하게 되었다.

그래서 `완전 탐색`을 사용하여 육지인 곳을 하나씩 bfs로 돌려서 최대 거리인 곳이 보물인 곳이다라고 결론을 내리고 확인을해 봤더니 python에서는 시간초과가 났지만 pypy3에서는 성공하는 코드를 만들 수 있었다.

코드는 다음과 같다.

## 4️⃣ 코드

```python
import sys
from collections import deque

input = sys.stdin.readline

h, w = map(int, input().split())
arr = [list(map(str, input())) for _ in range(h)]

answer = 0
dx = [-1, 0, 0, 1]
dy = [0, -1, 1, 0]

for i in range(h):
    for j in range(w):
        if arr[i][j] == 'W':
            continue
        vis = [[False] * w for _ in range(h)]
        q = deque()
        q.append([i, j, 0])
        vis[i][j] = True
        while q:
            x, y, value = q.popleft()
            answer = max(answer, value)
            for k in range(4):
                nx = x + dx[k]
                ny = y + dy[k]
                if 0 <= nx < h and 0 <= ny < w and arr[nx][ny] == 'L' and not vis[nx][ny]:
                    q.append([nx, ny, value + 1])
                    vis[nx][ny] = True

print(answer)
```

## 5️⃣ 마치며

좀더 최적화하면 python 으로 돌아가는 코드도 만들 수 있을 것 같다. 항상 완전탐색을 먼저 생각해보는 생각이 이번에 운좋게 적중하지 않았나 싶다.
