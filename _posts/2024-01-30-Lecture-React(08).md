---
title: 🎬 ReactJS로 영화 웹 서비스 만들기 (06) - useEffect
author: bokyung
date: 2024-01-30 00:00:00 +0800
toc: true
pin: false
published: true
categories: [Lecture, ReactJS로 영화 웹 서비스 만들기]
tags: [React, useEffect]
image: https://nomadcoders.co/_next/image?url=https%3A%2F%2Fd1telmomo28umc.cloudfront.net%2Fmedia%2Fpublic%2Fthumbnails%2Freact-for-beginners.jpeg&w=1920&q=75
---

> ## useEffect

- 두개의 인자를 가지는 function
  - 첫번째 인자 : 내가 딱 한번만 실행하고자 하는 코드
  - 두번째 인자 : 배열 [] 이 들어간다
- 컴포넌트의 첫번째 렌더 시점에 첫번째 인자가 호출된다<br>
  state가 변화하든, 무슨 일이 일어나든 단 한번만 실행되도록 해준다
- 참고로 useEffect는 컴포넌트 렌더링 이후에 실행된다 즉, 화면이 먼저 다 그려지고 그 이후에 실행된다는 점! 알아두장
- useEffect를 사용해 코드가 언제 실행될지 결정할 수 있다
  - 컴포넌트가 생성되는 첫 시작점
  - 무언가가 update될 때
