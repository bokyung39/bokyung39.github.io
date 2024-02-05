---
# {: width="100%" height="100%" .normal}
title: 🎬 ReactJS로 영화 웹 서비스 만들기 (11) - Moive App 만들기
author: bokyung
date: 2024-02-03 00:00:00 +0800
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
