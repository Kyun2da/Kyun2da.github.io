---
layout: post
title: "[백준/Python] 10830 행렬 제곱"
subtitle: "알고리즘 - 행렬 제곱"
date: 2020-08-30 15:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-universe.jpg"
tags:
  - Algorithm
  - 백준
  - 분할 정복
mathjax: true
---

## 1️⃣서론

백준 문제 10830번 `행렬 제곱` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/10830){:target="\_blank"}

## 2️⃣문제 설명

이 문제는 제목 그대로 행렬A를 B제곱한 결과를 구하는 문제입니다.

## 3️⃣풀이

첫 째 줄부터 행렬의 크기 N과 A가 주어집니다.

제곱수 에서 분할정복을 쓸 수 있는 이유는 2의 존재 때문입니다.

만약 $A^{8}$ 이라면 이는 단순히 A를 8번을 곱하는게 아닌 $A^{4} * A^{2} * A^{2}$ 의 식을 통해 더욱 단축시켜 해당 곱을 구할 수 있습니다.

이를 활용한 코드를 보시겠습니다.

## 4️⃣ 소스코드

```python
# 분할 정복을 사용해 행렬의 제곱을 단축시킨다.
def matrixMul(num):
    global N, arr
    if num == 1:
        for i in range(N):
            for j in range(N):
                arr[i][j] %= 1000
        return arr
    elif num % 2 == 1:
        tmp = [[0] * N for _ in range(N)]
        C = matrixMul(num - 1)
        for i in range(N):
            for j in range(N):
                for k in range(N):
                    tmp[i][j] += C[i][k] * arr[k][j]
                tmp[i][j] %= 1000
        return tmp
    else:
        tmp = [[0] * N for _ in range(N)]
        C = matrixMul(num // 2)
        for i in range(N):
            for j in range(N):
                for k in range(N):
                    tmp[i][j] += C[i][k] * C[k][j]
                tmp[i][j] %= 1000
        return tmp


N, A = map(int, input().split())
arr = []
for i in range(N):
    arr.append(list(map(int, input().split())))
res = matrixMul(A)

# 출력
for i in range(N):
    for j in range(N):
        print(res[i][j], end=" ")
    print()

```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
