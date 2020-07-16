---
layout: post
title: "[프로그래머스/Javascript] 타일 장식물"
subtitle: "알고리즘"
date: 2020-07-16 16:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 다이나믹 프로그래밍
---

## 1️⃣서론

프로그래머스 level3 문제 `타일 장식물`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/43104){:target="\_blank"}

## 2️⃣문제 설명

![타일장식물](/img/algorithm/tileDecoration.png)

## 3️⃣풀이

이 문제는 규칙을 찾아 DP를 이용하여 해결하는 문제입니다. 타일이 늘어나는 수또한 DP를 이루지만 타일의 둘레또한 DP를 이루며 증가하는 것을 알 수 있습니다. 4, 6, 10, 16, 26... 이런식으로 증가하는 순열은 `arr[i]=arr[i-1]+arr[i-2]`가 성립합니다. 따라서 이 식을 사용하여 문제를 해결할 수 있었습니다. 그럼 소스코드 보겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (N) => {
  const arr = [4, 6];
  for (let i = 2; i <= N - 1; i++) {
    arr[i] = arr[i - 1] + arr[i - 2];
  }
  return arr[N - 1];
};
```

## 5️⃣ 결론

규칙이 있다는 것을 깨닫고 DP를 사용하여 쉽게 풀 수 있었던 문제입니다. 프로그래머스가 level3 에서는 그래프 dp 위주의 개념들이 나오는것 같은데 dp 개념을 익히는데에는 좋은 문제라고 생각합니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
