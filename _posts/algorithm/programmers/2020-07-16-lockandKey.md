---
layout: post
title: "[프로그래머스/Javascript] 자물쇠와 열쇠"
subtitle: "알고리즘"
date: 2020-07-16 18:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 배열
---

## 1️⃣서론

프로그래머스 level3 문제 `자물쇠와 열쇠`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/60059){:target="\_blank"}

## 2️⃣문제 설명

![자물쇠와열쇠](/img/algorithm/lockandKey1.png)
![자물쇠와열쇠](/img/algorithm/lockandKey2.png)

## 3️⃣풀이

이 문제는 배열을 얼마나 잘 활용하는지 묻는 문제입니다. 키를 회전시키거나 이동시켜서 자물쇠에 맞춰 자물쇠를 푸는 것입니다. 키를 회전시키는 경우는 4가지가 있고 자물쇠의 배열도 최대 20행,열이 가능하므로 완전탐색으로 해결이 가능합니다. 자물쇠의 상하좌우를 자물쇠 크기만큼 늘리고 키를 회전시키거나 이동해가며 자물쇠에 맞춰보고 자물쇠가 모두 1로 채워지면 답이 되므로 true를 리턴하면 됩니다. 단 1이 겹치는 경우엔 키를 넣을 수 없으므로 1과 1이 만날땐 2로 대체합니다. 그림으로 보자면 다음과 같습니다.

![자물쇠와열쇠](/img/algorithm/lockandKey3.png)

이제 소스코드를 보겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
//키를 회전하는 함수
const rotationKey = (key) => {
  const len = key.length;
  const ret = Array.from(Array(len), () => Array(len).fill(null));
  for (let i = 0; i < len; ++i) {
    for (let j = 0; j < len; ++j) {
      ret[i][j] = key[len - j - 1][i];
    }
  }
  return ret;
};

//답인지 검사하는 함수
const isAnswer = (newLock, len) => {
  for (let i = len; i < len * 2; i++) {
    for (let j = len; j < len * 2; j++) {
      if (newLock[i][j] !== 1) {
        return false;
      }
    }
  }
  return true;
};
const solution = (key, lock) => {
  let answer = true;
  const len = lock.length;
  const arr = Array.from(Array(len * 3), () => Array(len * 3).fill(null));

  for (let i = len; i < len * 2; i++) {
    for (let j = len; j < len * 2; j++) {
      arr[i][j] = lock[i - len][j - len];
    }
  }
  //키를 회전 시키면서 탐색
  for (let i = 0; i < 4; i++) {
    key = rotationKey(key, i);
    //키를 이동시키면서 탐색
    for (let j = 0; j <= arr.length - key.length; j++) {
      for (let k = 0; k <= arr[0].length - key[0].length; k++) {
        const newLock = arr.map(function (arr) {
          return arr.slice();
        });
        for (let m = 0; m < key.length; m++) {
          for (let n = 0; n < key.length; n++) {
            if (newLock[j + m][k + n] === 1 && key[m][n] === 1) {
              //키가 둘다 1이면 2로바꿈 -> 답이 될수 없음
              newLock[j + m][k + n] = 2;
            } else if (newLock[j + m][k + n] === 1 && key[m][n] === 0) {
              newLock[j + m][k + n] = 1;
            } else {
              newLock[j + m][k + n] = key[m][n];
            }
          }
        }
        if (isAnswer(newLock, len)) {
          return true;
        }
      }
    }
  }
  return false;
};
```

## 5️⃣ 결론

배열을 활용하는 문제였는데 level3 치고는 어려웠던 문제가 아니었나 싶습니다. 블라인드 코딩테스트에서도 정답률이 7%대로 낮았습니다. 자바스크립트로 아직 배열을 다루는것이 익숙하지 않아서 2차원 배열을 만드는 함수를 찾고 회전하는 방법을 검색을 통해 알아냈습니다. 배열을 활용하는 것에 대하여 조금더 연습을 해야할 것 같습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
