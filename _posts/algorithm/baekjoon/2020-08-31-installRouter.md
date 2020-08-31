---
layout: post
title: "[백준/Python] 2110 공유기 설치"
subtitle: "알고리즘 - 공유기 설치"
date: 2020-08-31 13:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-universe.jpg"
tags:
  - Algorithm
  - 백준
  - 이분 탐색
mathjax: true
---

## 1️⃣ 서론

백준 문제 2110번 `공유기 설치` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/2110){:target="\_blank"}

## 2️⃣ 문제 설명

이 문제는 집 N개가 있다고 하면, 공유기 C개를 적절하게 가장 짧은 거리가 최대가 되게끔 푸는 문제입니다.

## 3️⃣ 풀이

이 문제는 `이분탐색`으로 해결할 수 있습니다.

바로 `공유기의 가장짧은거리를 탐색`하는 방법입니다.

즉, 거리를 임의로 정해 해당 거리로 공유기 C개를 모두 배치할수 있는지를 검사하며 답이 될 수 있는 가장 큰 거리를 찾는 문제입니다.

소스코드 보겠습니다.

## 4️⃣ 소스코드

```python
import sys

n, c = map(int, input().split())

arr = []
for _ in range(n):
    arr.append(int(sys.stdin.readline()))

# 집의 위치를 오름차순으로 정렬한다.
arr.sort()

# 가장 짧은 거리를 1이라고 하고 가장 큰거리를 첫집과 끝집의 차이라고 가정한다.
start = 1
end = arr[-1] - arr[0]

maxVal = 0
while start <= end:
    mid = (start + end) // 2
    idx, result = 0, 1
    # 집을 순회하며 공유기를 설치할 수 있는지의 여부를 검사한다.
    for i in range(1, len(arr)):
        if arr[idx] + mid <= arr[i]:
            result += 1
            idx = i
    # 만약 공유기를 전부 설치할 수 없다면 거리를 낮춘다.
    if result < c:
        end = mid - 1
    # 공유기를 전부 설치할 수 있다면 거리를 높인다.
    elif result >= c:
        maxVal = mid
        start = mid + 1

print(maxVal)
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
