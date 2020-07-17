---
layout: post
title: "[프로그래머스/Javascript] 섬 연결하기"
subtitle: "알고리즘"
date: 2020-07-17 16:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - DFS/BFS
---

## 1️⃣서론

프로그래머스 level3 문제 `섬 연결하기`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/42861){:target="\_blank"}

## 2️⃣문제 설명

![섬연결하기1](/img/algorithm/linkedIsland1.png)
![섬연결하기2](/img/algorithm/linkedIsland2.png)

## 3️⃣풀이

이 문제는 어려워서 풀이를 찾아서 제 코드로 다시 변경하여 풀었습니다. 두가지 방법이 있는데요 하나는 [크루스칼 알고리즘](https://m.blog.naver.com/PostView.nhn?blogId=ndb796&logNo=221230994142&proxyReferer=https:%2F%2Fwww.google.com%2F){:target="\_blank"} 을 이용하는 것입니다. 하지만 저는 여기서 크루스칼 알고리즘을 사용하지 않고 간선을 순회하며 노드를 순서대로 연결하는 알고리즘을 사용하였습니다. 여기서 크루스칼과 다른점은 크루스칼은 Union Find 기법을 사용하여 사이클이 되는지 안되는지를 검사하지만 아래의 소스코드의 알고리즘은 간선의 양쪽노드가 방문한 노드인지를 검사합니다. 단, 두개다 방문을 안됬을때 또한 아래의 알고리즘은 넘어갑니다. 이어지지 않는 두개의 그래프가 만들어 질 수 있기 때문입니다. 그럼 소스코드를 보고 가겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (n, costs) => {
  let answer = 0;
  const isVisited = new Array(n).fill(false);
  const isBridge = new Array(costs.length).fill(false);
  //비용이 작은 간선을 순서로 정렬
  costs.sort((a, b) => {
    return a[2] - b[2];
  });
  let num = 0;

  //처음에 가장 작은 간선을 무조건 넣는다. 비용이 가장작으므로
  isVisited[costs[0][0]] = true;
  isVisited[costs[0][1]] = true;
  isBridge[0] = true;
  answer += costs[0][2];
  num += 1;

  //간선의 개수가 노드의 개수-1을 만족할때까지 순회한다.
  while (num < n - 1) {
    for (let i = 1; i < costs.length; i++) {
      const [start, end, cost] = costs[i];
      //다리가 건설되어 있지않고 한쪽노드만 방문한경우를 찾는다.
      if (
        !isBridge[i] &&
        ((!isVisited[start] && isVisited[end]) ||
          (isVisited[start] && !isVisited[end]))
      ) {
        num++;
        answer += cost;
        isVisited[start] = true;
        isVisited[end] = true;
        isBridge[i] = true;
        break;
      }
      console.log(isVisited);
    }
  }
  return answer;
};
```

## 5️⃣ 결론

이 문제는 크루스칼 알고리즘이 시간복잡도가 뛰어난데요. 제가 크루스칼 알고리즘을 아직 개념만 알고 자바스크립트로 구현을 해본적이 없어서 쉽게 크루스칼 알고리즘을 적용하지 못했던 케이스입니다. 그래프쪽이 아직 많이 부족한 것 같습니다. 그래프 공부를 열심히 해야겠다는 생각이 듭니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
