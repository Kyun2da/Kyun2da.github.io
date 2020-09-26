---
layout: post
title: "[백준/Python] 14391 종이 조각"
subtitle: "알고리즘 - 종이 조각"
date: 2020-09-26 18:00:00
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

백준 문제 14391번 `종이 조각` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/14391){:target="\_blank"}

## 2️⃣ 문제 설명

첫째 줄에 종이 조각의 세로 크기 N과 가로 크기 M이 주어집니다. (1 ≤ N, M ≤ 4)

둘째 줄부터 종이 조각이 주어집니다. 각 칸에 쓰여 있는 숫자는 0부터 9까지 중 하나입니다.

종이를 적절히 잘라 영선이가 얻을 수 있는 점수의 최댓값을 출력하는 문제입니다.

## 3️⃣ 풀이

제가 아직 비트마스크를 몰라 인터넷 서치를 통해 문제를 해결하였습니다..

그래서 블로그를 통해 정리하며 최대한 설명하여 이해해보도록 하려고 합니다.

`종이는 각 칸마다 가로로 자르기 혹은 세로로 자르기 두가지의 상태가 존재`합니다.

그러므로 각 칸마다 두가지의 상태가 존재하므로, 경우의 수는 $2^{n \times m}$ 가지 입니다.

또한 해당 배열을 일렬로 늘여 이진수로 표현하면 모든 가짓수를 `0부터 n*m -1 까지 검사`해보면 답을 알 수 있습니다.

그렇게 모든 경우를 검사하고 나온 최댓값을 출력하면 됩니다.

그럼 소스코드 보시겠습니다.

## 4️⃣ 소스코드

```python
def bitmask():
    global maxAns
    # 비트마스크로 2^(N*M)의 경우의 수를 따져본다
    for i in range(1 << n * m):
        total = 0
        # 가로 합 계산
        for row in range(n):
            rowsum = 0
            for col in range(m):
                # idx 는 이차원 배열을 일렬로 늘렸을때의 인덱스가 어디인지 의미
                idx = row * m + col
                # 가로일때
                if i & (1 << idx) != 0:
                    rowsum = rowsum * 10 + arr[row][col]
                # 세로일때 앞에서 나온 수를 total에 더하고 rowsum 초기화
                else:
                    total += rowsum
                    rowsum = 0
            total += rowsum

        # 세로 합 계산
        for col in range(m):
            colsum = 0
            for row in range(n):
                # idx 는 이차원 배열을 일렬로 늘렸을때의 인덱스가 어디인지 의미
                idx = row * m + col
                # 세로일때
                if i & (1 << idx) == 0:
                    colsum = colsum * 10 + arr[row][col]
                # 가로일때 앞에서 나온 수를 total에 더하고 colsum 초기화
                else:
                    total += colsum
                    colsum = 0
            total += colsum
        maxAns = max(maxAns, total)


n, m = map(int, input().split())

arr = [list(map(int, input())) for _ in range(n)]

maxAns = 0
bitmask()
print(maxAns)

```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
