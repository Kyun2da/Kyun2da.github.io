---
layout: post
title: "[백준/Python] 2225 합분해"
subtitle: "알고리즘 - 합분해"
date: 2020-09-22 18:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-universe.jpg"
tags:
  - Algorithm
  - 백준
  - 다이나믹 프로그래밍
mathjax: true
---

## 1️⃣ 서론

백준 문제 2225번 `합분해` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/2225){:target="\_blank"}

## 2️⃣ 문제 설명

0 부터 N까지의 정수 K개를 더해서 그 합이 N이 되는 경우의 수를 구하는 문제입니다.

한 개의 수를 여러번 쓰는 것도 가능합니다.

## 3️⃣ 풀이

이 문제에 대한 점화식을 생각해내는게 상당히 까다로웠습니다.

0부터 N까지의 정수를 K개를 이용해 N을 만드는 방법은 0부터 N개까지 k-1를 만드는 개수의 합과 같습니다.

즉 점화식을 다음과 같이 표현할 수 있습니다.

$dp[k][n] = \sum_{l=0}^ndp[k-1][n-l]$

|N / k|N = 0| N = 1| N = 2 |
|K = 1| 0 | 1| 2|
|K = 2|00 |01 , 10|02,11,20|
|K = 3|000|001,010,100|002,011,101,020,110,200|

위 표를 보시면 k=2일때 00에 2를 붙이면 002를 만족하고, 01에 1을 붙이면 011을 만족하고, 10에 1을 붙이면 101을 만족합니다.

이를 통해 보았을 때 n=2, k=3 은 (n=0,k=2), (n=1,k=2), (n=2,k=2) 의 합과 같다고 볼 수 있습니다.

이는 다음과 같이 $O(\log{(K*N^2)})$으로 나타낼 수 있습니다.

```python
n, k = map(int,input().split())
mod = 1000000000
dp = [[0]*(n+1) for _ in range(k+1)]
dp[0][0] = 1
for i in range(1, k+1):
    for j in range(n+1):
        for l in range(j+1):
            dp[i][j] += dp[i-1][j-l]
        dp[i][j] %= mod
print(dp[k][n])
```

하지만 복잡도를 O(KN)까지 낮출 수 있는데요

DP[K][n-1] = DP[K-1][0]+DP[K-1][1]]+...+DP[K-1][n-1]

이러한 성질을 이용하면 됩니다.

그럼 최종 소스코드를 보겠습니다.

## 4️⃣ 소스코드

```python
n, k = map(int, input().split())

mod = 1000000000

dp = [[0] * (n + 1) for _ in range(k + 1)]
dp[0][0] = 1

for i in range(1, k + 1):
    for j in range(n + 1):
        dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        dp[i][j] %= mod

print(dp[k][n])
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
