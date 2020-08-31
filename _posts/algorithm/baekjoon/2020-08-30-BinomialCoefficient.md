---
layout: post
title: "[백준/Python] 11401 이항 계수 3"
subtitle: "알고리즘 - 이항 계수 3"
date: 2020-08-30 01:00:00
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

백준 문제 11401번 `이항 계수 3` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/11401){:target="\_blank"}

## 2️⃣문제 설명

이 문제는 이항계수를 구하는 문제입니다. 단, N의 범위가 4,000,000이하라서 일반적인 공식으로는 풀 수 없었습니다.

## 3️⃣풀이

이 문제는 `페르마의 소정리`를 활용한 코드, `확장 유클리드 호제법`의 두가지 방식으로 풀 수 있습니다.

여기서는 페르마의 소정리방법을 사용해서 문제를 풀어보도록 하겠습니다.

페르마의 소정리는 다음과 같습니다.

$
p가\,소수이고\,a가\,p의\,배수가\,아니면, a^{p-1} \equiv 1(mod p)\,이다.
\,즉, {a}^{p-1}을\,p로\,나눈\,나머지는\,1이다.
$

한 마디로 임의의 소수 p와 서로소인 한 수의(p - 1)승을 p 로 나눈 나머지는 무조건 1이라는 정리입니다.

예를 들면 $64^{70}$을 71로 나눈 나머지는 1이라는 것을 순식간에 알 수 있습니다.

이를 활용한 방법은 제가 설명하는 것 보다 더 자세히 나와있는 [링크](https://www.acmicpc.net/board/view/15795){:target="\_blank"}를 참조해주세요.

이를 구현한 코드를 확인해보도록 하겠습니다.

## 4️⃣ 소스코드

```python
# 페르마의 소정리 이용

# 분할 정복을 이용하여 a^b를 구한다.
def power(a, b):
    if b == 0:
        return 1
    if b % 2:  # 홀수이면
        return (power(a, b // 2) ** 2 * a) % p
    else:
        return (power(a, b // 2) ** 2) % p


p = 1000000007
N, K = map(int, input().split())

# nCk를 나타내기 위해 팩토리얼을 dp로 구해줍니다.
fact = [1 for _ in range(N + 1)]

for i in range(2, N + 1):
    fact[i] = fact[i - 1] * i % p

# A는 nCk의 분자가되고 B는 분모가 됩니다.
A = fact[N]
B = (fact[N - K] * fact[K]) % p

#여기서 페르마의 소정리가 사용됨
print((A % p) * (power(B, p - 2) % p) % p)

```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
