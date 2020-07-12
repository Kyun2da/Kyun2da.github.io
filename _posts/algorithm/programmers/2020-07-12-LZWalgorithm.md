---
layout: post
title: "[프로그래머스/Javascript] 압축"
subtitle: "알고리즘"
date: 2020-07-12 22:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - LZW알고리즘
---

## 1️⃣서론

프로그래머스 level2 문제 `압축`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/17684){:target="\_blank"}

## 2️⃣문제 설명

![압축1](/img/algorithm/lzwAlgorithm1.png)
![압축2](/img/algorithm/lzwAlgorithm2.png)
![압축3](/img/algorithm/lzwAlgorithm3.png)

## 3️⃣풀이

이 문제는 대표적인 압축기법인 lzw 알고리즘을 구현하는 예제입니다. 예전에 멀티미디어 과목에서 이 알고리즘을 배운적이 있어서 원리는 쉽게 이해할 수 있었고, 구현하는 것이 좀 어려웠는데 다행히 잘 해결할 수 있었습니다. 문자열을 순회하며 사전에 문자열이 있는지 검사하며 압축을 하는 알고리즘을 구현해보았습니다. 코드는 다음과 같습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (msg) => {
  const arr = [];

  //A부터 Z까지 미리 사전에 등록해 놓는다.
  for (let i = "A".charCodeAt(0); i <= "Z".charCodeAt(0); i++) {
    arr.push(String.fromCharCode(i));
  }

  const answer = [];
  let i = 0;
  //문자열을 순회하며 사전에 있으면 다음 문자열로 확장하며 사전에 등록하는 방식을 이용한다.
  while (i < msg.length) {
    let j = 1;
    //문자열이 없을때까지 찾는다.
    while (arr.indexOf(msg.substring(i, i + j)) !== -1 && i + j <= msg.length) {
      j++;
    }
    //없는 문자열을 사전에 등록
    arr.push(msg.substring(i, i + j));
    //현재 입력을 사전의 색인번호로 답에 추가한다.
    answer.push(arr.indexOf(msg.substring(i, i + j - 1)) + 1);
    i += j - 1;
  }
  return answer;
};
```

## 5️⃣ 결론

LZW 알고리즘을 알고 있었다면 이해하기에 쉬웠고 구현력을 요구하는 문제였습니다. 카카오는 보통 특별한 알고리즘을 요구하기 보다는 구현력을 요구하는 문제가 많은 것 같습니다. 그래도 점점 많은 문제를 풀어가며 구현력이 늘어가는 것 같아 뿌듯하기도 합니다. 앞으로 좀더 알고리즘을 열심히 공부해야겠습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
