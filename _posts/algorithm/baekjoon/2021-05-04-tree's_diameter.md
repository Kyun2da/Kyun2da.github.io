---
layout: post
title: '[백준 / Python] 1967 트리의 지름'
subtitle: 알고리즘 - 트리의 지름
date: 2021-05-04 14:00:00
author: 'Kyun2da'
header-img: 'img/post-bg-universe.jpg'
tags:
  - 알고리즘
  - 그래프
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

이 문제는 백준 [1967 트리의 지름](https://www.acmicpc.net/problem/1967) 문제에 대한 풀이이며 `파이썬(Python)`으로 해결하였다.

## 2️⃣ 문제 설명

트리(tree)는 사이클이 없는 무방향 그래프이다. 트리에서는 어떤 두 노드를 선택해도 둘 사이에 경로가 항상 하나만 존재하게 된다. 트리에서 어떤 두 노드를 선택해서 양쪽으로 쫙 당길 때, 가장 길게 늘어나는 경우가 있을 것이다. 이럴 때 트리의 모든 노드들은 이 두 노드를 지름의 끝 점으로 하는 원 안에 들어가게 된다. 이런 두 노드 사이의 경로의 길이를 `트리의 지름`이라고 한다. 이 때 트리의 지름을 구하는 문제이다.

## 3️⃣ 풀이

트리의 지름은 `bfs 두번`을 통하여 간단하게 `O(n)`의 시간복잡도로 구현이 가능하다.

이는 다음과 같은 순서로 진행이 된다.

1. 트리에서 아무 노드나 잡고 그 노드에 대한 가장 먼 노드를 구하고 이 노드를 n1이라고 하자.
2. n1 에대한 가장 먼 노드를 한번 더 구한다. 이 노드를 n2라고 하자.
3. 이제 n1과 n2의 거리가 트리의 지름이 된다.

이 3번에 대한 증명은 [구사과님 블로그](https://koosaga.com/14)에서 확인할 수 있다. 귀류법으로 증명을 하셨다.

이제 위 과정에 대한 코드를 간략하게 설명해보자면 다음과 같다.

1. 입력 받은 인풋으로 트리를 구현한다.
2. 트리에서 루트노드에서 가장 먼 노드를 dfs로 구한다.
3. 2번에서 구한 가장 먼 노드에서 한번 더 가장 먼 노드를 dfs로 구한다.
4. 3번에서 구한 가장 먼 길이가 정답이 된다.

이제 아래 코드를 살펴보자.

## 4️⃣ 코드

```python
import sys

input = sys.stdin.readline
sys.setrecursionlimit(10**9)

n = int(input())
graph = [[] for _ in range(n + 1)]


def dfs(x, wei):
    for i in graph[x]:
        a, b = i
        if distance[a] == -1:
            distance[a] = wei + b
            dfs(a, wei + b)


# 트리 구현
for _ in range(n - 1):
    a, b, c = map(int, input().split())
    graph[a].append([b, c])
    graph[b].append([a, c])

# 1번 노드에서 가장 먼 곳을 찾는다.
distance = [-1] * (n + 1)
distance[1] = 0
dfs(1, 0)

# 위에서 찾은 노드에 대한 가장 먼 노드를 찾는다.
start = distance.index(max(distance))
distance = [-1] * (n + 1)
distance[start] = 0
dfs(start, 0)

print(max(distance))
```

## 5️⃣ 마치며

트리의 지름이라는 문제를 새로 접해서 해결 방법을 찾아볼 수 밖에 없었던 것 같다. 이제라도 알았으니 트리 지름 구하는 방법을 숙지하고 있어야겠다.
