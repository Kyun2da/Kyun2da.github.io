---
layout: post
title: '[백준 / Python] 2146 다리 만들기'
subtitle:
date: 2021-04-22 13:00:00
author: 'Kyun2da'
header-style: text
tags:
  - 알고리즘
  - bfs
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

이 문제는 백준 [2146 다리만들기](https://www.acmicpc.net/problem/2146) 문제에 대한 풀이이며 `파이썬(Python)`으로 해결하였다.

## 2️⃣ 문제 설명

여러 섬으로 이루어진 나라가 있다. 이 나라는 N x N 크기의 이차원 평면상에 존재하고 여러 섬으로 이루어져 있으며, 동서남북으로 육지가 붙어있는 덩어리를 말한다. 0은 바다, 1은 육지를 나타내며, 지도가 주어질 때, 가장 짧은 다리 하나를 놓아 두 대륙을 연결하는 방법을 찾는 문제이다. 즉, 연결할 수 있는 가장 짧은 다리의 길이를 구하면 된다.

## 3️⃣ 풀이

일단 작업을 크게 두가지로 나눌 수 있었다.

1. 섬을 각각 어떻게 구분해 줄 것인지
2. 섬과 섬의 최단 다리를 어떻게 찾을 것인지

1번은 각각의 섬의 숫자를 다르게 나타내기로 했다. 이 때 방법은 `bfs`를 사용하여 섬을 구분하기로 했다.

2번이 좀 고민이 많이 됬는데 섬을 각각 돌면서 다른 섬을 만날 때 까지 바다를 건너며 가장 짧은 길이를 찾기로 하였다. 그럼 그 가장 짧은 길이가 가장 짧은 다리의 길이가 될 것이다. 이 방법 또한 `bfs`를 사용하여 어렵지 않게 해결할 수 있었다.

코드는 다음과 같다.

## 4️⃣ 코드

```python
import sys
from collections import deque

input = sys.stdin.readline

dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]


# 섬을 구분해주는 bfs
def bfs1(i, j):
    global count
    q = deque()
    q.append([i, j])
    vis[i][j] = True
    arr[i][j] = count

    while q:
        x, y = q.popleft()
        for k in range(4):
            nx = x + dx[k]
            ny = y + dy[k]
            if 0 <= nx < n and 0 <= ny < n and arr[nx][ny] == 1 and not vis[nx][ny]:
                vis[nx][ny] = True
                arr[nx][ny] = count
                q.append([nx, ny])

# 바다를 건너며 가장 짧은 거리를 구한다.
def bfs2(z):
    global answer
    dist = [[-1] * n for _ in range(n)] # 거리가 저장될 배열
    q = deque()

    for i in range(n):
        for j in range(n):
            if arr[i][j] == z:
                q.append([i, j])
                dist[i][j] = 0

    while q:
        x, y = q.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            # 갈 수 없는 곳이면 continue
            if nx < 0 or nx >= n or ny < 0 or ny >= n:
                continue
            # 다른 땅을 만나면 기존 답과 비교하여 짧은 거리 선택
            if arr[nx][ny] > 0 and arr[nx][ny] != z:
                answer = min(answer, dist[x][y])
                return
            # 바다를 만나면 dist를 1씩 늘린다.
            if arr[nx][ny] == 0 and dist[nx][ny] == -1:
                dist[nx][ny] = dist[x][y] + 1
                q.append([nx, ny])


n = int(input())

arr = [list(map(int, input().split())) for _ in range(n)]
vis = [[False] * n for _ in range(n)]
count = 1
answer = sys.maxsize

for i in range(n):
    for j in range(n):
        if not vis[i][j] and arr[i][j] == 1:
            bfs1(i, j)
            count += 1

# print(arr)

for i in range(1, count):
    bfs2(i)

print(answer)
```

## 5️⃣ 마치며

bfs를 연달아 두개 쓰는 방법이었는데 처음 보는 유형이어서 아이디어에 대한 생각이 많이 걸렸다. 이럴 때마다 알고리즘은 많이 푸는게 답이다 라는 것을 느끼게 되는 것 같다.
