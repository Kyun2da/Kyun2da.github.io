---
layout: post
title: "[프로그래머스/Javascript] 가장 큰 정사각형 찾기"
subtitle: "알고리즘"
date: 2020-07-10 14:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 다이나믹 프로그래밍
---

## 1️⃣서론

프로그래머스 level2 문제 `가장 큰 정사각형 찾기`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/12905){:target="\_blank"}

## 2️⃣문제 설명

![가장큰정사각형찾기1](/img/algorithm/biggestSquare1.png)
![가장큰정사각형찾기2](/img/algorithm/biggestSquare2.png)

## 3️⃣풀이

가장 큰 정사각형을 찾는 문제입니다. 이 문제는 `다이나믹 프로그래밍`을 이용하여 답을 풀 수 있습니다.
가장 작은 정사각형은 `1*1` 크기의 정사각형입니다. 그 다음 크기는 `2*2, 3*3 ...` 이런식으로 쭉 가는것을
알 수 있습니다.  
`1*1은 그냥 구하면 되지만 2*2는 1*1 4개가 모두 1이어야 성립이 가능합니다.`  
코드로 적어보면 `Math.min(board[j - 1][i], board[j][i - 1], board[j - 1][i - 1]) + 1;`입니다.
`3*3, 4*4, ...` 나머지 모두 위의 식이 성립하는 것을 볼 수 있습니다.
그리고 1부터검사하므로 첫번째 열과 첫번째 행에서 answer을 초기에 검사해주는 방어코드도 필요합니다.
그럼 코드를 보고 가겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (board) => {
  let answer = 0;

  //n*1, 1*n의 직사각형을 대비하여 answer이 1이 될 수 있는 상황을 생각해준다.
  answer = board[0].indexOf(1) != -1 ? 1 : 0;
  for (let i = 0; i < board.length; i++) {
    if (board[i][0] === 1) {
      answer = 1;
      break;
    }
  }

  //dp를 이용하여 검사
  for (let j = 1; j < board.length; j++) {
    for (let i = 1; i < board[0].length; i++) {
      if (board[j][i] === 1) {
        board[j][i] =
          Math.min(board[j - 1][i], board[j][i - 1], board[j - 1][i - 1]) + 1;
      }
      if (board[j][i] > answer) {
        answer = board[j][i];
      }
    }
  }
  return answer * answer;
};
```

## 5️⃣ 결론

`Math.min(board[j - 1][i], board[j][i - 1], board[j - 1][i - 1]) + 1;` 이거 한줄을 생각해내는게
정말 어려운 것 같습니다. dp라는 것을 알아차리는 것도 오래걸렸고 위의 코드또한 생각해내는 것도 오래걸렸습니다.
아직 알고리즘 개념을 적용시키는 훈련이 더 필요한 것 같습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
