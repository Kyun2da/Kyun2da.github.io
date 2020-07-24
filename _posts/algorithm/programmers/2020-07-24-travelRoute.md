---
layout: post
title: "[프로그래머스/Javascript] 여행경로"
subtitle: "알고리즘"
date: 2020-07-24 17:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - DFS/BFS
---

## 1️⃣서론

프로그래머스 level3 문제 `여행경로`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/43164){:target="\_blank"}

## 2️⃣문제 설명

![여행경로](/img/algorithm/travelRoute.png)

## 3️⃣풀이

이 문제는 dfs/bfs를 이용하여 항공권을 이용하는 모든 경우의 수를 구하는 문제입니다.  
주의해야할 조건은 다음과 같습니다.

1. 항상 "ICN"공항에서 출발한다.
2. 같은 티켓이 주어질 수 있다.
3. 알파벳 순서가 앞서는 경로를 return한다.

위의 조건을 충족하기 위해서 방어코드가 몇가지가 필요했는데요. 운좋게 통과하긴 했지만 제가 푼 소스코드에서 틀린경우가 있을수도 있을 것 같다는 생각이 듭니다. 혹시 반례나 좀더 복잡도가 적은 코드가 있으시면 공유해주시면 감사하겠습니다. 방어코드는 소스코드를 보겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
//답이 들어갈 answer 배열, 방문을 표시하는 visited 배열
let answer = [];
const visited = [];

const dfs = (tickets, temp, currentTicket) => {
  if (tickets.length === temp.length) {
    //마지막 도착지를 더해줌
    temp.push(tickets[currentTicket][1]);
    //처음답은 그냥 넣고  그 다음 부터는 알파벳 비교
    if (answer.length === 0) {
      answer = temp.slice();
    } else if (answer > temp) {
      answer = temp.slice();
    }
    temp.pop(tickets[currentTicket][1]);
    return;
  }
  for (let i = 0; i < tickets.length; i++) {
    if (!visited[i] && tickets[currentTicket][1] === tickets[i][0]) {
      visited[i] = true;
      temp.push(tickets[i][0]);
      dfs(tickets, temp, i);
      visited[i] = false;
      temp.pop();
    }
  }
};

const solution = (tickets) => {
  //모든 티켓들을 한번씩 방문하며 순회한다.
  for (let i = 0; i < tickets.length; i++) {
    let temp = [];
    if (tickets[i][0] !== "ICN") continue;
    visited[i] = true;
    temp.push(tickets[i][0]);
    dfs(tickets, temp, i);
    visited[i] = false;
    temp.pop();
  }
  return answer;
};
```

## 5️⃣ 결론

DFS/BFS로 풀긴 했지만 무언가 아쉬웠던 문제였습니다. 인천으로 가는 조건도 마지막에 추가해서 좀더 효율적인 코드를 못짰던 것 같고 블로그를 찾아보니 백트래킹이 가능한 문제라고 하더군요. 이 방법도 완전히 소화하지 못한 코드인 것 같아 아쉬움이 남습니다. 좀더 효율적으로 알고리즘을 짜는 것에 중점을 둬야할 것 같습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
