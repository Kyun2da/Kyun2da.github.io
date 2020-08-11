---
layout: post
title: "[백준/Python] 2579 계단 오르기"
subtitle: "알고리즘 - Dynamic Programming"
date: 2020-08-11 19:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-universe.jpg"
tags:
  - Algorithm
  - 백준
  - Dynamic Programming
---

## 1️⃣서론

백준 문제 2579번 `계단 오르기` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/2579){:target="\_blank"}

## 2️⃣문제 설명

이 문제는 전형적인 DP문제입니다. 근데 풀이 방식을 생각해내는게 어려워서 포스팅하게 되었습니다.  
계단 오르기 게임은 계단 아래 시작점부터 계단 꼭대기에 위치한 도착점까지 가는 게임입니다.  
계단을 오르는데는 다음과 같은 규칙이 있습니다.

1. 계단은 한 번에 한 계단씩 또는 두 계단씩 오를 수 있다. 즉, 한 계단을 밟으면서 이어서 다음 계단이나, 다음 다음 계단으로 오를 수 있다.
2. 연속된 세 개의 계단을 모두 밟아서는 안 된다. 단, 시작점은 계단에 포함되지 않는다.
3. 마지막 도착 계단은 반드시 밟아야 한다.

풀이를 보기전에 다이나믹프로그래밍을 처음 들어보신다면 제가 정리해놓은 개념정리를 추천합니다.

- [다이나믹프로그래밍 개념정리](https://kyun2da.github.io/2020/01/19/DynamicProgramming/){:target="\_blank"}

## 3️⃣풀이

지금부터 계단의 개수를 N이라고 하고 계단의 점수가 arr 배열에 있고 답이 저장될 배열이 dp 라고 합시다.  
먼저 계단의 개수가 1개일때, 즉 N=1이면 답은 계단을 하나 오르는 경우가 최대입니다.  
`N = 1, dp[0] = arr[0] 입니다.`  
계단의 개수가 2이면, 즉 N=2이면 무조건 두계단을 모두 하나씩 밟는 것이 가장 최대가 됩니다.  
`N = 2, dp[1] = arr[0]+ arr[1]입니다.`  
이제 계단의 개수가 3일때를 생각해봅시다.  
이때는 3개를 다 건널 순 없으므로 건너지 않을 하나의 계단을 선택해야합니다. 따라서 식은 다음과 같습니다.  
`N = 3, dp[2] = max(arr[0]+arr[2],arr[1]+arr[2])가 됩니다.`  
마지막 계단은 무조건 건너야 하기 때문에 arr[0]+arr[1]은 제외합니다.

그럼 N=4이상일때는 어떻게 될까요?
마지막 계단은 항상 건너야하므로 `dp[N]= arr[N]+ ?`입니다.  
?에 들어갈 식을 잘 생각해보면 연속된 세 개의 계단을 모두 밟아서는 안 됩니다. 하지만 맨 마지막은 무조건 밟아야하죠.  
하나의 식은 `dp[N] = arr[i]+arr[i-1]+dp[i-3]`이고 또 하나의 식은 `dp[N] = dp[i-2]+arr[i]`가 됩니다.
이 중 최댓값을 구하면 그것이 dp[N]의 값이 됩니다.
이제 소스코드를 보도록 하겠습니다.

## 4️⃣ 소스코드

```python
import sys

N = int(sys.stdin.readline())

arr = []

for _ in range(N):
    arr.append(int(sys.stdin.readline()))

if N==1:
    print(arr[0])
elif N==2:
    print(arr[0]+arr[1])
else:
    dp = [arr[0],arr[0]+arr[1],max(arr[0]+arr[2],arr[1]+arr[2])]
    for i in range(3,N):
        dp.append(max(dp[i-3]+arr[i-1]+arr[i],dp[i-2]+arr[i]))

    print(dp[N-1])
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
