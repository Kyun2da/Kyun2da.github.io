---
layout: post
title: "[프로그래머스/Javascript] 베스트앨범"
subtitle: "알고리즘"
date: 2020-07-24 18:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 해시
---

## 1️⃣서론

프로그래머스 level3 문제 `베스트앨범`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/42579){:target="\_blank"}

## 2️⃣문제 설명

![베스트앨범1](/img/algorithm/bestAlbum1.png)
![베스트앨범2](/img/algorithm/bestAlbum2.png)

## 3️⃣풀이

이 문제는 장르별로 가장 많이 재생된 노래를 두개씩 모아 앨범을 만드는 문제입니다. 풀이는 다음과 같습니다.

1. 먼저 장르별로 노래를 분리한다.
2. 그 후 분리한 노래의 시간을 장르마다 합쳐서 시간이 많은 순서대로 장르를 정렬한다.
3. 이제 각각의 장르들의 노래를 시간 순서대로 정렬한다.
4. 이제 장르들을 돌면서 시간이 가장 많은 순서대로 두개씩 뽑아 인덱스를 답에 추가한다.

## 4️⃣ 내가 푼 소스코드

```js
const sum = (a) => {
  return a.reduce((acc, cur) => {
    return acc + cur[0];
  }, 0);
};

const solution = (genres, plays) => {
  const answer = [];
  const genre = [];
  const play = [];

  //장르별로 노래를 묶어서 추가한다.
  for (let i = 0; i < genres.length; i++) {
    if (genre.includes(genres[i])) {
      //console.log(genre);
      const idx = genre.indexOf(genres[i]);
      play[idx].push([plays[i], i]);
    } else {
      genre.push(genres[i]);
      play.push([[plays[i], i]]);
    }
  }

  //장르별 시간합을 기준으로 정렬
  play.sort((a, b) => {
    return sum(b) - sum(a);
  });

  //장르별 노래들을 시간순으로 정렬
  for (let i = 0; i < play.length; i++) {
    play[i].sort((a, b) => {
      return b[0] - a[0];
    });
  }

  //장르별 노래를 두개씩 뽑아 답에 추가
  for (let i = 0; i < play.length; i++) {
    for (let j = 0; j < play[i].length; j++) {
      if (j === 2) break;
      answer.push(play[i][j][1]);
    }
  }
  return answer;
};
```

## 5️⃣ 결론

해시를 이용해 답을 구하는 문제입니다. 해시 문제를 처음 풀어봤는데 대학교 알고리즘 수업 때 배운적이 있어서 비교적 쉽게 풀 수 있었던 것 같습니다. 해시의 핵심은 그룹화를 하는 것인데 배열로 그룹화를 잘 구현한 것 같습니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
