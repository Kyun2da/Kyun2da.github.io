---
layout: post
title: "express https 설정하기"
subtitle: "아마존 EC2에 express https 설정하기"
date: 2020-10-01 23:30:00
author: "Kyun2da"
#header-style: text
header-img: "img/post-bg-web.jpg"
tags:
  - backend
  - AWS
  - EC2
  - https
---

## 1️⃣서론

이 글은 2020-10-01을 기준으로 작성된 문서입니다. 라이브러리 업데이트 등으로 내용이 다를 수 있다는 점을 주의해 주시기 바랍니다.

- [Let's Encrypt](https://letsencrypt.org/ko/)
- [Greenlock](https://git.rootprojects.org/root/greenlock-express.js.git)

을 참조해주시면 감사하겠습니다.

그럼 시작하겠습니다.😄

## 2️⃣https란?

먼저 https를 설정하기 전에 https의 정의에 대하여 나무위키 참조를 통해 간단하게 짚고 넘어가고자 합니다.

TLS를 사용해 암호화된 연결을 하는 HTTP를 HTTPS(HTTP Secure)라고 하며, 웹사이트 주소는 http://가 아닌 https://로 시작됩니다.

기본 포트는 80번이 아닌 443번을 씁니다.

이를 사용함으로 써 암호화, 증명서, 완전성 보호를 이용할 수 있게되어 보안성이 증가한 웹페이지가 탄생하게 되었습니다.

하지만, `SSL 인증서를 발급받아야되서 비용이 비싸다는 단점`이 있었습니다..

`Let's Encrypt`가 등장하기 전까지 말이죠..😄

그래서 우리는 이제 무료로 https를 사용할 수 있게 되었습니다.

그렇다면 어떻게 인증서를 발급받을 수 있을까요?

## 3️⃣SSL 인증서 발급받기

Let's Encrypt 사이트에 가보면 [링크](https://letsencrypt.org/ko/docs/client-options/)에 많은 언어마다 지원하는 라이브러리가 있는 것을 볼 수 있습니다. 보통 certbot을 사용하곤 하는데요.

하지만 여기서는 서버에 접속하여 터미널로 발급을 받을 수 있도록 터미널을 사용해 보도록 하겠습니다.

서버 os 는 `ubuntu`를 사용한 점을 주의 해주세요.

1. git과 파이썬을 설치합니다.( let's encrypt는 python 2.7을 선호한다고 합니다.)

   ```console
   $sudo apt-get install git python2.7
   ```

2. 그 후 홈 디렉토리로 이동하여 letsencrypt git을 clone 합니다.

   ```console
   $sudo git clone https://github.com/letsencrypt/letsencrypt
   ```

3. python 코드를 실행합니다.

   ```console
   $cd letsencrypt
   $./letsencrypt-auto certonly
   ```

4. 그 다음 여러가지 환경 설정을 해주어야 하는데요
   standalone 을 선택했고 약관 동의(A)를 하였으며 연락받을 이메일을 적으시면 됩니다.

그리고 등록해놓은 도메인을 입력하시면 설정에 성공하게 됩니다.

## 4️⃣node.js 적용시키기

[Greenlock](https://git.rootprojects.org/root/greenlock-express.js.git)

링크에 가시면 `greenlock`을 통해 express에서 https 서버를 사용하실 수 있습니다.

링크에 가셔서 변경된 부분이 있는 지 확인하시고 `메뉴얼을 따라하시는 것을 추천`드립니다.

여기서는 간단하게 `과정만 설명`해보도록 하겠습니다.

1. 먼저 Greenlock을 설치해 줍니다.

   ```console
   npm install --save greenlock-express@v4
   ```

2. app.js에 다음과 같은 코드를 입력합니다.

   ```js
   require("greenlock-express")
     .init({
       packageRoot: __dirname,
       configDir: "./greenlock.d",

       // contact for security and critical bug notices
       maintainerEmail: "jon@example.com",

       // whether or not to run at cloudscale
       cluster: false,
     })
     // Serves on 80 and 443
     // Get's SSL certificates magically!
     .serve(app);
   ```

3. `.greenlockrc` 와 `greenlock.d/config.json` 파일을 생성합니다.

   1. .greenlockrc엔 다음과 같은 코드를 삽입합니다.

      ```js
      {"manager":{"module":"@greenlock/manager"},"configDir":"greenlock.d"}
      ```

   2. greenlock.d/config.json에는 데이터베이스를 대체하기 때문에 다음과 같이 보일 것 입니다.

      ```js
      { "defaults": { "subscriberEmail": "john.doe@example.com" }, "sites": [] }
      ```

4. 도메인을 추가합니다.

   ```console
   npx greenlock add --subject example.com --altnames example.com
   ```

   위와 같이 설정하시고 서버를 실행시켜보면, `자물쇠 모양이 주소 왼편`에 생긴다면 성공한 것입니다.

## 5️⃣ 참조

- [alskt0419님의 블로그 Node.js 쉽게 https 적용 시키는법](https://velog.io/@alskt0419/Node.js-%EC%89%BD%EA%B2%8C-https-%EC%A0%81%EC%9A%A9-%EC%8B%9C%ED%82%A4%EB%8A%94-%EB%B2%95)
- [Greenlock git](https://git.rootprojects.org/root/greenlock-express.js.git)
- [Let's Encrypt](https://letsencrypt.org/ko/)

## 6️⃣ 마치며..

ubuntu 서버와 Node.js express에서 https를 적용하는 방법에 대하여 알아보았습니다.
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
