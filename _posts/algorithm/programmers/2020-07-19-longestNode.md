---
layout: post
title: "[프로그래머스/Javascript] 가장 먼 노드"
subtitle: "알고리즘"
date: 2020-07-19 23:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 그래프
---

## 1️⃣서론

프로그래머스 level3 문제 `가장 먼 노드`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/49189){:target="\_blank"}

## 2️⃣문제 설명

![가장 먼 노드1](/img/algorithm/longestNode1.png)
![가장 먼 노드2](/img/algorithm/longestNode2.png)

## 3️⃣풀이

이 문제는 그래프 문제입니다. 1번노드에서 가장 멀리 떨어진 노드의 갯수를 구하는 문제입니다. 저는 모든 노드를 방문하며 배열에 각 노드의 1번 노드와의 거리를 구해서 넣어주는 방식을 택했습니다. 소스코드 보겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (n, edge) => {
  const visited = new Array(n + 1).fill(-1);
  const queue = [1];
  visited[0] = 0;
  visited[1] = 0;
  //모든 노드를 방문할때까지 계속한다.
  while (edge.length !== 0) {
    //방문한 노드를 큐에서 뺀다.
    const Node = queue.shift();
    //edge를 순회하며 다음 방문할 노드를 찾는다.
    for (let i = 0; i < edge.length; i++) {
      //방문할 노드가 있다면
      if (edge[i].includes(Node)) {
        const filter = edge[i].filter((e) => e !== Node);
        //이미 방문했던 노드라면 엣지를 그냥 skip한다.
        if (visited[filter[0]] !== -1) {
          edge.splice(i, 1);
          i--;
          continue;
        }
        //방문하지 않았던 노드라면 노드를 방문해준다.
        queue.push(filter[0]);
        visited[filter[0]] = visited[Node] + 1;
        edge.splice(i, 1);
        i--;
      }
    }
  }
  const maxNum = Math.max(...visited);
  return visited.filter((e) => e === maxNum).length;
};
```

## 5️⃣ 결론

그래프의 가장 먼 노드를 구하는 문제였는데 하마터면 시간초과가 날 뻔 했던 것 같습니다. 좀더 효율적으로 풀 수 있는 방법이 있다면 알려주시면 감사하겠습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
