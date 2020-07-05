---
layout: post
title: "[프로그래머스/Javascript] 방금그곡"
subtitle: "알고리즘"
date: 2020-07-05 18:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-rwd.jpg"
tags:
  - Algorithm
  - 프로그래머스
  - 구현력
---

## 1️⃣서론

프로그래머스 level2 문제 `방금그곡`입니다.
`Javascript`를 이용하여 해결하였습니다.

- [출처](https://programmers.co.kr/learn/courses/30/lessons/17683){:target="\_blank"}

## 2️⃣문제 설명

![방금그곡1](/img/algorithm/recentSong1.png)
![방금그곡2](/img/algorithm/recentSong2.png)

## 3️⃣풀이

이 문제는 문자열을 이용하는 문제입니다. 독특한 점이 있다면 음계라는 것을 사용했다는 것인데 `#`이 들어간 음계를 한 글자의 음계로 표현한다면 문자열 찾기 문제가 되어 그리 어렵지만은 않았던 문제 입니다. 핵심은 `#`이 들어간 음계를 어떻게 처리할 것이냐 였던 것 같습니다.

## 4️⃣ 내가 푼 소스코드

```js
//이노래가 답의 후보가 될 수 있는지 찾는 함수
const isThisSong = (timeDiff, lyrics, findString) => {
  const newM = findString
    .replace(/(C#)/g, "c")
    .replace(/(D#)/g, "d")
    .replace(/(F#)/g, "f")
    .replace(/(G#)/g, "g")
    .replace(/(A#)/g, "a");

  const newMusicInfos = lyrics
    .replace(/(C#)/g, "c")
    .replace(/(D#)/g, "d")
    .replace(/(F#)/g, "f")
    .replace(/(G#)/g, "g")
    .replace(/(A#)/g, "a");

  let str = "";
  const repeatCount = parseInt(timeDiff / newMusicInfos.length);
  if (repeatCount === 0) {
    str = newMusicInfos.substring(0, timeDiff);
  } else {
    str =
      newMusicInfos.repeat(repeatCount) +
      newMusicInfos.substring(0, timeDiff - newMusicInfos.length * repeatCount);
  }
  //console.log(str);
  if (str.indexOf(newM) !== -1) {
    return 1;
  }
  return 0;
};

//시간을 계산하는 함수
const calculateTime = (st_time, ed_time) => {
  return (
    (parseInt(ed_time.substring(0, 2)) - parseInt(st_time.substring(0, 2))) *
      60 +
    parseInt(ed_time.substring(3)) -
    parseInt(st_time.substring(3))
  );
};

const solution = (m, musicinfos) => {
  //답이 될 수 있는 후보를 고른다.
  let songCandidates = [];
  for (let i = 0; i < musicinfos.length; i++) {
    const arr = musicinfos[i].split(",");
    const [st_time, ed_time, title, lyrics] = arr;
    const timeDiff = calculateTime(st_time, ed_time);
    if (isThisSong(timeDiff, lyrics, m)) {
      songCandidates.push([title, timeDiff]);
    }
  }

  //답을 구한다. 0일경우 none 출력, 1일경우 배열에있는 제목 출력, 나머지는 가장 시간이 긴 제목 출력
  if (songCandidates.length === 0) {
    return "(None)";
  } else if (songCandidates.length === 1) {
    return songCandidates[0][0];
  } else {
    let maxTime = 0;
    let answer = "";
    for (let i = 0; i < songCandidates.length; i++) {
      if (maxTime < songCandidates[i][1]) {
        maxTime = songCandidates[i][1];
        answer = songCandidates[i][0];
      }
    }
    return answer;
  }
};
```

## 5️⃣ 결론

음계를 하나의 글자로 치환하는 것만 안다면 그리 어려웠던 문제는 아니었던 것 같습니다. 다만 과정이 좀 길어져서 집중력이 좀 필요했던 것 같습니다. 저도 실수를 꽤 많이해서 어디가 틀렸는지 찾느라 고생했던 문제이기도 합니다. 감사합니다.

## 6️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
