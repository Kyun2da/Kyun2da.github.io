---
layout: post
title: "[프로그래머스/Javascript] 입국심사"
subtitle: "알고리즘"
date: 2020-07-24 17:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 이분탐색
---

## 1️⃣서론

프로그래머스 level3 문제 `입국심사`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/43238){:target="\_blank"}

## 2️⃣문제 설명

![입국심사](/img/algorithm/Immigration.png)

## 3️⃣풀이

이 문제는 이분탐색을 활용해서 푸는 문제입니다. 모든 사람이 심사를 받는데 걸리는 가장 최소의 시간을 구하는 것입니다.
가장 최대의 시간은 가장 오래걸리는 심사대에서만 계속 심사를 받을 때의 시간입니다. `이를 활용해 1초부터 가장 최대의 시간까지 이분탐색을 하며 가장 최소의 시간에서 n명을 검사할 수 있을 때 까지 탐색을 하며 답을 구하는 문제`입니다. 그럼 코드를 보겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (n, times) => {
  let answer = Infinity;

  times.sort((a, b) => {
    return a - b;
  });
  let left = 1;
  //가장 최대의 시간
  let right = times[times.length - 1] * n;

  //가장 최소의 시간을 찾을때까지 계속 탐색한다.
  while (left <= right) {
    let mid = parseInt((left + right) / 2);
    let cnt = 0;
    for (let i = 0; i < times.length; i++) {
      cnt += parseInt(mid / times[i]);
      if (cnt >= n) {
        answer = Math.min(answer, mid);
      }
    }
    if (cnt >= n) {
      right = mid - 1;
    } else {
      left = mid + 1;
    }
  }
  return answer;
};
```

## 5️⃣ 결론

먼저 이분탐색이라고 주제에 주어지지 않았다면 풀기 어려웠을 거라는 생각이 들었습니다. 주제가 이분탐색임을 알고도 처음에 어떻게 해결을 해야할지 막막해서 블로그를 보면서 풀이법을 익혔습니다. 아직 이분탐색이 완벽하지 않다는 느낌을 받았습니다. 좀더 활용방법과 문제해결능력을 키워야할 것 같습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
