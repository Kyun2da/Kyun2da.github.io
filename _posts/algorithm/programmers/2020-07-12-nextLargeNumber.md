---
layout: post
title: "[프로그래머스/Javascript] 다음 큰 숫자"
subtitle: "알고리즘"
date: 2020-07-12 17:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
---

## 1️⃣서론

프로그래머스 level2 문제 `다음 큰 숫자`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/12911){:target="\_blank"}

## 2️⃣문제 설명

![올바른 괄호](/img/algorithm/nextLargeNumber.png)

## 3️⃣풀이

이 문제는 10진수를 2진수로 변환하는 방법을 안다면 쉽게 풀 수 있습니다. 먼저 10진수를 1씩 증가시키며 그 숫자를 이진수로 변환
하여 1의 개수를 비교해간다면 쉽게 풀 수 있었습니다. 코드는 다음과 같습니다.

## 4️⃣ 내가 푼 소스코드

```js
const digitOneNum = (num) => {
  const str = num.toString(2);
  let length = 0;
  for (let i = 0; i < str.length; i++) {
    if (str[i] === "1") {
      length++;
    }
  }
  return length;
};

const solution = (n) => {
  const compareLength = digitOneNum(n);
  for (let i = n + 1; i <= 1000000; i++) {
    const answer = digitOneNum(i);
    if (compareLength === answer) {
      return i;
    }
  }
  return answer;
};
```

## 5️⃣ 결론

자바스크립트는 이진수에 대한 변환이 `toString(2)`로 정의가 되있어서 쉽게 풀 수 있었습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
