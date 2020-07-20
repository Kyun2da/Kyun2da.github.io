---
layout: post
title: "[프로그래머스/Javascript] 단속 카메라"
subtitle: "알고리즘"
date: 2020-07-20 16:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 그리디
---

## 1️⃣서론

프로그래머스 level3 문제 `단속 카메라`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/42884){:target="\_blank"}

## 2️⃣문제 설명

![단속카메라](/img/algorithm/checkCamera.png)

## 3️⃣풀이

이 문제는 탐욕적으로 답을 찾아내는 그리디 문제입니다. 풀이는 다음과 같습니다.

1. 먼저 차량의 경로를 진출 지점을 기준으로 정렬합니다. 카메라를 설치할 지점을 초기에 -30001로 잡아놓습니다.
2. 설치한 카메라의 위치가 차량의 진입지점보다 전에 있다면 다음 카메라를 그 차량의 진출지점으로 정해줍니다.
3. 이런식으로 루프를 계속 돌려 카메라가 설치된 개수를 구합니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (routes) => {
  let answer = 0;
  routes.sort((a, b) => {
    return a[1] - b[1];
  });
  let camera = -30001;
  for (let i = 0; i < routes.length; i++) {
    if (camera < routes[i][0]) {
      answer++;
      camera = routes[i][1];
    }
  }
  return answer;
};
```

## 5️⃣ 결론

그리디 문제였는데 그리디 문제 자체가 방식이 어렵고 구현하는데는 크게 어려움이 있어서 이 방법을 어떻게 생각하느냐가 중요했던 문제였던 것 같습니다. 근데 이러한 문제가 그리디라는 것을 어떻게 알고 접근해야할지 그것에 대한 어려움이 있는 것 같습니다. 알고리즘 유형 파악을 좀더 잘 할 수 있도록 많이 풀어봐야겠습니다. 감사합니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
