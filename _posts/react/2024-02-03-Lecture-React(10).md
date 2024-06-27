---
# {: width="100%" height="100%" .normal}
title: 🎬 ReactJS로 영화 웹 서비스 만들기 (10) - Coin Tracker 만들기
author: bokyung
date: 2024-02-03 00:00:00 +0800
toc: true
pin: false
published: true
categories: [Lecture, ReactJS로 영화 웹 서비스 만들기]
tags: [React, Coin Tracker, Coin API]
image: https://nomadcoders.co/_next/image?url=https%3A%2F%2Fd1telmomo28umc.cloudfront.net%2Fmedia%2Fpublic%2Fthumbnails%2Freact-for-beginners.jpeg&w=1920&q=75
---

이번에는 useEffect를 포함한 내용들을 이용해 Coin Tracker를 만들어보도록 하겠다!
<br>
<br>
사용할 coin API는 <https://api.coinpaprika.com/v1/tickers> 이것!

```jsx
useEffect(() => {
  fetch("https://api.coinpaprika.com/v1/tickers")
    .then((response) => response.json())
    .then((json) => {
      setCoins(json);
      setLoading(false);
    });
}, []);
```

coin API는 fetch를 이용해 불러와서 사용하면 된다.
<br>
<br>

```jsx
{
  coins.map((coin) => (
    <li>
      {coin.name} ({coin.symbol}): ${coin.quotes.USD.price} USD
    </li>
  ));
}
```

여기서 `coin`이라는 변수는 `coins array`안에 있는 각각의 `coin`을 의미.

#### **🔽 결과물 🔽**

![-Clipchamp2-ezgif com-video-to-gif-converter](https://github.com/bokyung39/intro-me/assets/72790694/93a561cc-70a7-4267-96b8-b36f7249b10f){: width="100%" height="100%" .normal}

로딩 중엔 코인의 개수가 0으로 뜨고, 로딩이 끝나면 불러온 코인의 개수 값까지 출력되는 것을 볼 수 있다!
<br>
<br>

#### **🔽 전체 코드 🔽**

```jsx
//App.js
import { useState, useEffect } from "react";

function App() {
  const [loading, setLoading] = useState(true);
  const [coins, setCoins] = useState([]);
  useEffect(() => {
    fetch("https://api.coinpaprika.com/v1/tickers")
      .then((response) => response.json())
      .then((json) => {
        setCoins(json);
        setLoading(false);
      });
  }, []);
  return (
    <div>
      <h1>The Coins! ({coins.length})</h1>
      {loading ? <strong>Loading...</strong> : null}
      <ul>
        {coins.map((coin) => (
          <li>
            {coin.name} ({coin.symbol}): ${coin.quotes.USD.price} USD
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```
