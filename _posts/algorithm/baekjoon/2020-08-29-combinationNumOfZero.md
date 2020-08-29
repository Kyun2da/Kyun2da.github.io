---
layout: post
title: "[백준/Python] 2004 조합 0의 개수"
subtitle: "알고리즘 - 수학"
date: 2020-08-29 21:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-universe.jpg"
tags:
  - Algorithm
  - 백준
  - 수학
---

## 1️⃣서론

백준 문제 2004번 `조합 0의 개수` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/2004){:target="\_blank"}

## 2️⃣문제 설명

이 문제는 조합 nCm의 끝자리 0의 개수를 출력하는 문제입니다.

## 3️⃣풀이

먼저 단순하게 nCm의 계산공식을 생각해봅시다. `nCm = n!/((n-m)!*m!)`입니다.

하지만 n과 m의 범위가 <= 2,000,000,000 이라 우리는 이를 팩토리얼을 써서 계산하기엔 너무나 많은 시간이 소요됩니다.

따라서, 다른 식을 생각해내는데 수에 `0이 생기는 경우는 10이 만들어지는 경우`입니다.

그렇다면 10은 언제 만들어질까요? 바로 10은 `2와 5의 곱`으로 만들어집니다.

그렇다면, 우리는 0의 개수가 주어진 수의 **2가 몇번나누어지는지와 5가 몇번 나누어지는지를 구하고 2 와 5의 개수중 더 작은 개수를 선택**하면 됩니다.

그럼 소스코드를 보시겠습니다.

## 4️⃣ 소스코드

```python
# 5가 몇번 나누어지는지를 구한다.
def fiveCount(n):
    answer = 0
    while n != 0:
        n = n // 5
        answer += n
    return answer

# 2가 몇번 나누어지는지를 구한다.
def twoCount(n):
    answer = 0
    while n != 0:
        n = n // 2
        answer += n
    return answer


n, m = map(int, input().split())

if m == 0:
    print(0)

else:
    # 2와 5의 개수를 nCm을 구할 때처럼 구해서 더 작은 개수를 선택한다.
    print(min(twoCount(n) - twoCount(m) - twoCount(n - m), fiveCount(n) - fiveCount(m) - fiveCount(n - m)))

```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
