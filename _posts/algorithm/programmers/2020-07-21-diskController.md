---
layout: post
title: "[프로그래머스/Javascript] 디스크 컨트롤러"
subtitle: "알고리즘"
date: 2020-07-21 18:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - Heap
---

## 1️⃣서론

프로그래머스 level3 문제 `디스크 컨트롤러`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/42627){:target="\_blank"}

## 2️⃣문제 설명

![디스크 컨트롤러1](/img/algorithm/diskController1.png)
![디스크 컨트롤러2](/img/algorithm/diskController2.png)
![디스크 컨트롤러3](/img/algorithm/diskController3.png)

## 3️⃣풀이

이 문제는 `우선순위 큐`를 통해 해결할 수 있습니다.  
문제의 핵심은 어떤 순서로 작업을 실행해야 가장 최소의 평균시간을 구할 수 있나입니다.

1. `하드디스크가 작업을 수행하고 있지 않을 때에는 먼저 요청이 들어온 작업부터 처리합니다.` 라고 써있으므로 먼저 요청의 시간순으로 jobs를 정렬해야합니다.
2. 그러나 요청의 시간순으로 처리하면 문제의 예처럼 최소시간을 보장하지 못합니다. 여기서 필요한 것이 중간단계의 `우선순위 큐`입니다.
3. 우선순위 큐에는 해당작업을 처리하는동안 요청이 오는 모든 jobs들을 넣어줍니다. 예를 들어 0초부터3초까지의 작업을하는 하나의 작업이 있다고하면 0,1,2,3초에 요청이 온 모든 작업을 우선순위 큐에 넣어줍니다.
4. 그리고 작업이 끝나면 `우선순위 큐에있는 작업중 가장 처리시간이 작은 작업부터 실행`해줍니다. 이것이 최소시간을 만족하는 방법이기 때문입니다.
5. 이런식으로 작업은 jobs의 작업들이 모두 끝날때 까지 계속됩니다.
6. 마지막으로 `주의할 점은 우선순위 큐가 다 비고나서 작업이 아직 남아있다면 jobs의 첫번째 배열에있는 작업을 실행해주면됩니다. 즉 요청의 시간순으로 다시 실행해 주면 된다는 뜻입니다.`

그럼 소스코드를 보겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (jobs) => {
  let answer = 0,
    j = 0,
    time = 0;
  jobs.sort((a, b) => {
    return a[0] - b[0];
  });

  const priorityQueue = [];
  while (j < jobs.length || priorityQueue.length !== 0) {
    if (jobs.length > j && time >= jobs[j][0]) {
      priorityQueue.push(jobs[j++]);
      priorityQueue.sort((a, b) => {
        return a[1] - b[1];
      });
      continue;
    }
    if (priorityQueue.length !== 0) {
      time += priorityQueue[0][1];
      answer += time - priorityQueue[0][0];
      priorityQueue.shift();
    } else {
      time = jobs[j][0];
    }
  }
  return parseInt(answer / jobs.length);
};
```

## 5️⃣ 결론

자바스크립트는 우선순위 큐가 구현되어 있지않아서 직접적으로 정렬을 해주어야 하는 문제가 있었습니다. 코드는 비교적 짧게 나왔지만 시간복잡도 상으로 보았을 때 이 답이 최적의 답인지는 잘 모르겠습니다. 혹시 시간복잡도가 더 짧게 구현하는 방법이 있다면 알려주시면 감사하겠습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
