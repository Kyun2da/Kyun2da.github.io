---
layout: post
title: "[백준/Python] 1644 소수의 연속합"
subtitle: "알고리즘 - 소수의 연속합"
date: 2020-09-27 19:00:00
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

백준 문제 1644번 `소수의 연속합` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/1644){:target="\_blank"}

## 2️⃣ 문제 설명

하나 이상의 연속된 소수의 합으로 나타낼 수 있는 자연수들이 있습니다.

하지만 연속된 소수의 합으로 나타낼 수 없는 자연수들도 있는데, 20이 그 예입니다.

7+13을 계산하면 20이 되기는 하나 7과 13이 연속이 아니기에 적합한 표현이 아닙니다.

또한 한 소수는 반드시 한 번만 덧셈에 사용될 수 있기 때문에, 3+5+5+7과 같은 표현도 적합하지 않다.

자연수가 주어졌을 때, 이 자연수를 연속된 소수의 합으로 나타낼 수 있는 경우의 수를 구하는 문제입니다.

## 3️⃣ 풀이

먼저, `에라토스 테네스의 체`를 통해 소수를 구합니다.

나온 소수를 n까지 sosu 배열에 집어넣습니다.

그 후 `투 포인터`를 이용해 sosu배열을 순회하며 만족하는 부분 합이 몇개 있는지 구합니다.

그럼 소스코드를 보시겠습니다.

## 4️⃣ 소스코드

```python
import math

n = 4_000_000
arr = [True for _ in range(n + 1)]

# 에라토스테네스의 체
for i in range(2, int(math.sqrt(n)) + 1):
    if arr[i]:
        j = 2
        while i * j <= n:
            arr[i * j] = False
            j += 1

k = int(input())
if k == 1:
    print(0)
    exit()

sosu = []
for i in range(2, k + 1):
    if arr[i]:
        sosu.append(i)

ans = 0
end = 0
sumA = sosu[0]
length = len(sosu)
# 투 포인터로 소수 배열을 순회하며 부분합 개수를 구한다.
for start in sosu:
    while sumA < k and end < length:
        end += 1
        if end == length:
            break
        sumA += sosu[end]
    if sumA == k:
        ans += 1
    sumA -= start

print(ans)
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
