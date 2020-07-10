---
layout: post
title: "[프로그래머스/Javascript] 올바른 괄호"
subtitle: "알고리즘"
date: 2020-07-10 14:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 스택
---

## 1️⃣서론

프로그래머스 level2 문제 `올바른 괄호`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/12909){:target="\_blank"}

## 2️⃣문제 설명

![올바른 괄호](/img/algorithm/correctBracket.png)

## 3️⃣풀이

이 문제는 스택 개념만 알고있다면 쉽게 풀 수 있던 문제인 것 같습니다.  
괄호 문제는 대부분 스택으로 모두 해결이 가능합니다. 예전에 괄호 문제를 많이 풀어본터라 쉽게 해결할 수 있었습니다.  
그럼 코드를 살펴보도록 하겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (s) => {
  let answer = true;

  //스택을 간단하게 변수 하나로 생각
  let sum = 0;

  //for문을 돌면서 sum이 -값이되면 올바르지 않은 괄호
  //닫는괄호가 먼저 나올 수 없으므로
  for (let i = 0; i < s.length; i++) {
    if (s[i] === "(") {
      sum++;
    } else {
      sum--;
    }
    if (sum < 0) {
      return false;
    }
  }

  //괄호가 끝나지않았다면 올바르지 않은 괄호
  //+값이라면 여는괄호가 남아있고 -값이라면 닫는괄호가 남아있다는 뜻
  if (sum !== 0) {
    return false;
  }
  return true;
};
```

## 5️⃣ 결론

예전에 비슷한 문제를 풀 수 있어서 쉽게 풀 수 있었습니다. 어느덧 level2 문제를 거의 다 풀어가는데
좀더 실력 상승에 정진해야겠습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
