---
layout: post
title: "[백준/Python] 1707 이분 그래프"
subtitle: "알고리즘 - 이분 그래프"
date: 2020-09-21 20:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-universe.jpg"
tags:
  - Algorithm
  - 백준
  - DFS/BFS
mathjax: true
---

## 1️⃣ 서론

백준 문제 1707번 `이분 그래프` 입니다. `파이썬(Python)`으로 풀었습니다.

- [출처](https://www.acmicpc.net/problem/1707){:target="\_blank"}

## 2️⃣ 문제 설명

그래프의 정점의 집합을 둘로 분할하여, 각 집합에 속한 정점끼리는 서로 인접하지 않도록 분할할 수 있을 때, 그러한 그래프를 특별히 `이분 그래프 (Bipartite Graph)` 라 부른다.

그래프가 입력으로 주어졌을 때, 이 그래프가 이분 그래프인지 아닌지 판별하는 프로그램을 작성하시오.

## 3️⃣ 풀이

이분 그래프에 대해서는 [나무위키](https://ko.wikipedia.org/wiki/%EC%9D%B4%EB%B6%84_%EA%B7%B8%EB%9E%98%ED%94%84#%EB%B3%80%EB%B3%84_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98){:target="\_blank"}를 참조하시면 더 좋을 것 같습니다.

변별 알고리즘 또한 나무위키에 잘 나와있는데요.

바로, 그래프의 꼭짓점들을 `깊이 우선 탐색으로 나열한 뒤, 각 꼭짓점들을 이웃 꼭짓점들과 다른 색으로 계속해서 칠해 나가면서, 같은 색깔의 꼭짓점이 서로 연결되어 있는 모순이 발생하는지 여부를 확인`하면 됩니다.

이 알고리즘의 시간복잡도는 $O(\|V\|+\|E\|)$입니다.

## 4️⃣ 소스코드

```python
import sys

sys.setrecursionlimit(10 ** 6)
input = sys.stdin.readline


def dfs(now, group):
    vis[now] = group
    for i in arr[now]:
        # 아직 안가본 곳이면 방문
        if vis[i] == 0:
            if not dfs(i, -group):
                return False
        # 방문한 곳인데 색깔이 다르면 취소
        elif vis[i] == vis[now]:
            return False
    return True


for _ in range(int(input())):
    v, e = map(int, input().split())
    arr = [[] for _ in range(v + 1)]
    vis = [0] * (v + 1)
    for _ in range(e):
        x, y = map(int, input().split())
        arr[x].append(y)
        arr[y].append(x)
    ans = True
    for i in range(1, v + 1):
        if vis[i] == 0:
            ans = dfs(i, 1)
            if not ans:
                break
    print("YES" if ans else "NO")
```

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
