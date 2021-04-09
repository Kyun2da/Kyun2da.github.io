---
layout: post
title: '[백준 / Python] 1915 가장 큰 정사각형'
subtitle:
date: 2021-04-09 16:00:00
author: 'Kyun2da'
header-style: text
tags:
  - 알고리즘
  - dp
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

이 문제는 백준 [1915 가장 큰 정사각형](https://www.acmicpc.net/problem/1915) 문제에 대한 풀이이며 `파이썬(Python)`으로 해결하였다.

## 2️⃣ 문제 설명

n×m의 0, 1로 된 배열이 있다. 이 배열에서 1로 된 가장 큰 정사각형의 크기를 구하는 프로그램을 작성하는 문제이다.

## 3️⃣ 풀이

제일 간단하게는 하나의 인덱스를 검사하면서 어디까지 정사각형이 만들어지는지를 확인하는 전체 탐색이 있을 것이다. 하지만 n,m이 1000이기 때문에 ( 1000 x 1000 ) ^ 2번을 수행해야 해서 절대 2초안에 통과할 수 없다고 생각해서 `dp`를 생각해보게 되었다. 먼저 모두 다 1로 채워진 2x2 정사각형을 생각해보면 [i-1][j-1] 칸과 [i-1][j]칸과 [i][j-1]칸중 가장 최소인 것의 +1이 해당 칸이 정사각형 오른쪽 아래 꼭짓점일 때 최대 크기의 정사각형임을 알 수 있다.

3x3 과 4x4 의 정사각형도 생각해보자

그림으로 표현해보면 다음과 같다.

![dp 가장 큰 정사각형](/img/algorithm/dp_biggest_square.png)

이는 dp로 다음과 같은 공식으로 나타낼 수 있다.

```python
dp[i][j] = min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1
```

단, 1번째 행과 1번째 열은 dp 계산에서 그냥 자기 자신의 값을 따르고 해당 arr[i][j]=0 이면 그냥 dp[i][j] 또한 0 인 것이다. 즉 이것을 코드로 표현하면 다음과 같다.

```python
if i==0 or j==0:
  dp[i][j] = arr[i][j]
elif arr[i][j] == 0:
  dp[i][j] = 0
```

이제 이를 합친 코드를 살펴보자.

## 4️⃣ 코드

```python
import sys

input = sys.stdin.readline

n, m = map(int, input().split())

arr = []
dp = [[0] * m for _ in range(n)]

for _ in range(n):
    arr.append(list(map(int, list(input().rstrip()))))

answer = 0
for i in range(n):
    for j in range(m):
        if i == 0 or j == 0:
            dp[i][j] = arr[i][j]
        elif arr[i][j] == 0:
            dp[i][j] = 0
        else:
            dp[i][j] = min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1
        answer = max(dp[i][j], answer)

print(answer * answer)
```

## 5️⃣ 마치며

확실히 dp는 많이 풀어보는게 정답인 것 같다. 느낌적으로 dp 문제같다라는 생각이 들었고 쉽게 접근하여 해결할 수 있었다. 물론 어려운 dp문제를 만나면 아직도 못풀 것 같긴 하다..
