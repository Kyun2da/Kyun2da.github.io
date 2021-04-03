---
layout: post
title: '[백준 / Python] 5014 스타트링크'
subtitle: bfs 문제
date: 2021-04-03 15:00:00
author: 'Kyun2da'
header-style: text
tags:
  - 알고리즘
  - bfs
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

백준 문제 5014번 `스타트링크` 문제이며 `파이썬(Python)`으로 해결하였다.

- [출처](https://www.acmicpc.net/problem/5014){:target="\_blank"}

## 2️⃣ 문제 설명

총 F층으로 이루어진 건물이 있고 강호는 S층에 있다.

엘리베이터는 2개가 있는데 u칸단위로 올라갈 수 있는 엘리베이터와 d칸단위로 올라갈 수 있는 엘리베티어 2개가 있다.

강호가 이 엘리베이터를 이용해 s층에서 g층으로 가기위해 눌러야하는 엘리베이터 버튼 수의 최솟값을 입력하는 문제이다.

단, 엘리베이터로 이동할 수 없는 경우에는 "use the stairs"를 출력한다.

## 3️⃣ 풀이

이 문제는 갈 수 있는 방법의 수가 2개의 경로가 존재하고 최소의 이동 횟수를 찾는 문제여서 바로 `bfs`라는 알고리즘을 떠올리게 되었다.

갈 수 있는 경로의 수는 다음과 같이 2가지가 존재한다.

- 현재 경로에서 u칸 위로 엘리베이터를 이동한경우 (단, f층을 넘으면 안되고 이전에 방문한 곳이면 안됨)
- 현재 경로에서 d칸 아래로 엘리베이터를 이동한경우 (단, 1층보다 아래로 갈 수 없고 이전에 방문한 곳이면 안됨)

여기서 이전에 방문한 곳이 되면 안되는 이유는 최소 경로를 찾는 문제이기 때문이다.

또 개인적으로 고민되었던게 어떻게 이동할 수 없는 경우를 찾지? 의 문제였는데 해결법은 `더 이상 갈 곳이 없는데 답을 아직 찾지 못했을 때, 즉 bfs의 큐가 비어있을 때` 마지막에 use the stairs를 출력하도록 하였다.

## 4️⃣ 코드

```python
# f : 총 건물의 층 수
# g : 스타트링크가 있는 곳
# s : 강호가 지금 있는 곳
# u : 위로 u층을 갈 수 있음
# d : 아래로 d층을 갈 수 있음

# s 층에서 g 층으로 가기위해 눌러야하는 최소 버튼 횟수

from collections import deque

f, s, g, u, d = map(int, input().split())

q = deque([s])

vis = [False] * (f + 1)
vis[s] = True
count = 0
while q:
    for _ in range(len(q)):
        cur_pos = q.popleft()

        if cur_pos == g:
            print(count)
            exit()

        if cur_pos + u <= f and not vis[cur_pos + u]:
            q.append(cur_pos + u)
            vis[cur_pos+u] = True
        if cur_pos - d >= 1 and not vis[cur_pos - d]:
            q.append(cur_pos - d)
            vis[cur_pos - d] = True
    count += 1

print("use the stairs")
```

## 5️⃣ 마치며

일반적인 bfs문제 였지만 마지막에 큐가 비어있을때를 어떻게 갈까 고민하다가 exit()를 이용해서 바로 큐를 끝내고 while문을 탈출하면 답을 찾지 못한경우이므로 use the stairs를 출력하도록 하였다.
