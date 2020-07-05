---
layout: post
title: "[프로그래머스/Javascript] 뉴스 클러스터링"
subtitle: "알고리즘 - 문자열 다루기"
date: 2020-07-05 12:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 문자열
---

## 1️⃣서론

프로그래머스 level2 문제 `[1차] 뉴스 클러스터링`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/17677){:target="\_blank"}

## 2️⃣문제 설명

![클러스터링](/img/algorithm/clustering.png)

## 3️⃣풀이

처음에 자바스크립트의 Set을 이용해 풀다가 중복된 원소가 들어갈 수 있다는 것을 보고 Array로 변경하였다.
Array로 Set과 비슷하게 `합집합 교집합을 구하는 방식으로 구현`을 하였다. 원소는 알파벳만 들어갈 수 있으므로
넣을 때 알파벳만 푸시하도록 하였다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (str1, str2) => {
  //각각의 원소 쌍을 구하는 과정 Set으로 구현할 수 없어서 Array를 사용했다.
  str1 = str1.toUpperCase();
  str2 = str2.toUpperCase();
  const arr1 = new Array();
  const arr2 = new Array();

  //이부분이 str1과 str2가 겹치므로 함수로 따로 뺐어도 됐을 것 같다.
  for (let i = 0; i < str1.length - 1; i++) {
    const str = str1.substr(i, 2);
    if (str[0] >= "A" && str[0] <= "Z" && str[1] >= "A" && str[1] <= "Z") {
      arr1.push(str);
    }
  }
  for (let i = 0; i < str2.length - 1; i++) {
    const str = str2.substr(i, 2);
    if (str[0] >= "A" && str[0] <= "Z" && str[1] >= "A" && str[1] <= "Z") {
      arr2.push(str);
    }
  }

  //교집합과 합집합을 구하는 과정
  const intersection = [];
  const union = [];
  for (let i = 0; i < arr2.length; i++) {
    if (arr1.indexOf(arr2[i]) >= 0) {
      intersection.push(arr1.splice(arr1.indexOf(arr2[i]), 1));
    }
    union.push(arr2[i]);
  }

  for (let i = 0; i < arr1.length; i++) {
    union.push(arr1[i]);
  }
  if (intersection.length === 0 && union.length === 0) {
    return 65536;
  }
  return parseInt(65536 * (intersection.length / union.length));
};
```

## 5️⃣ 다른 사람의 소스코드

프로그래머스의 풀이를 보면 좀더 효율적인 코드를 발견할 수 있었는데 먼저 알파벳만 찾는 것에
`정규표현식`을 사용하였고 교집합과 합집합을 사용할때 `Set`을 사용했다는 것을 알 수 있었다.

```js
function solution (str1, str2) {
  
  //
  function explode(text) {
    const result = [];
    for (let i = 0; i < text.length - 1; i++) {
      const node = text.substr(i, 2);
      if (node.match(/[A-Za-z]{2}/)) {
        result.push(node.toLowerCase());
      }
    }
    return result;
  }

  const arr1 = explode(str1);
  const arr2 = explode(str2);
  const set = new Set([...arr1, ...arr2]);
  let union = 0;
  let intersection = 0;

  //같은 원소를 검사해서 많은  쪽은 union에 더하고 적은쪽은 intersection에 더한다.
  set.forEach(item => {
    const has1 = arr1.filter(x => x === item).length;
    const has2 = arr2.filter(x => x === item).length;
    union += Math.max(has1, has2);
    intersection += Math.min(has1, has2);
  })
  return union === 0 ? 65536 : Math.floor(intersection / union * 65536);
}
```

## 6️⃣ 결론

이 문제는 문제의 원소쌍을 어떻게 구하고 그 원소쌍에 대한 합집합과 교집합을 어떻게 구해야 할지 `구현력이 요구`되는 문제였다.
그렇게 어려운 문제는 아니었지만 최적화를 시키는 것이 중요했던 것 같다.

## 7️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
