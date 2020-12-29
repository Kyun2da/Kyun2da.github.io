---
layout: post
title: "Express로 서버 구성하기 (cookie-parser) - 5"
date: 2020-12-29 14:00:00
author: "Kyun2da"
header-style: text
tags:
  - 서버
  - Node.js
  - Express
---

## 1️⃣ 서론

이번 시간엔 `cookie-parser` 모듈을 통해서 쿠키를 쉽게 추출하는 방법에 대하여 알아보도록 하겠습니다.

그 전에 쿠키에대한 개념이 명확하지 않으시다면 다음 [링크](https://kyun2da.github.io/2020/12/28/cookieSession/)를 통해 쿠키에 대해 배워보는 것도 좋을 것 같습니다.

그럼 시작하겠습니다.

## 2️⃣ Cookie-Parser 모듈 설치

다음과 같은 명령어로 cookie-parser 모듈을 설치해줍니다.

```bash
npm install cookie-parser
```

## 3️⃣ 간단한 예제

전 시간에 이어 쿠키파서를 import해주고 미들웨어에 추가합니다.

```js
import express from "express";
import { dirname } from "path";
import { fileURLToPath } from "url";
import morgan from "morgan";
import cookieParser from "cookie-parser"; // cookie-parser 모듈 import

const __dirname = dirname(fileURLToPath(import.meta.url));
const app = express();
const port = 3000;

app.use(cookieParser()); // cookieParser 미들웨어에 추가하기
app.use(morgan("dev"));
app.use("/static", express.static(__dirname + "/public"));

app.get("/", (req, res) => {
  res.send("Hello World!");
  console.log("Cookies : ", req.cookies); // 쿠키 조회 로그 찍기
});

app.listen(port, () => {
  console.log(`현재 앱이 http://localhost:${port} 에서 구동중입니다.`);
});
```

이 후 서버를 node app.js의 명령어로 실행시키면 쿠키가 터미널에 찍히는 것을 확인하실 수 있습니다.

실제로 이 쿠키는 브라우저에서 F12로 개발자모드에 들어간 후 Application 탭에 들어가서 쿠키를 눌러보면

로그와 동일한 쿠키가 있는 것을 보실 수 있습니다.

이처럼 cookie-parser의 기능은 요청에 동봉된 쿠키를 해석해 req.cookies 객체로 만드는 역할을 합니다.

## 4️⃣ 이외의 기능들

이밖의 기능들은 [공식 홈페이지](https://github.com/expressjs/cookie-parser#readme) 에서 확인이 가능합니다.

여기서 간단하게 소개해보자면, 쿠키에는 서명된 쿠키가 있는데요. 이러한 쿠키들은 `req.signedCookies`로 가져올 수 있습니다.

또한 cookie-parser의 기능은 아니지만 서버에서 쿠키를 만들거나 삭제할 때는 다음 코드와 같이 쓰기도 합니다.

```js
const days = 1;
// 쿠키 생성 코드
res.cookie("name", "kyun2da", {
  expires: new Date(Date.now() + days * 24 * 60 * 60 * 1000), // 쿠키의 만료일을 하루 뒤로 설정
  httpOnly: true,
  secure: true,
});

// 쿠키 삭제 코드
res.clearCookie("name", "kyun2da", {
  httpOnly: true,
  secure: true,
});
```

마지막으로 res.cookies의 옵션은 다음과 같습니다.

| 옵션 | 설명|
|maxAge|현재 시간으로부터 만료 시간을 밀리초(millisecond) 단위로 설정합니다.|
|expires|Cookie의 만료 날짜를 GMT 시간으로 설정합니다. 지정되어 있지 않거나 0으로 지정되어 있는 경우 session cookie를 생성합니다.|
|path|Cookie의 경로. 기본 경로는 "/"입니다.|
|domain|Cookie의 domain name입니다. 기본 domain name은 loaded입니다.|
|secure|HTTPS에서만 cookie를 사용할 수 있도록 합니다.|
|httpOnly|웹 서버를 통해서만 cookie에 접근할 수 있도록 합니다.|
|signed|cookie가 서명되어야 할 지를 결정합니다.|

오늘은 cookie-parser 모듈에 대해 알아보았습니다. 다음 시간에는 body-parser 모듈에 대해 알아보도록 하겠습니다.

읽어주셔서 감사합니다.

## 5️⃣ 마치며..

질문과 지적은 환영합니다. 이 문제는 최적의 정답일 수도 아닐수도 있습니다.  
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
