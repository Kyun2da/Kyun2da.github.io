---
layout: post
title: "[프로그래머스/Javascript] 타겟 넘버"
subtitle: "알고리즘"
date: 2020-07-09 14:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 완전탐색
---

## 1️⃣서론

프로그래머스 level2 문제 `타겟 넘버`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/43165){:target="\_blank"}

## 2️⃣문제 설명

![타겟넘버](/img/algorithm/targetnumber.png)

## 3️⃣풀이

이 문제는 dfs를 이용하여 나올수 있는 경우의 수를 다 검색하여 답을 찾는 문제입니다. 이 경우에는 계속 두갈래로 나눠지는데
`각 자리수가 +가 되느냐 아니면 -가 되느냐로 두갈래로 나뉘어집니다.` 따라서 경우의 수는 위의 예시에따르면 2^5가 됩니다. 주어진 경우의 수를 dfs로 순회하면서 target과 합이 같는 경우를 찾아서 더해주면 답이 됩니다.

## 4️⃣ 내가 푼 소스코드

```js
let answer = 0;
const dfs = (numbers, target, idx, plusMinus, sum) => {
  if (idx === numbers.length) {
    if (target === sum) {
      answer += 1;
    }
    return;
  } else {
    let tmp = sum + numbers[idx] * plusMinus;
    dfs(numbers, target, idx + 1, 1, tmp);
    dfs(numbers, target, idx + 1, -1, tmp);
  }
};

const solution = (numbers, target) => {
  dfs(numbers, target, 0, 1, 0);
  dfs(numbers, target, 0, -1, 0);
  return answer / 2;
};
```

## 5️⃣ 다른 소스코드

풀이에 좀더 직관적인 코드가 있어서 가져와봤습니다..
아직 제가 dfs에 익숙하지 않아서 그런지 코드를 좀 비효율적으로 짠것 같네요.
dfs 최적코드는 이 코드가 가장 최적의 코드인 것 같습니다.

```js
function solution(numbers, target) {
  let answer = 0;
  getAnswer(0, 0);
  function getAnswer(x, value) {
    if (x < numbers.length) {
      getAnswer(x + 1, value + numbers[x]);
      getAnswer(x + 1, value - numbers[x]);
    } else {
      if (value === target) {
        answer++;
      }
    }
  }
  return answer;
}
```

## 6️⃣ 결론

dfs를 알고 있었다면 쉽게 풀 수 있던 문제였던것 같습니다.
저는 아직 완벽하게 dfs를 익히지 못해서 좀 비효율적으로 짠 것 같아 좀더 dfs bfs에 익숙해져야 겠다는 생각을 했습니다.

## 7️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
