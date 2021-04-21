---
layout: post
title: '[백준 / Python] 1504 특정한 최단 경로'
subtitle:
date: 2021-04-21 17:00:00
author: 'Kyun2da'
header-style: text
tags:
  - 알고리즘
  - 다익스트라
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

이 문제는 백준 [1504 특정한 최단 경로](https://www.acmicpc.net/problem/1504) 문제에 대한 풀이이며 `파이썬(Python)`으로 해결하였다.

## 2️⃣ 문제 설명

세준이는 1번 정점에서 N번 정점으로 최단 거리로 이동하려고 한다. 또한 임의로 주어진 두 정점은 반드시 통과해야 한다. 주어진 두 정점을 반드시 거치면서 최단 경로로 이동하는 최단 경로의 길이를 구하는 문제이다.

## 3️⃣ 풀이

노드와 노드 사이의 최단 경로를 구할 때는 `다익스트라 알고리즘`을 사용한다. 이 문제에서 시작점, 주어진 정점1, 주어진 정점2, 도착점이 있는데 네 개의 점을 갖고 점의 순서는 시작점과 도착점의 위치가 고정이기 때문에 두 가지 밖에 존재하지 않는다.

1. 시작점 -> 정점1 -> 정점2 -> 도착점
2. 시작점 -> 정점2 -> 정점1 -> 도착점

위의 경로를 다익스트라로 각각 구해서 더 작은 경로의 길이가 이 문제의 답이 된다. 위의 경로를 다익스트라 형태로 표현하면 다음과 같다.

1. 시작점 -> 정점1의 최단경로 + 정점1 -> 정점2의 최단경로 + 정점2 -> 도착점의 최단경로의 길이
2. 시작점 -> 정점2의 최단경로 + 정점1 -> 정점1의 최단경로 + 정점1 -> 도착점의 최단경로의 길이

이를 코드로 표현하면 아래와 같다.

## 4️⃣ 코드

```python
import sys
import heapq

input = sys.stdin.readline
INF = sys.maxsize

n, e = map(int, input().split())

graph = [[] for _ in range(n + 1)]
for _ in range(e):
    a, b, c = map(int, input().split())
    graph[a].append([b, c])
    graph[b].append([a, c])

v1, v2 = map(int, input().split())


def dijkstra(start):
    q = []
    distance = [INF] * (n + 1)
    distance[start] = 0

    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q:
        dist, now = heapq.heappop(q)
        if distance[now] < dist:
            continue
        for i in graph[now]:
            cost = dist + i[1]
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

    return distance


one = dijkstra(1)
v1_distance = dijkstra(v1)
v2_distance = dijkstra(v2)

answer = min(one[v1] + v1_distance[v2] + v2_distance[n], one[v2] + v2_distance[v1] + v1_distance[n])

if answer < INF:
    print(answer)
else:
    print(-1)
```

## 5️⃣ 마치며

다익스트라가 살짝 응용된 문제여서 처음에 어떻게 풀어야 할지 고민을 많이 했는데 노드와 노드사이의 거리를 구하는 것에 힌트를 얻어 아이디어를 쉽게 생각할 수 있었다. 다익스트라 알고리즘만 알고 있었다면 그렇게 어려운 문제는 아니었던 것 같다.
