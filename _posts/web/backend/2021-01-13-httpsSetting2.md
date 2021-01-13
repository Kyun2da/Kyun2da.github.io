---
layout: post
title: 'Linux 서버 https 세팅 - Node.js Express'
subtitle: Linux 환경 Let'sEncrypt로 https 연결하기
date: 2021-01-13 22:00:00
author: 'Kyun2da'
header-style: text
tags:
  - backend
  - linux
  - https
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ https 설정하기를 두번 쓰게된 이유

이전에 [express https 설정하기](https://kyun2da.github.io/2020/10/01/httpsSetting/) 포스팅에서 https 설정하는 방법을 다뤘었는데요.

그 때는 Greenlock-Express를 사용하여 Express의 https 세팅을 하곤했습니다.

하지만 pm2로 cluster 모드로 실행하였을 때 문제가 생기는 것을 발견하였고 (물론 [해결책](https://stackoverflow.com/questions/61550683/should-i-use-node-js-greenlock-express-with-cluster-mode-at-the-same-time-im-us)이 있었지만 어떻게 하는지 잘 모르겠어서 방법 변경) 방법을 찾던 중에 greenlock-express를 사용하지 않고 https 세팅하는 방법을 찾아서 해결하였습니다.

그래서 다음에 https 세팅할때 봐두고자 다시 한번 포스팅을 남겨두려고 합니다.

## 2️⃣ 준비물

1. 80포트와 443포트가 열려있어야 합니다.
2. 구매한 도메인이 준비되어 있어야 합니다. 도메인을 구매했으면 IP주소를 A포트로 도메인 연결을 해놓으면 됩니다. Let's Encrypt는 IP주소로는 인증서를 발급해주지 않는다고 합니다.
3. 서버 코드 : 기본적인 Express 서버코드가 준비되어 있어야 합니다. 응답을 받을 정도면 됩니다.
4. 현재 80포트나 443포트에 서버가 켜져있다면 서버를 끄고 진행합니다.

## 3️⃣ SSL 인증서 발급받기

이전에도 진행했었던 Let's Encrypt를 이용해 다시한번 서버에 인증서를 받아보도록 하겠습니다.

설치 순서

```console
sudo snap install --classic certbot
```

위 명령어를 통해 리눅스에 letsencrypt SSL 인증서를 받는 certbot을 설치해줍니다.

저는 Apache나 Nginx를 쓰지 않으므로 Web Server가 따로 없는 --standalone 형식을 사용하도록 하겠습니다.

```console
sudo certbot certonly --standalone
```

그리고 여러가지 약관동의(A)를 누르시고, 연락받을 이메일 주소와 등록해놓은 도메인등을 적은 후 OK 하면
`Congratulations!...` 이라는 문서가 뜨면서 성공처리가 됩니다.

그럼 `/etc/letsencrypt/live/` 해당 경로에 방금 전 적은 도메인 이름의 폴더 안에 여러가지 인증 문서 .pem파일이 있는 것을 확인하실 수 있습니다.

## 4️⃣ Express 적용하기

보통 앱이라면 app.js에서 listen을 하고 있을 것입니다. 이제 listen을 따로 server.js로 빼보도록 하겠습니다.

제 server.js 쪽 코드는 이러합니다.

```js
const app = require('./app');
const https = require('https');
const fs = require('fs');
const prod = process.env.NODE_ENV === 'production';

if (prod) {
  const options = {
    ca: fs.readFileSync('/etc/letsencrypt/live/도메인주소/fullchain.pem'),
    key: fs.readFileSync('/etc/letsencrypt/live/도메인주소/privkey.pem'),
    cert: fs.readFileSync('/etc/letsencrypt/live/도메인주소/cert.pem'),
  };
  https.createServer(options, app).listen(443, () => {
    console.log('443번 포트에서 대기중입니다.');
  });
} else {
  app.listen(app.get('port'), () => {
    console.log(app.get('port'), '번 포트에서 대기중');
  });
}
```

이런 식으로 server.js에 코드를 빼서 개발모드와 production 모드에서 따로 동작하도록 해놨습니다.

위에있는 옵션이라는 객체로 인증서 파일을 불러와 https 세팅을 해주는 것입니다.

이렇게 되면 홈페이지 주소 왼쪽에 자물쇠가 잠겨있는 것을 볼 수 있습니다.

## 5️⃣ crontab을 이용하여 인증서 자동 갱신 하기

리눅스의 작업 예약 스케줄러인 cron을 통해 인증서를 자동으로 갱신해주도록 합시다.

let's Encrypt의 기본 인증 기간은 3개월입니다. 따라서 3개월마다 인증서를 자동 갱신해주어야 하는데요.

이 작업을 cron을 통해 실행해보도록 하겠습니다.

먼저 cron을 설치합니다.

```console
# cron 설치
sudo apt update -y
sudo apt install -y cron

# cron 시작
sudo service cron start

# cron systemctl 활성화
sudo systemctl enable cron.service

# cron systemctl 등록 확인
sudo systemctl list-unit-files | grep cron
sudo service cron status
```

다음과 같이 cron을 설치한 후에 cron을 등록해줍니다.

```console
# crontab에 등록하기
sudo crontab -e

# 2개월마다 1일에 인증서를 갱신하고 pm2로 서버를 재시작 하겠다는 뜻
0 0 1 */2 * /usr/bin/certbot renew --renew-hook="sudo pm2 restart app"

# 잘 등록되었는지 목록 확인
sudo crontab -l

# crontab 실행 로그 확인
view /var/log/syslog
```

## 6️⃣ 참고

- [NodeJS - (보안) https 설정 ( Nodejs+letsencrypt )](https://velog.io/@neity16/EC2-https%EC%84%A4%EC%A0%95Nodejsletsencrypt)
- [Crontab 설치 및 사용법](https://blog.secuof.net/27)
- [How to Setup Let’s Encrypt (Certbot) on Ubuntu 20.04](https://tecadmin.net/how-to-setup-lets-encrypt-on-ubuntu-20-04/)
- [nginx와 let's encrypt로 SSL 적용하기(+자동 갱신)](https://www.zerocho.com/category/NodeJS/post/5ef450a5701d8a001f84baeb)

## 7️⃣ 마치며

오늘은 let's Encrypt를 이용하여 https 설정을 하는 것을 해보았습니다.

예전부터 이 부분이 많이 헷갈리고 어려웠었는데 오늘에서야 그 마침표를 찍은 것 같습니다.

만약 잘못된 점이 있거나 궁금한점이 있다면 아래 댓글창으로 질문 부탁드립니다.

읽어주셔서 감사합니다.
