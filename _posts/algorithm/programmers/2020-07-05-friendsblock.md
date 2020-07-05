---
layout: post
title: "[프로그래머스/Javascript] 프렌즈4블록"
subtitle: "알고리즘 - 배열 다루기"
date: 2020-07-05 14:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 배열
---

## 1️⃣서론

프로그래머스 level2 문제 `[1차] 프렌즈4블록`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/17679){:target="\_blank"}

## 2️⃣문제 설명

![프렌즈블록1](/img/algorithm/friendsblock1.png)
![프렌즈블록2](/img/algorithm/friendsblock2.png)
![프렌즈블록3](/img/algorithm/friendsblock3.png)
![프렌즈블록4](/img/algorithm/friendsblock4.png)

## 3️⃣풀이

이문제는 푸는 원리는 다들 쉽게 이해할 테지만 구현력을 상당히 요구하는 문제였다. 문제 설명을 그대로 따라가며 알고리즘을 구현하면 되지만
배열에 익숙하지 않다면 많이 헤매야 했다. 풀이는 다음과 같다.  

1. 먼저 배열의 문자열을 2차원 배열로 나눈다.
2. 배열에서 지워질 블록의 인덱스를 구해 arr안에 넣는다.
3. 배열에서 지워질 블록을 0으로 바꾼다.
4. 깨진 블록을 없애고 위에서 블록을 당겨온다. (이 부분의 로직이 어려운데 먼저 위에서 가져올 블록이 있는지 검사한다.)

## 4️⃣ 내가 푼 소스코드

```js
const solution = (m, n, board) => {
  let answer = 0;
  //1. 먼저 배열의 문자열을 2차원 배열로 나눈다.
  board = board.map((v) => v.split(""));

  //2. 배열에서 지워질 블록의 인덱스를 구해 arr안에 넣는다.
  while (true) {
    const arr = [];
    for (let i = 0; i < m - 1; i++) {
      for (let j = 0; j < n - 1; j++) {
        if (
          board[i][j] &&
          board[i][j] === board[i + 1][j] &&
          board[i][j] === board[i][j + 1] &&
          board[i][j] === board[i + 1][j + 1]
        ) {
          arr.push([i, j]);
        }
      }
    }
    // 답을 구하는 로직 : 깨질 블록이 없다면 0인 개수를 세고 리턴한다.
    if (!arr.length) {
      return [].concat(...board).filter((v) => !v).length;
    }

    // 3. 배열에서 지워질 블록을 0으로 바꾼다.
    for (let i = 0; i < arr.length; i++) {
      const col = arr[i][0];
      const row = arr[i][1];
      board[col][row] = 0;
      board[col][row + 1] = 0;
      board[col + 1][row] = 0;
      board[col + 1][row + 1] = 0;
    }

    // 4. 깨진 블록을 없애고 위에서 블록을 당겨온다.
    for (let i = m - 1; i > 0; i--) {
      if (!board[i].some((v) => !v)) continue;

      for (let j = 0; j < n; j++) {
        for (let k = i - 1; k >= 0 && !board[i][j]; k--) {
          if (board[k][j]) {
            board[i][j] = board[k][j];
            board[k][j] = 0;
            break;
          }
        }
      }
    }
  }
};
```

## 5️⃣ 결론

4번 로직이 좀 어려운데 배열에 대한 조건들을 잘 생각해보고 따져봐야 통과할 수 있는 문제였다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
