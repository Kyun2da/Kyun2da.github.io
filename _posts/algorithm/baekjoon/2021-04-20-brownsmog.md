---
layout: post
title: '[백준 / Python] 17144 미세먼지 안녕!'
subtitle:
date: 2021-04-20 17:00:00
author: 'Kyun2da'
header-style: text
tags:
  - 알고리즘
  - 시뮬레이션
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

이 문제는 백준 [17144 미세먼지 안녕!](https://www.acmicpc.net/problem/17144) 문제에 대한 풀이이며 `파이썬(Python)`으로 해결하였다.

## 2️⃣ 문제 설명

R x C 크기의 격자판이 있고 공기 청정기는 항상 1열 어딘가에 위치해 있다. 미세먼지는 다음과 같은 규칙으로 퍼지거나 움직인다.

1초 동안 아래 적힌 일이 순서대로 일어난다.

1. 미세먼지가 확산된다. 확산은 미세먼지가 있는 모든 칸에서 동시에 일어난다.

- (r, c)에 있는 미세먼지는 인접한 네 방향으로 확산된다.
- 인접한 방향에 공기청정기가 있거나, 칸이 없으면 그 방향으로는 확산이 일어나지 않는다.
- 확산되는 양은 Ar,c/5이고 소수점은 버린다.
- (r, c)에 남은 미세먼지의 양은 Ar,c - (Ar,c/5)×(확산된 방향의 개수) 이다.

2. 공기청정기가 작동한다.

- 공기청정기에서는 바람이 나온다.
- 위쪽 공기청정기의 바람은 반시계방향으로 순환하고, 아래쪽 공기청정기의 바람은 시계방향으로 순환한다.
- 바람이 불면 미세먼지가 바람의 방향대로 모두 한 칸씩 이동한다.
- 공기청정기에서 부는 바람은 미세먼지가 없는 바람이고, 공기청정기로 들어간 미세먼지는 모두 정화된다.

## 3️⃣ 풀이

시뮬레이션 문제이다. 미세먼지의 확산과 위쪽 공기청정기 바람의 이동, 아래쪽 공기청정기 바람의 이동 이렇게 세가지의 행동을 나눠서 생각하여 문제를 해결하였다. 미세먼지의 확산은 확산이 완료된 새로운 배열을 하나 만들어 원래의 배열의 남은 먼지배열과 합쳐주어서 쉽게 해결할 수 있었지만 공기청정기의 이동 부분이 많은 고민이 필요하였다. 풀이는 다음과 같다.

## 4️⃣ 코드

```python
import sys

input = sys.stdin.readline

r, c, t = map(int, input().split())

arr = [list(map(int, input().split())) for _ in range(r)]

up = -1
down = -1
# 공기 청정기 위치 찾기
for i in range(r):
    if arr[i][0] == -1:
        up = i
        down = i + 1
        break

# 미세먼지 확산
def spread():
    dx = [-1, 0, 0, 1]
    dy = [0, -1, 1, 0]

    tmp_arr = [[0] * c for _ in range(r)]
    for i in range(r):
        for j in range(c):
            if arr[i][j] != 0 and arr[i][j] != -1:
                tmp = 0
                for k in range(4):
                    nx = dx[k] + i
                    ny = dy[k] + j
                    if 0 <= nx < r and 0 <= ny < c and arr[nx][ny] != -1:
                        tmp_arr[nx][ny] += arr[i][j] // 5
                        tmp += arr[i][j] // 5
                arr[i][j] -= tmp

    for i in range(r):
        for j in range(c):
            arr[i][j] += tmp_arr[i][j]

# 공기청정기 위쪽 이동
def air_up():
    dx = [0, -1, 0, 1]
    dy = [1, 0, -1, 0]
    direct = 0
    before = 0
    x, y = up, 1
    while True:
        nx = x + dx[direct]
        ny = y + dy[direct]
        if x == up and y == 0:
            break
        if nx < 0 or nx >= r or ny < 0 or ny >= c:
            direct += 1
            continue
        arr[x][y], before = before, arr[x][y]
        x = nx
        y = ny

# 공기청정기 아래쪽 이동
def air_down():
    dx = [0, 1, 0, -1]
    dy = [1, 0, -1, 0]
    direct = 0
    before = 0
    x, y = down, 1
    while True:
        nx = x + dx[direct]
        ny = y + dy[direct]
        if x == down and y == 0:
            break
        if nx < 0 or nx >= r or ny < 0 or ny >= c:
            direct += 1
            continue
        arr[x][y], before = before, arr[x][y]
        x = nx
        y = ny


for _ in range(t):
    spread()
    air_up()
    air_down()

answer = 0
for i in range(r):
    for j in range(c):
        if arr[i][j] > 0:
            answer += arr[i][j]

print(answer)
```

## 5️⃣ 마치며

디버깅을 계속 해가며 어느 곳이 잘못 되었는지 체크하면서 가야하는 시뮬레이션 문제가 개인적으로 나는 제일 까다로운 것 같다. 디버깅의 실력이 안좋아서 그런지 아직 많이 미숙한 것 같다. 좀더 시뮬레이션을 많이 풀어서 익숙해지도록 노력해야겠다.
