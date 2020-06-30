---
layout: post
title: "[프로그래머스/Javascript] 짝지어 제거하기"
subtitle: "알고리즘 - 스택"
date: 2020-06-28 19:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 스택
---

## 1️⃣서론

프로그래머스 level2 문제 `짝지어 제거하기`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/12973){:target="\_blank"}

## 2️⃣문제 설명

![피보나치](/img/algorithm/removeInPair.png)

## 3️⃣풀이

이 문제는 어떻게 문자열을 짝지어 제거할때 검사를 어떻게 효율적이게 하느냐에 따라 시간초과가 날 수도 있고 통과할 수도 있는 문제입니다.
처음에는 `스택을 전혀 생각 못하고 그냥 제거한뒤에 제거한 자리의 앞으로 가서 다시 for문을 순회하는 방법`을 사용했습니다. 하지만 이렇게 했더니 시간초과가 났고 스택을 사용해야 통과하였습니다. 초기코드와 최종코드를 보겠습니다.

## 4️⃣ 초기 소스코드

시간초과 발생

```js
const solution = (s) => {
  let answer = 0;
  for (let i = 0; i < s.length - 1; i++) {
    if (s[i] === s[i + 1]) {
      s = s.substr(0, i) + s.substr(i + 2);
      i -= 2;
    }
    console.log(s);
  }
  if (s === "") {
    return 1;
  }
  return 0;
};
```

## 5️⃣ 최종 소스코드

```js
const solution = (s) => {
  const stack = [];

  for (let i = 0; i < s.length; i++) {
    if (stack.length === 0 || stack[stack.length - 1] !== s[i]) {
      stack.push(s[i]);
    } else {
      stack.pop();
    }
  }

  if (stack.length === 0) {
    return 1;
  }
  return 0;
};
```

## 6️⃣ 결론

이 문제는 스택을 생각하는 것이 그리 쉽지는 않았던 것 같습니다.
어떤 자료구조를 써야하는 지에 대한 힘을 더 길러야 겠다는 생각이 듭니다.

## 7️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
