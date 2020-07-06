---
layout: post
title: "[프로그래머스/Javascript] 위장"
subtitle: "알고리즘"
date: 2020-07-06 15:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
---

## 1️⃣서론

프로그래머스 level2 문제 `위장`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/42578){:target="\_blank"}

## 2️⃣문제 설명

![위장1](/img/algorithm/Camouflage1.png)
![위장2](/img/algorithm/Camouflage2.png)

## 3️⃣풀이

입을 수 있는 옷의 가지수를 구하는 문제입니다. `최소 한가지의 옷은 입어야하므로 모든 경우의 수에서 하나도 입지않는 경우의 수 1을 빼주는 형식으로 구하였습니다.`

## 4️⃣ 내가 푼 소스코드

```js
function solution(clothes) {
  let answer = 1;
  const obj = {};

  //옷을 개수별로 분리 + 1  (안입는 경우가 있으므로 +1을 해줘야한다.)
  for (let i = 0; i < clothes.length; i++) {
    obj[clothes[i][1]] = (obj[clothes[i][1]] || 1) + 1;
  }

  for (let key in obj) {
    answer *= obj[key];
  }
  //console.log(obj);

  //아예 안입는 경우는 빼줘야하므로 -1을 해준다.
  return answer - 1;
}
```

## 5️⃣ 결론

백준에서 비슷한 문제를 본 적이 있는지 어디서 많이 본 문제인 것 같아서 쉽게 풀었습니다.
경우의 수를 생각할 때 복잡하게 생각하지 않는다면 쉽게 풀 수 있었던 문제인 것 같습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
