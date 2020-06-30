---
layout: post
title: "[프로그래머스/Javascript] JadenCase 문자열 만들기"
subtitle: "알고리즘 - 문자열 변환"
date: 2020-06-26 19:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 문자열
---

## 1️⃣서론

프로그래머스 level2 문제 `JadenCase 문자열 만들기`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/12951){:target="\_blank"}

## 2️⃣문제 설명

![피보나치](/img/algorithm/jadencase.png)

## 3️⃣풀이

먼저 이 문제는 문장의 매 단어의 제일 앞글자를 대문자로 하고 나머지 문자는 소문자로 치환해주어야 하는 알고리즘을 구현해야 합니다.
그렇게 하기 위해 저는 **문장의 단어를 배열에 저장하여 각단어의 제일 앞을 대문자로 저장하고 나머지는 소문자로 놔두는 식**을 사용하였습니다. 그렇게 구현된 초기 소스코드는 아래와 같습니다.

## 4️⃣ 초기 소스코드

```js
const changeJadenWord = (s) => {
  let s1 = s.substring(0, 1);
  let s2 = s.substring(1);
  if (
    s1.charCodeAt() >= "a".charCodeAt() &&
    s1.charCodeAt() <= "z".charCodeAt()
  ) {
    s1 = s1.toUpperCase();
  }
  s2 = s2.toLowerCase();
  return s1 + s2;
};

const solution = (s) => {
  let arr = s.split(" ");
  for (let i = 0; i < arr.length; i++) {
    arr[i] = changeJadenWord(arr[i]);
  }
  arr = arr.join(" ");
  return arr;
};
```

하지만 여기서 좀더 개선되는 방법을 생각해보자면 숫자 1은 js의 문법 `toUpperCase`와 `toLowerCase`를 사용해도 똑같이 1로 고정이 됨을 확인할 수 있었고 알파벳을 구분할 필요 없이 그냥 맨앞글자는 대문자로 뒤에 글자는 소문자로 치환만 해주면 된다는 사실을 확인할 수 있었습니다. 아래는 개선된 최종 코드입니다.

## 5️⃣ 최종 소스코드

```js
const solution = (s) => {
  let answer = "";
  for (let i = 0; i < s.length; i++) {
    if (i === 0 || s[i - 1] === " ") {
      answer += s[i].toUpperCase();
    } else {
      answer += s[i].toLowerCase();
    }
  }
  return answer;
};
```

## 6️⃣ 사용 문법

- [charCodeAt](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt){:target="\_blank"}
- [toUpperCase](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase){:target="\_blank"}
- [toLowerCase](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase){:target="\_blank"}

## 7️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
