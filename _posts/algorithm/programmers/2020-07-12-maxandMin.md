---
layout: post
title: "[프로그래머스/Javascript] 최댓값과 최솟값"
subtitle: "알고리즘"
date: 2020-07-12 21:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 문자열
---

## 1️⃣서론

프로그래머스 level2 문제 `최댓값과 최솟값`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/12939){:target="\_blank"}

## 2️⃣문제 설명

![최댓값과 최솟값](/img/algorithm/maxandMin.png)

## 3️⃣풀이

이 문제는 공백으로 나눠진 숫자들로 이루어진 문자열을 파싱하여 최솟값과 최댓값을 리턴하는 문제였습니다.
자바스크립트는 split 함수를 이용해서 비교적 쉽게 파싱하고 해결할 수 있었습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (s) => {
  const arr = s
    .split(" ")
    .map((it) => parseInt(it))
    .sort((a, b) => a - b);
  return String(arr[0]) + " " + String(arr[arr.length - 1]);
};
```

## 5️⃣ 결론

이 문제는 자바스크립트의 `split`, `map`, `sort`함수를 사용하여 쉽게 해결할 수 있었습니다. 자바스크립트가 문자열 문제를 푸는데에 있어서 확실히 편리한감이 있는 것 같습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
