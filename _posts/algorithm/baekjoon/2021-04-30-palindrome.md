---
layout: post
title: '[백준 / Python] 10942 팰린드롬'
subtitle:
date: 2021-04-30 16:00:00
author: 'Kyun2da'
header-style: text
tags:
  - 알고리즘
  - dp
mathjax: true
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

이 문제는 백준 [10942 팰린드롬?](https://www.acmicpc.net/problem/10942) 문제에 대한 풀이이며 `파이썬(Python)`으로 해결하였다.

## 2️⃣ 문제 설명

자연수 n개가 있는 배열이 주어지고, 해당하는 구간이 팰린드롬이면 1을 출력하고 팰린드롬이 아니면 0을 출력하는 문제이다.

## 3️⃣ 풀이

처음에 아이디어를 잘 생각해내지 못해서 쉽게 풀지 못했다. 단순히 브루트포스를 사용하기에는 시간복잡도가 너무 높았기 때문에, 다른 아이디어를 찾아야했는데 팰린드롬의 알고리즘에는 크게 `dp`와 `Manacher's 알고리즘`이 있다는 사실을 알게되었다.

dp 는 $O({N^2})$ 이고 Manacher's Algorithm은 O(N)의 시간복잡도로 해결이 가능한데 `이 문제는 dp로도 충분히 해결이 가능`하였다. dp의 해결방법은 다음과 같다.

1. 글자가 1개인 부분 문자열은 무조건 팰린드롬이다.
2. 글자가 2개인 부분 문자열은 2개의 글자가 같다면 팰린드롬이다.
3. 글자가 3개이상이면 시작 문자열과 끝 문자열이 같고 그 사이의 문자열이 팰린드롬이다. 이를 dp 공식화 하면 아래 코드와 같다.

## 4️⃣ 코드

```python
import sys

input = sys.stdin.readline

n = int(input())
arr = list(map(int, input().split()))
dp = [[0] * n for _ in range(n)]

for i in range(n):
    dp[i][i] = 1

for i in range(n - 1):
    if arr[i] == arr[i + 1]:
        dp[i][i + 1] = 1

for i in range(2, n):
    for j in range(n - i):
        if arr[j] == arr[j + i] and dp[j + 1][j + i - 1] == 1:
            dp[j][i + j] = 1

t = int(input())

for _ in range(t):
    a, b = map(int, input().split())
    print(dp[a - 1][b - 1])
```

## 5️⃣ 마치며

팰린드롬 알고리즘이 어떤 것들이 있는지 알게 되었다. 팰린드롬은 좀 특이하지만 잘 출제되는 문제이기도 하니 꼭 구현 방법을 제대로 숙지하고 있어야겠다.
