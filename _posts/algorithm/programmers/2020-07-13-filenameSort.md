---
layout: post
title: "[프로그래머스/Javascript] 파일명 정렬"
subtitle: "알고리즘"
date: 2020-07-13 17:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
---

## 1️⃣서론

프로그래머스 level2 문제 `파일명 정렬`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/17686){:target="\_blank"}

## 2️⃣문제 설명

![파일명 정렬1](/img/algorithm/filenameSort1.png)
![파일명 정렬2](/img/algorithm/filenameSort2.png)

## 3️⃣풀이

이 문제는 파일 명을 `HEAD, NUMBER, TAIL` 로 분리하여 나누는 것입니다. 그 뒤로 `HEAD와 NUMBER`순으로 정렬해야합니다.
주의할 점이 몇가지 있습니다.

1. 파일명은 대문자와 소문자를 구분하지 않는다.
2. 숫자는 0부터 99999가 될 수있다.
3. 숫자는 01과 1은 같은 수로 친다.
4. 모두 같다면 정렬 후에도 두 파일의 순서가 바뀌어서는 안된다. (안정정렬)

이를 유의해서 풀어야 모두 solve를 받을 수 있었습니다. 그럼 코드를 살펴보겠습니다.

## 4️⃣ 내가 푼 소스코드

```js
const solution = (files) => {
  let answer = [];
  const arr = [];
  for (let i = 0; i < files.length; i++) {
    const value = files[i].split(/(\d+)/g);
    const file = files[i];

    //1번째 유의사항 해결
    const head = value[0].toUpperCase();
    let number = value[1];
    // 2번째 유의사항 해결
    if (number.length > 5) {
      number = number.substring(0, 5);
    }
    // 3번째 유의사항 해결
    number = Number(number);
    arr.push({ file: file, head: head, number: number, idx: i });
  }
  //정렬
  arr.sort((a, b) => {
    if (a.head < b.head) return -1;
    else if (a.head > b.head) return 1;
    else {
      if (a.number > b.number) return 1;
      else if (a.number < b.number) return -1;
      else {
        //4번째 유의사항 해결
        if (a.idx < b.idx) return -1;
        else return 1;
      }
    }
  });
  //답 구하기
  for (let i = 0; i < arr.length; i++) {
    answer.push(arr[i].file);
  }
  return answer;
};
```

## 5️⃣ 결론

정규표현식을 활용하면 문제를 보다 손쉽게 풀 수 있었습니다. 아직 정규표현식에 대해 공부한적이 없어서 해당 정규표현식을 찾느라 고생을 많이 했습니다. 정규표현식의 필요성에 대해 느끼게 되었고 이렇게 지켜야할 규칙이 많은 문제는 꼼꼼함이 중요하다는 것을 다시 한 번 깨닫게 되었던 것 같습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
