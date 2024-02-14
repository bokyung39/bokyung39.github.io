---
# {: width="100%" height="100%" .normal}
title: 🎬 ReactJS로 영화 웹 서비스 만들기 (11) - Moive App 만들기
author: bokyung
date: 2024-02-04 00:00:00 +0800
toc: true
pin: false
published: true
categories: [Lecture, ReactJS로 영화 웹 서비스 만들기]
tags: [React, 영화 웹 만들기, Moive App]
image: https://nomadcoders.co/_next/image?url=https%3A%2F%2Fd1telmomo28umc.cloudfront.net%2Fmedia%2Fpublic%2Fthumbnails%2Freact-for-beginners.jpeg&w=1920&q=75
---

드디어 강의의 마지막 코스인 영화 웹 서비스 만들기 !! 🤩🤩
<br>
차근차근 만들어보장
<br>
<br>

> ## 영화 API 가져오기

<br>
이번에는 영화 정보들을 가져오기 위해 <https://yts.mx/api/v2/list_movies.json> 이 API를 사용할 것이다
<br>

나는 그 중에서도 별점이 9점 이상이고 연도별로 정렬한 값을 가져오고 싶어서 url뒤에 minimum_rating=9&sort_by=year 를 추가해주었다
<br>
<br>

### 🧩 then 대신 async-await

전 게시물에서의 coin tracker를 만들땐 api에서 json data를 가져올 때

```jsx
fetch("https://yts.mx/api/v2/list_movies.json?minimum_rating=9&sort_by=year")
  .then((response) => response.json())
  .then((json) => {
    setMoives(json.data.movies);
    setLoading(false);
  });
```

이런식으로 `then`을 사용하였지만 보통은 `then` 대신 ⭐**`async-await`**⭐를 사용한다
<br>

```jsx
const getMovies = async () => {
  const response = await fetch(
    "https://yts.mx/api/v2/list_movies.json?minimum_rating=9&sort_by=year"
  );
  const json = await response.json();
  setMoives(json.data.movies);
  setLoading(false);
};
useEffect(() => {
  getMovies();
}, []);
```

이렇게하면 위에서의 `then`을 사용한 코드와 동일하게 동작한다<br>
이 `getMovies`함수 코드를 더 줄이면

```jsx
const getMovies = async () => {
  const json = await (
    await fetch(
      "https://yts.mx/api/v2/list_movies.json?minimum_rating=9&sort_by=year"
    )
  ).json();
  setMoives(json.data.movies);
  setLoading(false);
};
```

이렇게 `await`가 또 다른 `await`를 감싸고 있는 형태로 줄일 수도 있다!

<br>
<br>
이 이후부터는 이 전의 coin tracker를 만들때와 같이 가져온 api data들을 이용해 코드를 작성하고, 꾸며주었다

<br>
<br>
> ## 😕 어려웠던 점

![20240215_1801550369-ezgif com-video-to-gif-converter](https://github.com/bokyung39/intro-me/assets/72790694/82a4cd07-535a-42a0-bc50-2dab8cc6cf43){: width="100%" height="100%" .normal}

헤더의 MOVIE COLLECTION 텍스트 위치를 잘 보면,,,
<br>
홈 화면에서 api를 불러오기 전에 로딩중일 때와 로딩된 후의 텍스트 위치가 미세하게 움직이는 것을 발견했다
<br>
처음엔 내가 헤더의 스타일을 이상하게 준 줄 알고 이것저것 지우고 추가하고를 반복했는데,,
<br>
알고보니 api가 로딩된 후에 스크롤바가 생겨서 스크롤바의 너비 길이 때문에 헤더의 길이도 같이 바뀌는 거였다..🤦🏻‍♀️
<br>
스크롤바는 생각도 못했다 진짜....
<br>
<br>
그래서 어떻게 해결하였느냐 !
<br>
해결 방법은 매우 간단했음
<br>
<br>

#### 🙂 **해결 방법**

html와 body를 100vw로 설정하면 된다.
<br>

```css
html,
body {
  width: 100vw;
  overflow-x: hidden;
  overflow-y: auto;
}
```

이것만 추가하면,,

![20240215_1754550032-ezgif com-video-to-gif-converter](https://github.com/bokyung39/intro-me/assets/72790694/070dc346-8647-47bd-9db7-ea181f9b2ae6){: width="100%" height="100%" .normal}

(대충 편안하다는 짤)
<br>
<br>
여기서 한가지 유의할 점은 스크롤바가 나타나면 스크롤바 때문에 맨 오른쪽이 약간 잘린다는 것.
<br>
이 점을 염두해 두고 스타일 코드를 작성하면 될 것 같다
<br>
<br>
<br>

> ## 🖥️ 최종 결과물

엄청나게 만족스럽진 않지만,, 그냥 깔끔하게 꾸미는 것에 목표를 두고 만들어보았다

#### 👉🏻 [확인하러가기💨💨](https://bokyung39.github.io/React-MovieApp/){:target="\_blank"}
