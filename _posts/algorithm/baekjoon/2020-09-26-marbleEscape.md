---
layout: post
title: "[백준/Python] 13460 구슬 탈출 2"
subtitle: "알고리즘 - 구슬 탈출 2"
date: 2020-09-26 19:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-universe.jpg"
tags:
  - Algorithm
  - 백준
  - 브루트 포스
mathjax: true
---

## 1️⃣ 서론

백준 문제 13460번 `구슬 탈출 2` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/13460){:target="\_blank"}

## 2️⃣ 문제 설명

구슬 탈출은 직사각형 보드에 빨간 구슬과 파란 구슬을 하나씩 넣은 다음, 빨간 구슬을 구멍을 통해 빼내는 게임입니다.

게임의 목표는 빨간 구슬을 구멍을 통해서 빼내는 것입니다.

이때, 파란 구슬이 먼저 구멍에 들어가면 안 됩니다.

왼쪽으로 기울이기, 오른쪽으로 기울이기, 위쪽으로 기울이기, 아래쪽으로 기울이기와 같은 네 가지 동작이 가능합니다.

빨간 구슬과 파란 구슬은 동시에 같은 칸에 있을 수 없습니다. 또, 빨간 구슬과 파란 구슬의 크기는 한 칸을 모두 차지합니다.

보드의 상태가 주어졌을 때, 최소 몇 번 만에 빨간 구슬을 구멍을 통해 빼낼 수 있는지 구하는 문제입니다.

## 3️⃣ 풀이

bfs로 빨간 구슬과 파란구슬을 이동시키며 몇번만에 빨간 구슬을 이동시킬 수 있는지 확인하면 되는 문제입니다.

하지만 여기서 빨간 구슬과 파란 구슬이 겹칠때 어떤 구슬을 먼저 오게 해주느냐를 결정하는 부분이 상당히 까다로웠습니다.

겹칠 땐 맨 처음에 누가더 가까웠느냐에 따라 더 먼쪽을 한칸 이전으로 이동시킵니다.

이런식으로 큐가 빌때까지 계속 bfs로 탐색을 하면 되는 문제입니다.

그럼 소스코드 보시겠습니다.

## 4️⃣ 소스코드

```python
import sys
from collections import deque

n, m = map(int, input().split())

arr = [list(sys.stdin.readline().rstrip()) for _ in range(n)]
c, q, cnt = [], deque(), 0

dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

# R,B도 갈 수 있는 지점이기 때문에
# R과 B의 인덱스를 저장하고 .으로 변경합니다.
for i in range(n):
    for j in range(m):
        if arr[i][j] == 'R':
            rx, ry = i, j
            arr[i][j] = '.'
        elif arr[i][j] == 'B':
            bx, by = i, j
            arr[i][j] = '.'


def bfs(rx, ry, bx, by, cnt):
    # bfs를 하기위한 q와 갔던 곳인지를 확인하는 c 를 준비합니다.
    q.append([rx, ry, bx, by])
    c.append([rx, ry, bx, by])
    while q:
        lenq = len(q)
        for _ in range(lenq):
            rx, ry, bx, by = q.popleft()
            if arr[rx][ry] == 'O':
                print(cnt)
                return
            for i in range(4):
                nrx, nry, nbx, nby = rx, ry, bx, by
                # #이 나올때까지 빨간색 이동합니다.
                while True:
                    nrx += dx[i]
                    nry += dy[i]
                    if arr[nrx][nry] == 'O':
                        break
                    if arr[nrx][nry] == '#':
                        nrx -= dx[i]
                        nry -= dy[i]
                        break
                # '#'이 나올때까지 파란색 이동합니다.
                while True:
                    nbx += dx[i]
                    nby += dy[i]
                    if arr[nbx][nby] == 'O':
                        break
                    if arr[nbx][nby] == '#':
                        nbx -= dx[i]
                        nby -= dy[i]
                        break

                # 파란색 구슬이 빠진경우 다음 경우의 수를 탐색합니다.
                if arr[nbx][nby] == 'O':
                    continue
                # 빨간색 구슬과 파란색 구슬이 겹치면 서로의 위치를 보고 계산해줌
                if nrx == nbx and nry == nby:
                    if abs(rx - nrx) + abs(ry - nry) > abs(bx - nbx) + abs(by - nby):
                        nrx -= dx[i]
                        nry -= dy[i]
                    else:
                        nbx -= dx[i]
                        nby -= dy[i]

                if [nrx, nry, nbx, nby] not in c:
                    c.append([nrx, nry, nbx, nby])
                    q.append([nrx, nry, nbx, nby])

        if cnt == 10:
            print(-1)
            return
        cnt += 1
    print(-1)
    return


bfs(rx, ry, bx, by, cnt)


```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
