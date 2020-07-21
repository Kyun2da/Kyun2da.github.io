---
layout: post
title: "[프로그래머스/Javascript] 단어 변환"
subtitle: "알고리즘"
date: 2020-07-21 17:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - DFS/BFS
---

## 1️⃣서론

프로그래머스 level3 문제 `단어 변환`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/43163){:target="\_blank"}

## 2️⃣문제 설명

![단어변환](/img/algorithm/wordConversion.png)

## 3️⃣풀이

이 문제는 dfs/bfs를 활용하여 한 단어씩 변화하며 가장 최소의 경로 수를 찾는 문제입니다. 풀이 과정은 다음과 같습니다.

1. 필요한 자료구조는 내가 해당 단어를 방문했는지 확인하는 check배열과 답의 경로 수를 나타낼 answer입니다.
2. 재귀함수 dfs를 만들어줍니다. 답을 찾는 조건은 시작단어가 타겟단어와 같다면 해당 깊이를 return 해주면 됩니다.
3. 다음에 방문할 단어가 한글자 차이인지 확인하는 함수 diffOneLetters를 만듭니다.
4. 방문한 단어가 아니고 한글자 차이가 난다면 해당 단어를 dfs로 방문합니다. dfs가 끝나면 다음 재귀를 위해 해당 단어를 방문취소해주고 깊이도 하나 낮춰줍니다.
5. 이런식으로 재귀를 돌려 나올수 있는 가장 최소의 경로를 리턴합니다.

코드는 다음과 같습니다.

## 4️⃣ 내가 푼 소스코드

```js
let answer = 100;
let check = [];

const diffOneLetters = (begin, words) => {
  let diffNum = 0;
  for (let i = 0; i < begin.length; i++) {
    if (begin[i] !== words[i]) diffNum += 1;
  }
  if (diffNum === 1) return 1;
  return 0;
};

const dfs = (begin, target, words, depth, check) => {
  //시작단어가 타겟단어와 같다면 답은 depth이다.
  if (begin == target && answer > depth) {
    answer = depth;
    console.log(check);
    return;
  }
  for (let i = 0; i < words.length; i++) {
    //방문하지 않았고 단어의 차이가 한개라면 방문한다.
    if (!check[i] && diffOneLetters(begin, words[i])) {
      depth += 1;
      check[i] = true;
      dfs(words[i], target, words, depth, check);
      check[i] = false;
      depth -= 1;
    }
  }
};

const solution = (begin, target, words) => {
  if (!words.includes(target)) {
    return 0;
  }
  for (let i = 0; i < words.length; i++) check[i] = false;
  dfs(begin, target, words, 0, check);
  return answer === 100 ? 0 : answer;
};
```

## 5️⃣ 결론

dfs를 이용하여 단어를 방문하는 문제였습니다. 아직 재귀에 익숙하지 않은 것 같아 꽤나 시간이 걸렸던 문제입니다. 재귀에 익숙해지도록 노력해야할 것 같습니다. 감사합니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
