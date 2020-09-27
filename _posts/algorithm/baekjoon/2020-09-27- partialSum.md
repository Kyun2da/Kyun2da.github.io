---
layout: post
title: "[백준/Python] 1806 부분합"
subtitle: "알고리즘 - 부분합"
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

백준 문제 1806번 `부분합` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/1806){:target="\_blank"}

## 2️⃣ 문제 설명

10,000 이하의 자연수로 이루어진 길이 N짜리 수열이 주어집니다.

이 수열에서 연속된 수들의 부분합 중에 그 합이 S 이상이 되는 것 중, 가장 짧은 것의 길이를 구하는 문제입니다.

## 3️⃣ 풀이

이 문제는 `투 포인터`를 활용하면 제한 시간내에 해결할 수 있는 문제입니다.

start와 end 포인터의 위치를 초기에 0으로 놓고 두 포인터를 증가시키며 두 포인터 사이의 합이

s보다 크거나 같은 최소의 포인터 사이의 길이를 구하면 됩니다.

그럼 소스코드 보시겠습니다.

## 4️⃣ 소스코드

```python
n, s = map(int, input().split())

arr = list(map(int, input().split()))

end = 0
# 초기의 합을 arr[0]으로 해준다.
intervalSum = arr[0]
ans = float('inf')

# 투 포인터 돌리면서 가장 최소의 길이 구하기
for start in range(n):
    while intervalSum < s and end < n:
        end += 1
        if end == n:
            break
        intervalSum += arr[end]
    if intervalSum >= s:
        ans = min(ans, end - start + 1)
    intervalSum -= arr[start]

if ans == float('inf'):
    print(0)
else:
    print(ans)
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
