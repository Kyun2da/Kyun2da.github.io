---
layout: post
title: "[프로그래머스/Javascript] 수식 최대화"
subtitle: "알고리즘"
date: 2020-07-12 20:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
---

## 1️⃣서론

프로그래머스 level2 문제 `수식 최대화`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/67257){:target="\_blank"}

## 2️⃣문제 설명

![수식 최대화1](/img/algorithm/maximumEquation1.png)
![수식 최대화2](/img/algorithm/maximumEquation2.png)
![수식 최대화3](/img/algorithm/maximumEquation3.png)

## 3️⃣풀이

이 문제는 카카오 인턴십 2020문제입니다. `+, -, *`로 나타낼 수 있는 수식의 가짓수는 6가지이므로 완전탐색을 통하여 모든 경우의 수를 구해
절댓값이 가장 큰 값을 리턴하면 되는 문제였습니다. 이 문제의 key Point는 `어떻게 기호의 우선순위대로 계산을 해서 답을 도출하느냐`가 가장중요한 부분이 아니었나 싶습니다. 제가 푼 풀이 방법은 다음과 같습니다.

1. 먼저 수식을 기호와 숫자로 나눈다.
2. 배열과 수식을 복사하여 각 수식 우선순위마다 계산을 도출한다.
3. 계산 후에 최댓값과 계속 비교하여 최댓값을 찾는다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (expression) => {
  const arr = [
    ["+", "-", "*"],
    ["+", "*", "-"],
    ["-", "+", "*"],
    ["-", "*", "+"],
    ["*", "+", "-"],
    ["*", "-", "+"],
  ];

  //1. 수식을 숫자(num)과 기호(sign)으로 나눈다.
  let num = expression.split(/[^0-9]/);
  num = num.map((it) => {
    return parseInt(it);
  });
  const sign = [];
  for (let i = 0; i < expression.length; i++) {
    if (
      expression[i] === "*" ||
      expression[i] === "+" ||
      expression[i] === "-"
    ) {
      sign.push(expression[i]);
    }
  }

  let maxNum = 0;
  for (let i = 0; i < arr.length; i++) {
    //2. 배열과 수식을 복사한다.
    const copyNum = num.slice();
    const copySign = sign.slice();
    for (let j = 0; j < arr[i].length; j++) {
      for (let k = 0; k < copySign.length; k++) {
        if (copySign[k] === arr[i][j]) {
          if (copySign[k] === "*") {
            copyNum[k] *= copyNum[k + 1];
            copyNum.splice(k + 1, 1);
            copySign.splice(k, 1);
            k--;
          } else if (copySign[k] === "+") {
            copyNum[k] += copyNum[k + 1];
            copyNum.splice(k + 1, 1);
            copySign.splice(k, 1);
            k--;
          } else {
            copyNum[k] -= copyNum[k + 1];
            copyNum.splice(k + 1, 1);
            copySign.splice(k, 1);
            k--;
          }
        }
      }
    }
    //3. 계산후에 최댓값과 비교하여 최댓값을 찾는다.
    if (Math.abs(copyNum[0]) >= maxNum) {
      maxNum = Math.abs(copyNum[0]);
    }
  }
  return maxNum;
};
```

## 5️⃣ 결론

level2 지만 구현력을 상당히 요구하는 문제였습니다. 2020 인턴십 시험을 볼때는 테스트 케이스 몇개를 통과하지 못했었는데 다시 문제가 등록되고 나서 풀어보니 무사히 테스트케이스를 전부 통과할 수 있었습니다. 숫자와 수식을 분리하자는 아이디어만 쉽게 떠올릴 수 있다면 그렇게 헤맬필요가 없었는데 인턴십때는 완벽하게 통과하지 못했던 것이 아쉽습니다. 좀더 노력해야할 것 같습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
