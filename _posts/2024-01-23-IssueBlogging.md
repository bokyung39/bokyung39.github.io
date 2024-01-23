---
title: 🔨 깃허브 블로그 게시물 업데이트 안되는 문제 해결
author: bokyung
date: 2024-01-23 00:00:00 +0800
toc: true
pin: false
published: true
categories: [Blogging, Etc]
---

열심히 작성한 게시물을 push했는데 실제 내 블로그에는 게시물이 업데이트 되지 않는 이슈 발생 ... 😢

깃허브 블로그 레포의 Actions에 들어가서 봐도 배포는 잘 된 것 같은데 업데이트가 안되었다 ㅠ
<br>

#### **해결 방법**

1.  `_config.yml`에 `futrue: true` 추가
2.  (제목, 작성일 같은)게시물 정보? 적는 곳에 `published: true` 추가
    ![image](https://github.com/bokyung39/intro-me/assets/72790694/6465b2bb-bfb3-453a-b230-0bc694a1b7b8)

    - **tip!** `published: false` 은 해당 게시물을 비공개로 돌리겠다는 뜻.

3.  `index.html`에 의미없는 아무 내용 추가 <br>
    나는 그냥 글자 하나 대문자->소문자로 바꿈 ㅎ
4.  push 하기

<br>
성공....🥰<br>
블로그 밀고 다시 만들어야 되는 줄 알고 눈물 흘릴 뻔 했잖아..
