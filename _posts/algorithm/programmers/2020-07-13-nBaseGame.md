---
layout: post
title: "[프로그래머스/Javascript] N진수 게임"
subtitle: "알고리즘"
date: 2020-07-13 18:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
---

## 1️⃣서론

프로그래머스 level2 문제 `N진수 게임`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/17687){:target="\_blank"}

## 2️⃣문제 설명

![파일명 정렬1](/img/algorithm/nBasegame1.png)
![파일명 정렬2](/img/algorithm/nBasegame2.png)

## 3️⃣풀이

이 문제는 미리 설계를 잘 해야 쉽게 통과할 수 있었던 문제가 아니었나 싶습니다.  
`진법 n, 미리 구할 숫자의 개수 t, 게임에 참가하는 인원 m, 튜브의 순서 p`가 주어집니다.  
먼저 구할숫자의 개수를 구하기 위해 필요한 게임 진행 문자열의 길이는 `t*m` 입니다. 문자열의 길이가 `t*m`보다 작을 때까지 게임을 진행하고 해당 문자열을 다시 한번 순회하며 튜브의 순서마다 나온 숫자를 answer 문자열에 추가합니다.  
`(i + 1) % m === p || ((i + 1) % m === 0 && m === p)` 이 식은 문자열의 인덱스가 튜브의 순서인지 아닌지를 검사하는 조건식입니다.
문제 설계는 이쯤으로 하고 코드를 살펴보겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (n, t, m, p) => {
  let answer = "";
  let str = "";
  let i = 0;
  while (str.length <= t * m) {
    const baseStr = i.toString(n);
    str += baseStr;
    i++;
  }
  for (let i = 0; i < str.length; i++) {
    if (answer.length === t) break;
    if ((i + 1) % m === p || ((i + 1) % m === 0 && m === p)) {
      answer += str[i];
    }
  }
  return answer.toUpperCase();
};
```

## 5️⃣ 결론

카카오 문제치고는 그리 어렵지는 않았던 문제였습니다. 진법을 변환하는 방법과 어떻게 문제를 설계하느냐가 가장 중요했던 문제였습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
