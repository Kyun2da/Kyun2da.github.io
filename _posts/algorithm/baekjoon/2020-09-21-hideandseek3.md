---
layout: post
title: "[백준/Python] 13549 숨바꼭질 3"
subtitle: "알고리즘 - 숨바꼭질 3"
date: 2020-09-21 21:30:00
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

백준 문제 13549번 `숨바꼭질 3` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/13549){:target="\_blank"}

## 2️⃣ 문제 설명

수빈이가 N 위치에 있고, 동생이 K위치에 있을 때, 수빈이가 동생의 위치까지 가는 최소의 시간을 구하는 문제입니다.

수빈이는 다음 3가지의 행동을 취할 수 있습니다.

1. 1초 후에 X-1 로 이동한다.
2. 1초 후에 X+1 로 이동한다.
3. 0초 후에 X\*2 로 이동한다.

## 3️⃣ 풀이

이 문제는 `bfs` 를 활용하여 문제를 해결할 수 있습니다.

가장 중요한 점이 `0초 후에 X*2로 이동하는 것을 어떻게 구현하느냐`의 문제였습니다.

방법은 수빈이가 k초에 있는 지점에서 200,000전까지 k\*2를 전부 방문처리한 후,

큐의 맨 앞에 넣는 것입니다. 그렇게 하면 k초에해당하는 지점을 전부 방문할 수 있습니다.

이를 구현한 소스코드를 보시겠습니다.

## 4️⃣ 소스코드

```python
import sys
from collections import deque

n, k = map(int, input().split())

q = deque()
vis = [-1] * 200001
q.append(n)
vis[n] = 0

while q:
    x = q.popleft()
    if x == k:
        print(vis[x])
        sys.exit()
    # 순간이동해서 갈수 있는곳을 구한다.
    if x * 2 <= 200000 and vis[x * 2] == -1:
        vis[x * 2] = vis[x]
        # appendleft를 통해 큐의 앞에 넣어 해당 초에 방문할 수 있도록 한다.
        q.appendleft(x * 2)
    # x-1 로 갈수 있는곳 1초 더한다.
    if x - 1 >= 0 and vis[x - 1] == -1:
        vis[x - 1] = vis[x] + 1
        q.append(x - 1)
    # x+1 로 갈 수 있는곳 1초 더한다.
    if x + 1 <= 200000 and vis[x + 1] == -1:
        vis[x + 1] = vis[x] + 1
        q.append(x + 1)
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
