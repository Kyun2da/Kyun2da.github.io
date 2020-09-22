---
layout: post
title: "[백준/Python] 2206 벽 부수고 이동하기"
subtitle: "알고리즘 - 벽 부수고 이동하기"
date: 2020-09-22 15:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-universe.jpg"
tags:
  - Algorithm
  - 백준
  - DFS/BFS
mathjax: true
---

## 1️⃣ 서론

백준 문제 2206번 `벽 부수고 이동하기` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/2206){:target="\_blank"}

## 2️⃣ 문제 설명

벽을 한개까지 부술 수 있을 때, 최단 경로를 구하는 문제입니다.

## 3️⃣ 풀이

벽을 부순 횟수가 1이므로 3차원 행렬을 통해 이를 표현할 수 있습니다.

[x][y][0] 칸은 벽을 아직 한번도 부순적이 없을 때의 최단 경로 횟수가 들어있습니다.

반면, [x][y][1] 칸은 벽을 이미 한번 부수고 왔을 때의 최단 경로 입니다.

이렇게 bfs로 다음 행렬을 탐색하며 최단 경로를 탐색하면 됩니다.

그럼 소스코드를 살펴보겠습니다.

## 4️⃣ 소스코드

```python
import sys
from collections import deque


def bfs():
    q.append([0, 0, 0])
    vis[0][0][0] = 1
    while q:
        x, y, z = q.popleft()
        for i in range(4):
            dx = x + dir[i][0]
            dy = y + dir[i][1]
            if 0 <= dx < n and 0 <= dy < m:
                # 아직 방문하지 않았고, 갈 수 있는 경우
                # 벽을 뚫고온 배열이면 벽을 뚫고온 배열에, 아니면 뚫고 오지 않은 배열에 1을더한다.
                if arr[dx][dy] == 0 and vis[dx][dy][z] == -1:
                    vis[dx][dy][z] = vis[x][y][z] + 1
                    q.append([dx, dy, z])
                # 벽을 뚫고오지 않은 배열이고 갈려는 곳에 벽이 있을 때
                elif z == 0 and arr[dx][dy] == 1 and vis[dx][dy][1] == -1:
                    vis[dx][dy][1] = vis[x][y][z] + 1
                    q.append([dx, dy, 1])


n, m = map(int, input().split())

arr = []
for _ in range(n):
    arr.append(list(map(int, sys.stdin.readline().rstrip())))

# 방문을 하지 않았다는 표시는 -1로 하고 여기에 최단 경로의 수가 저장이 됩니다.
vis = [[[-1] * 2 for _ in range(m)] for _ in range(n)]
# bfs로 돌 큐 선언
q = deque()
# 방향 탐색을 위한 dir 배열
dir = [[1, 0], [0, 1], [-1, 0], [0, -1]]

bfs()

# ans1은 벽을 한번도 뚫지 않고 왔을 때의 최단경로,
# ans2는 벽을 한번 뚫고 왔을 때의 최단경로가 저장됩니다.
ans1, ans2 = vis[n - 1][m - 1][0], vis[n - 1][m - 1][1]

if ans1 == -1 and ans2 != -1:
    print(ans2)
elif ans1 != -1 and ans2 == -1:
    print(ans1)
else:
    print(min(ans1, ans2))
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
