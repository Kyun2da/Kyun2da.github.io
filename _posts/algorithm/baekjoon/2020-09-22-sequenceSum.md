---
layout: post
title: "[백준/Python] 13398 연속합 2"
subtitle: "알고리즘 - 연속합 2"
date: 2020-09-22 17:30:00
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

백준 문제 13398번 `연속합 2` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/13398){:target="\_blank"}

## 2️⃣ 문제 설명

n개의 정수로 이루어진 임의의 수열이 주어집니다.

이중 연속된 몇개의 수를 선택해서 구할 수 있는 합 중 가장 큰 합을 구하려고 합니다.

또한 수열에서 수를 하나 제거할 수 있습니다.

## 3️⃣ 풀이

수를 한번 제거한 경우와 제거하지 않은 경우를 배열로 나눠서 dp를 구할 수 있습니다.

즉, 제거할 횟수가 남아있는 배열은 dp[1]에, 제거를 할 횟수가 남아 있지 않은 배열은 dp[0]에 저장합니다.

그럼 dp[0][i]는 본인을 제거한나머지의 합 dp[1][i-1]과,

이전에 제거된 배열과 본인의 합 중 더 큰 값이 dp[0][i]가 됩니다.

이는 식으로 다음과 같이 표현할 수 있습니다.

```python
dp[0][i] = max(dp[1][i-1], dp[0][i-1]+arr[i])
```

또한 dp[1][i] 는 본인혼자만의 합과 이전의 합중 더 최대인 값을 고르면 됩니다.

이 또한 식으로 다음과 같이 표현할 수 있습니다.

```python
dp[1][i] = max(dp[1][i-1]+arr[i], arr[i])
```

여기서 arr[i]를 max에 포함시키는 이유는 이전의 값들의 합이 -가 될 수 있기 때문입니다.

그럼 소스코드를 보시겠습니다.

## 4️⃣ 소스코드

```python
n = int(input())

arr = list(map(int, input().split()))

dp = [[0] * n for _ in range(2)]

dp[0][0], dp[1][0] = arr[0], arr[0]
for i in range(1, n):
    dp[0][i] = max(dp[1][i - 1], dp[0][i - 1] + arr[i])
    dp[1][i] = max(dp[1][i - 1] + arr[i], arr[i])

maxNum = float('-inf')
for i in range(2):
    for j in range(n):
        if maxNum < dp[i][j]:
            maxNum = dp[i][j]

print(maxNum)

```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
