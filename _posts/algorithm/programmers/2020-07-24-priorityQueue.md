---
layout: post
title: "[프로그래머스/Javascript] 이중우선순위큐"
subtitle: "알고리즘"
date: 2020-07-24 16:30
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 우선순위큐
---

## 1️⃣서론

프로그래머스 level3 문제 `이중우선순위큐`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/42628){:target="\_blank"}

## 2️⃣문제 설명

![이중우선순위큐](/img/algorithm/priorityQueue.png)

## 3️⃣풀이

이 문제는 이중우선순위큐를 구현하는 문제입니다. 자바스크립트에선 배열로 이를 간단하게 구현할 수 있는데요. 원소가 들어올때마다 정렬하고 최솟값은 맨 앞으로, 최댓값은 맨 뒤로 놓아진 상태에서 `shift와 pop 연산`을 하면 쉽게 풀 수 있는 문제였습니다. 그럼 소스코드 보겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (operations) => {
  let answer = [];
  for (let i = 0; i < operations.length; i++) {
    const num = Number(operations[i].substring(2));
    switch (operations[i].substring(0, 1)) {
      case "I":
        answer.push(num);
        answer.sort((a, b) => {
          return a - b;
        });
        break;
      case "D":
        if (num === 1) {
          answer.pop();
        } else {
          answer.shift();
        }
        break;
    }
  }
  if (answer.length === 0) {
    return [0, 0];
  }

  return [answer[answer.length - 1], answer[0]];
};
```

## 5️⃣ 결론

이중우선순위큐를 구현하는 문제였는데 자바스크립트는 shift와 pop의 내장 함수 덕분에 쉽게 구할 수 있는 문제 였습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
