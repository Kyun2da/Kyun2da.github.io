---
layout: post
title: "[백준/Python] 11054 가장 긴 바이토닉 부분 수열"
subtitle: "알고리즘 - 가장 긴 바이토닉 부분 수열"
date: 2020-09-22 17:00:00
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

백준 문제 11054번 `가장 긴 바이토닉 부분 수열` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/11054){:target="\_blank"}

## 2️⃣ 문제 설명

수열 S가 어떤 수 $S_{k}$를 기준으로 $S_{1} < S_{2} < ... S_{k-1} < S_{k} > S_{k+1} > ... S_{N-1} > S_{N}$을 만족한다면, 그 수열을 바이토닉 수열이라고 합니다.

주어진 수열에서 가장 긴 바이토닉 수열의 길이를 출력하는 문제입니다.

## 3️⃣ 풀이

[가장 긴 증가하는 수열](http://kyun2da.github.io/2020/09/23/longestIncreasingSubsequence4/){:target="\_blank"}을 아직 풀지 않으셨다면 먼저 풀거나 제 블로그를 한번 보고 오시는 것을 추천 드립니다.

이 문제는 가장 긴 증가하는 수열을 왼쪽으로 한번, 오른쪽으로 한번 구해 두개를 더한 것이 가장 큰 수가 나오는 곳이 가장 긴
바이토닉 수열이라고 할 수 있습니다.

그럼 소스코드를 보시겠습니다.

## 4️⃣ 소스코드

```python
import sys

N = int(sys.stdin.readline())
arr = list(map(int, sys.stdin.readline().split()))

ldp = [1 for _ in range(N)]
rdp = [1 for _ in range(N)]

# 왼쪽으로 돌면서 가장 긴 증가하는 부분수열의 길이를 구한다.
for i in range(1, len(arr)):
    for j in range(i):
        if arr[i] > arr[j]:
            ldp[i] = max(ldp[i], ldp[j] + 1)

# 오른쪽으로 돌면서 가장 긴 증가하는 부분수열의 길이를 구한다.
for i in range(len(arr) - 2, -1, -1):
    for j in range(len(arr) - 1, i, -1):
        if arr[i] > arr[j]:
            rdp[i] = max(rdp[i], rdp[j] + 1)

# 왼쪽과 오른쪽 두개를 더한 것중 max 값을 구한다.
ans = 0
for i in range(N):
    tmp = ldp[i] + rdp[i] - 1
    if ans < tmp:
        ans = tmp

print(ans)
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
