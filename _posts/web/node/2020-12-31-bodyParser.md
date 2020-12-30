---
layout: post
title: "Express로 서버 구성하기 (body-parser) - 6"
date: 2020-12-31 01:00:00
author: "Kyun2da"
header-style: text
tags:
  - 서버
  - Node.js
  - Express
---

## 1️⃣ 서론

안녕하세요. 오늘은 Express 미들웨어 중 하나인 body-parser 미들웨어에 대해 알아보려고 합니다.

## 2️⃣ body-parser 모듈 설치

```bash
npm install body-parser
```

다음과 같은 명령어로 body-parser 모듈을 설치해 줍니다.

시작하기 전에 [공식 홈페이지](https://github.com/expressjs/body-parser#readme)를 읽으시는 것도 추천드립니다.

## 3️⃣ 간단한 예제

```js
import bodyParser from "body-parser";

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));
```

이렇게 쓰면 JSON 형식으로 { name: 'kyun2da' , subject: 'nodejs' }를 본문으로 보낸다면 req.body에 그대로 들어가게 됩니다.

하지만 4.17.1 버전 기준으로는 Express 모듈에 bodyParser가 내장되어 있어서

```js
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
```

다음과 같은 코드로 body-parser 기능을 구현할 수 있습니다.

이제 서버에서 req.body 로 해석된 본문을 받으실 수 있습니다.

## 4️⃣ 정리

최신 문법에서는 body-parser가 필요없지만 위의 문법들을 아는정도로는 좋은 것 같습니다.

다음 시간에는 본격적으로 라우터들을 활용하여 요청을 전달받고 보내는 방법에 대해 알아보겠습니다.

읽어주셔서 감사합니다.

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
