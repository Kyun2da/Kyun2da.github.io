---
layout: post
title: "[백준/Python] 1931 회의실 배정"
subtitle: "알고리즘 - 그리디"
date: 2020-08-28 21:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-universe.jpg"
tags:
  - Algorithm
  - 백준
  - 그리디
---

## 1️⃣서론

백준 문제 1931번 `회의실배정` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/1931){:target="\_blank"}

## 2️⃣문제 설명

이 문제는 회의를 겹치지 않게 하면서 회의실을 사용할 수 있는 회의의 최대 개수를 찾는 문제입니다.

## 3️⃣풀이

이 문제는 `그리디(greedy)` 즉, 탐욕법이라고도 불리는 방법을 사용하는 대표적인 문제입니다.  
어떻게 회의를 배치해야 회의를 가장 많이 열 수 있을까요?  
우리가 생각해낼 수 있는 방법은 다음과 같습니다.

1. 회의가 일찍 시작하는 순으로 회의를 배치
2. 회의가 일찍 끝나는 순으로 회의를 배치
3. 회의시간이 짧은 순으로 회의를 배치
4. 다른회의들과 적게 겹치는 순으로 회의를 배치

이중 정답은 `2번 : 회의가 일찍 끝나는 순으로 회의를 배치`하는 것 입니다.
이는 귀류법으로 증명할 수 있습니다.
귀류법은 어떤 가정이 옳지않다고 가정하고 그 반례를 찾는 방법입니다.
2번 말고 1, 3, 4 번은 모두 반례가 존재함을 생각해보면 알 수 있습니다.

그리고 2번에대해 생각을 해봅시다.  
현재 t1 시간까지 도달했다고 생각하고, 현재 회의 가능한 회의가 arr[0],arr[1],arr[2],arr[3]이 있고 arr[0]이 가장 일찍 끝나는 회의라고
할 때, arr[0]을 빼고 다른 어떤 arr[N]을 사용해서 스케줄을 만들 었다고 가정하면 arr[N]을 빼고 arr[1]을 대신 사용해도 그 스케줄은 여전히
조건을 만족하고 회의의 수는 동일합니다.  
즉, 끝나는 시간이 가장 이르지 않은 회의를 포함한 최대 스케줄을 만들었을 경우, 회의를 바꿔치기 해서 끝나는 시간이 가장 이른 회의만으로도
최대 스케줄을 만들 수 있으므로 해당 그리디가 성립합니다.

- [증명 참조](https://blog.encrypted.gg/65)

## 4️⃣ 소스코드

```python
import sys

N = int(input())

arr = []
for _ in range(N):
    arr.append(list(map(int,sys.stdin.readline().split())))

arr.sort(key=lambda x: (x[1],x[0]))


ans = 1
tmp = arr[0][1]
for i in range(1,len(arr)):
    if arr[i][0] < tmp: continue
    tmp = arr[i][1]
    ans+=1

print(ans)
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️