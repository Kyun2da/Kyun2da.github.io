---
layout: post
title: "[백준/Python] 14888 연산자 끼워넣기"
subtitle: "알고리즘 - 백트래킹"
date: 2020-08-11 18:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-universe.jpg"
tags:
  - Algorithm
  - 백준
  - 백트래킹
---

## 1️⃣서론

백준 문제 14888번 `연산자 끼워넣기` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/14888){:target="\_blank"}

## 2️⃣문제 설명

이 문제는 백트래킹을 이용하여 연산자의 위치를 바꿔가며 가장 최대가 되는 값과 최소가 되는 값을 찾는 문제입니다.
혹시 백트래킹을 처음들어본다면 제가 개념을 정리해놓은 곳을 가보시면 될 것 같습니다.

- [백트래킹 개념정리](https://kyun2da.github.io/2020/08/10/backTracking/){:target="\_blank"}

## 3️⃣풀이

입력으로는 첫째줄에는 수의 개수 N, 둘째 줄에는 A1,A2,...가 주어지고 마지막 줄에는 연산자의 숫자가 +, -, \*, /가 차례대로 주어집니다.
여기서 숫자의 위치는 바뀌지 않고 연산자의 위치만 바뀌므로 DFS로 해결할 수 있습니다.  
예제 2번을 통해 확인을 해보면 숫자 3,4,5가 주어지고 더하기와 곱셈이 하나씩 주어집니다.  
이에 따라 경우의 수는 다음과 같이 두가지가 있습니다.

1. 3+4\*5 = 35
2. 3\*4+5 = 35
   여기서 주의해야할 점은 연산자의 우선순위는 고려하지않고 `항상 앞에있는 연산자부터 계산`한다는 점입니다.
   그럼 DFS를 통해 해결한 소스코드를 보시겠습니다.

## 4️⃣ 소스코드

```python
def dfs(index,res):
    global minAns
    global maxAns
    # 계산의 끝에 도달했을 때 최댓값과 최솟값이 될 수 있는지 판단한다.
    if index==N-1:
        if minAns > res:
            minAns = res
        if maxAns < res:
            maxAns = res
        return res
    # 백트래킹 DFS로 순회
    for i in range(4):
        temp = res
        if operator[i]==0:
            continue
        if i==0:
            res+=numArr[index+1]
        elif i==1:
            res-=numArr[index+1]
        elif i==2:
            res*=numArr[index+1]
        else:
            if res<0:
                res = abs(res)//numArr[index+1]*-1
            else:
                res //=numArr[index+1]
        operator[i] -= 1
        dfs(index+1,res)
        operator[i] += 1
        res = temp

N = int(input())
numArr = list(map(int,input().split()))
operator = list(map(int,input().split()))
minAns = float('Inf')
maxAns = float('-Inf')

dfs(0,numArr[0])
print(maxAns)
print(minAns)
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
