---
layout: post
title: "[백준/Python] 14002 가장 긴 증가하는 부분 수열 4"
subtitle: "알고리즘 - 가장 긴 증가하는 부분 수열 4"
date: 2020-09-22 16:00:00
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

백준 문제 14002번 `가장 긴 증가하는 부분 수열 4` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/14002){:target="\_blank"}

## 2️⃣ 문제 설명

수열 A가 주어졌을 때, 가장 긴 증가하는 부분 수열을 구하는 프로그램을 작성하는 문제입니다.

## 3️⃣ 풀이

이 문제는 전체탐색으로는 시간이 많이 걸리기 때문에 dp를 사용해야합니다.

dp 를 사용하면 $O(N^2)$ 의 시간복잡도로 해결이 가능합니다.

추가적인 설명은 소스코드를 통해 보시겠습니다.

## 4️⃣ 소스코드

```python
from collections import deque

n = int(input())

arr = list(map(int, input().split()))
dp = [0] * n
v = [0] * n
ans = deque()
maxNum = float('-inf')
maxIdx = 0

# 0부터 n 까지 돌면서 해당 수의 부분 수열 길이를 구합니다.
for i in range(0, n):
    dp[i] = 1
    v[i] = i
    # 자신보다 작은 수의 부분수열 길이가 자신보다 크거나 같으면,
    # 그 수 보다 부분수열의 길이를 1 늘려줍니다.
    # 또한 v라는 배열에는 자신보다 작은 부분수열의 인덱스를 저장해 놓습니다.
    for j in range(0, i):
        if dp[i] < dp[j] + 1 and arr[i] > arr[j]:
            dp[i] = dp[j] + 1
            v[i] = j
    if maxNum < dp[i]:
        maxIdx = i
        maxNum = dp[i]

# 아까 저장해놓은 v배열을 통해 가장 긴 부분수열을 구합니다.
idx = maxIdx
for _ in range(maxNum):
    ans.appendleft(arr[idx])
    idx = v[idx]

print(maxNum)
for x in ans:
    print(x, end=" ")
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
