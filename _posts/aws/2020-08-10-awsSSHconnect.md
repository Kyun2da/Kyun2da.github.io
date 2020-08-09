---
layout: post
title: "[아마존/AWS] EC2 접속하기 with SSH"
subtitle: "EC2 SSH .pem 파일 없이 접속하기"
date: 2020-08-10 00:00:00
author: "Kyun2da"
#header-style: text
header-img: "img/aws/aws_company.jpg"
tags:
  - AWS
  - SSH
---

## 1️⃣서론

먼저 이 글은 `2020년 8월 10일`을 기준으로 작성한 글입니다. 추후에 이 글을 보신다면 변경된 부분일 수도 있다는 점을 감안해주시고
봐주시면 감사하겠습니다.  
이번 포스팅은 아마존에서 운영하는 `아마존 웹 서비스(AWS) EC2를 접속하는 방법`에 대해 살펴보려고 합니다.
아직 EC2를 만들지 않았다면 아래 동빈나 님의 서버 구축 강의를 보고 오시면 될 것 같습니다.

<iframe width="1280" height="720" src="https://www.youtube.com/embed/7-zwChaCYzA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

그럼 서버를 구축하였다는 가정하에 `.pem 파일 없이 접속하는 방법`을 알아보도록 하겠습니다.
기본적으로 EC2는 ssh를 이용하여 접속을 하는데요. 먼저 SSH가 무엇인가에 대해 알아보려고 합니다. 그럼 시작해보겠습니다.😄

## 2️⃣SSH란?

> 시큐어 셸(Secure Shell, SSH)은 네트워크 상의 다른 컴퓨터에 로그인하거나 원격 시스템에서 명령을 실행하고 다른 시스템으로 파일을 복사할 수 있도록 해 주는 응용 프로그램 또는 그 프로토콜을 가리킵니다. 기존의 rsh, rlogin, 텔넷 등을 대체하기 위해 설계되었으며, 강력한 인증 방법 및 안전하지 못한 네트워크에서 안전하게 통신을 할 수 있는 기능을 제공합니다. 기본적으로는 22번 포트를 사용합니다.

위의 내용은 SSH에 대한 나무위키에 대한 설명입니다.  
보통 SSH를 사용하여 ec2에 접속하곤 합니다. 그럼 EC2에 접속해보도록 하겠습니다.🚀~

## 3️⃣EC2 접속하기

먼저 저의 EC2 환경은 Ubuntu 18.04 임을 밝힙니다. 또한 접속은 윈도우 cmd를 이용하였습니다.
준비물은 다음과 같습니다. `접속할 서버의 IP주소, pem key가 있는 파일`이 필요합니다.

1. 먼저 EC2를 접속하기 위해 cmd를 켜줍니다.
2. cd명령어를 이용하여 pem키가 다운되어 있는 폴더로 갑니다.
3. 접속 명령어는 다음과 같습니다.(여기서 ubuntu의 경우 username에는 ubuntu를 입력해주시면 됩니다.)

   ```console
   $ssh -i pemkeyname.pem username@IPaddress
   ```

4. `Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 5.3.0-1023-aws x86_64)` 다음과 같은 메시지가 뜬다면 서버 접속에 성공한 것입니다.

## 4️⃣ pem파일 없이 EC2 편하게 접속하기

위의 방법으로는 매번 pem key가 필요하므로 다른 컴퓨터에서 접속하기가 까다로워집니다. 물론 보안상으로는 pem key로 접속하는 방법은 대단히 좋은 방법이긴 하지만 저는 컴퓨터를 옮기며 코딩하는 일이 많기 때문에 pem key없이 로그인을 하는 방법을 알아보았습니다.  
방법은 다음과 같습니다.

1. 위와 같은 방법으로 ssh로 ec2를 접속한다.
2. 새로운 유저를 생성한다.(USERNAME엔 본인이 원하는 이름을 넣어주시면 됩니다.)

   ```console
   $sudo useradd -s /bin/bash -m -d /home/USERNAME -g root USERNAME
   ```

3. 유저 비밀번호를 설정합니다.

   ```console
   $sudo passwd USERNAME
   ```

   - 패스워드를 입력합니다.

4. sudoers 파일 권한을 변경합니다.

   ```console
   $sudo chmod u+w /etc/sudoers
   ```

5. sudoers 파일 열고, username을 추가합니다.(추가할때는 i를 누르시고 입력한 후에 :wq로 저장을하고 나오면 됩니다.)

   ```console
   $sudo vi /etc/sudoers
   ```

   - `USERNAME ALL=(ALL:ALL) ALL`을 추가합니다.

6. sshd_config 파일에 PasswordAuthentication 설정을 변경합니다.

   ```console
   $sudo vi /etc/ssh/sshd_config
   ```

   - PasswordAuthentication이 no라고 되어있는 것을 `yes로 변경`합니다.

7. ssh를 재시작합니다.

   ```console
   $sudo service ssh restart
   ```

8. 서버를 나갔다가 변경한 유저로 접속합니다.
   - ex) ssh [username]@host
   - 위에서 설정한 비밀번호를 입력합니다.
9. 접속이 되면 성공한 것입니다. 다음부터는 pem key를 쓰지 않고 서버에 접속을 할 수 있게 되었습니다.

## 5️⃣오류?

만약 위와 같은 방법으로 접속이 안된다면 `ec2의 인바운드 규칙에 SSH 22번 포트가 열려있는지 확인` 바랍니다.
추가적으로 문제가 있을 시 댓글 남겨주시면 감사하겠습니다.

## 6️⃣ 참조

- [.pem파일 없이 AWS EC2 접속하는 방법](https://ithub.tistory.com/215)
- [ssh 나무위키](https://namu.wiki/w/Secure%20Shell)

## 7️⃣ 마치며..

pem 키 없이 ec2에 접속하는 방법에 대하여 알아보았습니다.
궁금한게 있으시면 아래 댓글 남겨주세요.🙏  
댓글은 저에게 큰 힘이 됩니다!  
감사합니다. ❤️
