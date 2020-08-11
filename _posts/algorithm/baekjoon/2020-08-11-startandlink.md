---
layout: post
title: "[백준/Python] 14889 스타트와 링크"
subtitle: "알고리즘 - 백트래킹"
date: 2020-08-11 18:30:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-universe.jpg"
tags:
  - Algorithm
  - 백준
  - 백트래킹
---

## 1️⃣서론

백준 문제 14889번 `스타트와 링크` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/14889){:target="\_blank"}

## 2️⃣문제 설명

이 문제는 스타트팀과 링크팀을 나눠 각 팀의 능력치의 차이를 최소로 하는 것이 문제입니다.  
각 시너지가 배열로 주어지고 각 팀의 시너지의 합을 구해 차이를 구해야합니다.  
결국 `완전탐색으로 해결할 수 밖에 없는 문제`입니다.  
총 인원은 항상 짝수이므로 `스타트팀의 인원수는 항상 N//2명` 입니다.  
혹시 백트래킹 개념이 아직 익숙하지 않으시다면 제가 정리해놓은 백트래킹 개념을 보고 오시면 좋을 것 같습니다.

- [백트래킹 개념정리](https://kyun2da.github.io/2020/08/10/backTracking/){:target="\_blank"}

## 3️⃣풀이

흐름은 일반적으로 dfs를 구현할때와 비슷하게 구현합니다.  
dfs가 답을 체크할때는 스타트팀이 N//2명일 시점입니다.  
`스타트팀의 배열에 속하지 않은 사람을 링크팀에 넣고 각각 팀의 시너지 합`을 구합니다.  
그 후에 서로의 차이가 최소인지를 확인하며 계속 답을 갱신합니다.  
주의해야할 점은 링크팀은 답 체크시점에만 더해주므로 `항상 답인지를 체크한 후에 마지막에는 링크팀을 비워주어야 합니다.`
그럼 백트래킹을 이용한 소스코드를 보고 가시겠습니다.

## 4️⃣ 소스코드

```python
def dfs(index):
    global minAns
    # 백트래킹 답 체크 시점
    if index == N // 2:
        startSum = 0
        linkSum = 0
        for i in range(0,N):
            if i not in start:
                link.append(i)
        for i in range(0, N // 2 - 1):
            for j in range(i+1, N // 2):
                startSum += arr[start[i]][start[j]] + arr[start[j]][start[i]]
                linkSum += arr[link[i]][link[j]] + arr[link[j]][link[i]]
        diff = abs(linkSum-startSum)
        if minAns > diff:
            minAns = diff
        # 링크팀을 항상 계산이 끝나면 비워줘야한다.
        link.clear()
        return
    #dfs 시행
    for i in range(N):
        if i in start: continue
        if len(start)>0 and start[len(start)-1]> i : continue
        start.append(i)
        dfs(index + 1)
        start.pop()


N = int(input())

arr = []
start = []
link = []
for i in range(N):
    arr.append(list(map(int, input().split())))

minAns = float('Inf')
dfs(0)
print(minAns)
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
