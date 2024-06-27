---
title: 🎬 ReactJS로 영화 웹 서비스 만들기 (08) - useEffect
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

  - ex1) 컴포넌트가 생성되는 첫 시작점
  - ex2) 무언가가 update될 때

- 예제
  ![-Clipchamp-ezgif com-video-to-gif-converter](https://github.com/bokyung39/intro-me/assets/72790694/e5a7804a-593a-4d94-bd9d-a65f947ea7eb){: width="100%" height="100%" .normal}

  1. `"I run only once."`

     ```jsx
     useEffect(() => {
       console.log("I run only once.");
     }, []);
     ```

     → 두번째 인자 배열이 비어있기 때문에 컴포넌트가d 렌더링 될 때 한번 실행되고 끝

  2. `"I run when 'counter' changes."`

     ```jsx
     useEffect(() => {
       console.log("I run when 'counter' changes.");
     }, [counter]);
     ```

     → counter가 변화할 때마다 실행

  3. `"I run when 'keyword' length is more than 5"`

     ```jsx
     useEffect(() => {
       if (keyword !== "" && keyword.length > 5) {
         console.log("I run when 'keyword' length is more than 5", keyword);
       }
     }, [keyword]);
     ```

     → keyword의 길이가 5 이상일때 실행

  - 전체 코드

  ```jsx
  // App.js
  import { useState, useEffect } from "react";

  function App() {
    const [counter, setValue] = useState(0);
    const [keyword, setKeyword] = useState("");
    const onClick = () => setValue((prev) => prev + 1);
    const onChange = (event) => setKeyword(event.target.value);

    useEffect(() => {
      console.log("I run only once.");
    }, []);
    useEffect(() => {
      if (keyword !== "" && keyword.length > 5) {
        console.log("I run when 'keyword' length is more than 5", keyword);
      }
    }, [keyword]);
    useEffect(() => {
      console.log("I run when 'counter' changes.");
    }, [counter]);
    return (
      <div>
        <input
          value={keyword}
          onChange={onChange}
          type="text"
          placeholder="Keyword here..."
        />
        <h1>{counter}</h1>
        <button onClick={onClick}>click me</button>
      </div>
    );
  }

  export default App;
  ```

- 컴포넌트가 파괴될때 코드가 실행되도록 할 수도 있다<br>
  → return으로 함수를 만들어주면 된다.
  ```jsx
  function Hello() {
    function hiFn() {
      console.log("created :)");
      return byeFn;
    }
    function byeFn() {
      console.log("bye :(");
    }
    useEffect(hiFn, []);
    return <h1>Hello</h1>;
  }
  ```
