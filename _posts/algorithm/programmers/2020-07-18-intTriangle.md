---
layout: post
title: "[프로그래머스/Javascript] 정수 삼각형"
subtitle: "알고리즘"
date: 2020-07-18 18:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 다이나믹 프로그래밍
---

## 1️⃣서론

프로그래머스 level3 문제 `정수 삼각형`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/43105){:target="\_blank"}

## 2️⃣문제 설명

![정수삼각형1](/img/algorithm/intTriangle.png)

## 3️⃣풀이

![정수삼각형2](/img/algorithm/intTriangle2.png)

이 문제는 다이나믹 프로그래밍을 활용하여 풀 수 있습니다. 삼각형을 위부터 차례대로 1층이라 보았을때 1번 삼각형 자리의 최대수는 항상 각 위층을 더한 값이 최대가 됩니다. 3번 노란색 선을 보면 이쪽 라인도 각 위층의 숫자를 더한값이 최댓값이 됨을 알 수 있습니다. 그러나 주황색 2번 삼각형은 위 양쪽과의 합 중 더 큰 합을 선택한 합이 더 최대임을 알 수 있습니다. 소스코드는 다음과 같습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (triangle) => {
  let answer = 0;
  const col = triangle.length;
  for (let i = 1; i < col; i++) {
    for (let j = 0; j < triangle[i].length; j++) {
      if (j === 0) {
        //1번 삼각형
        triangle[i][j] += triangle[i - 1][j];
      } else if (j === triangle[i].length - 1) {
        //3번 삼각형
        triangle[i][j] += triangle[i - 1][j - 1];
      } else {
        //2번 삼각형
        triangle[i][j] += Math.max(triangle[i - 1][j - 1], triangle[i - 1][j]);
      }
    }
  }
  for (let i = 0; i < triangle[col - 1].length; i++) {
    if (answer < triangle[col - 1][i]) {
      answer = triangle[col - 1][i];
    }
  }

  return answer;
};
```

## 5️⃣ 다른 사람의 소스코드

reduce를 활용하면 다음과 같이 짧게 쓸 수도 있는 듯 하여 기록 겸 포스팅을 해둡니다.

```js
function solution(triangle) {
  return Math.max(
    ...triangle.reduce((cost, line) => {
      return line.map((v, index) => {
        return (
          v +
          Math.max(
            index < cost.length ? cost[index] : 0,
            index > 0 ? cost[index - 1] : 0
          )
        );
      });
    }, [])
  );
}
```

## 6️⃣ 결론

dp를 사용하는데 익숙하다면 쉽게 풀 수 있던 문제였던 것 같습니다. 백준에서도 비슷한 문제를 푼 경험이 있어서 쉽게 풀 수 있었습니다.

## 7️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
