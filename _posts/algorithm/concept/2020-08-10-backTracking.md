---
layout: post
title: "[알고리즘/Algorithm] 개념: 백트래킹이란?"
subtitle: "알고리즘 개념 정리 - 백트래킹"
date: 2020-08-10 19:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-os-metro.jpg"
tags:
  - 알고리즘 개념
  - 백트래킹
---

## 1️⃣서론

백트래킹은 모든 경우의 수를 전부 고려하는 알고리즘입니다. 일종의 탐색 알고리즘인데 DFS와 BFS 두가지로 구현이 가능합니다.  
일반적으로 DFS로 구현하는게 더 편하다고 합니다. 그 이유는 BFS는 큐의 크기가 커질 수 있기 때문입니다.  
DFS를 쓸 수 없는 경우는 트리의 깊이가 무한대가 될 때입니다. 이 경우에는 BFS를 쓰도록 합시다.  
하지만 일반적인 경우에는 DFS로 모두 통용되니 기본적으로 백트래킹은 DFS로 구현한다고 생각하면 좋을 것 같습니다.

## 2️⃣백트래킹 구현 방법

아래와 같은 9개의 노드를 가진 그래프가 있다고 가정해봅시다.
![백트래킹](/img/algorithm/backTracking.png)
백트래킹은 `답이 될 수 없는 후보는 더이상 깊게 들어가지않고 되돌아가는 방법`을 의미합니다.  
즉, 그림으로 본다면 4번노드가 답이 될 수 없기 때문에 8번과 9번노드는 탐색하지 않고 되돌아가서 5번노드를 탐색하게 됩니다.  
그러므로 백트래킹은 `모든 경우의 수를 탐색하는 브루트포스(brute force) 방법보다 훨씬 더 시간을 절약`할 수 있게 됩니다.

위키피디아의 순서도를 참고하면 수도코드(Pseudocode)는 다음과 같습니다.

```pseudocode
procedure bt(c) is
    if reject(P, c) then return
    if accept(P, c) then output(P, c)
    s ← first(P, c)
    while s ≠ NULL do
        bt(s)
        s ← next(P, s)
```

위의 수도코드를 해석하면 다음과 같습니다.

1. reject(P,c): 만약 다음의 노드가 후보가 아닌다면 return으로 끝낸다.
2. accept(P,c): 만약 현재 노드까지가 답과 일치한다면 답을 출력한다.
3. first(P,c): 후보 C의 첫번째 확장을 시작한다.
4. 답이 없을때까지 다음 함수를 계속반복한다.

## 4️⃣ 백트래킹 대표문제 추천

백트래킹은 다음과 같이 대표적인 문제로 N-Queen문제와 스도쿠 문제가 있습니다.
간단하게 탐색 과정을 그림으로 보겠습니다.

![N-Queen](/img/algorithm/nQueen.gif)
![sudoku](/img/algorithm/sudoku.gif)
마지막으로 백트래킹에 대해 문제를 풀어보고 싶으시다면 `백준의 단계별로 풀어보기 백트래킹` 부분을 추천합니다.

- [백준 단계별로 풀어보기 백트래킹](https://www.acmicpc.net/step/34)

그리고 아직 백트래킹이 이해가 가지 않으셨다면 저보다 더 설명이 완벽한 바킹독님의 블로그와 강의를 추천합니다!

- [바킹독님 블로그 백트래킹](https://blog.encrypted.gg/945)

<iframe width="1195" height="672" src="https://www.youtube.com/embed/Enz2csssTCs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 5️⃣ 마치며..

백트래킹 알고리즘에 대하여 알아보았습니다. 아직 저도 부족한 부분이 많아 틀린 부분이 있을 수도 있습니다.
잘못된 개념이 있거나 궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
