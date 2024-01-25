---
title: 🎬 ReactJS로 영화 웹 서비스 만들기 (05) - Converter App 만들기
author: bokyung
date: 2024-01-22 00:00:00 +0800
toc: true
pin: false
published: true
categories: [Lecture, ReactJS로 영화 웹 서비스 만들기]
tags: [React, State]
image: https://nomadcoders.co/_next/image?url=https%3A%2F%2Fd1telmomo28umc.cloudfront.net%2Fmedia%2Fpublic%2Fthumbnails%2Freact-for-beginners.jpeg&w=1920&q=75
---

State를 좀 더 제대로 이해하기 위해 간단한 단위변환기 app을 만들어보자<br>

#### **🔽 결과물 🔽**

![제목 없는 동영상 - Clipchamp로 제작 (7)](https://github.com/bokyung39/intro-me/assets/72790694/4cc067dc-a00e-4d22-8d0a-e83ec1520b1b){: width="200%" height="100%" .normal}

<br>

#### **🔽 전체 코드 🔽**

```jsx
<!DOCTYPE html>
<html lang="en">
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    function MinutesToHours() {
      const [amount, setAmount] = React.useState(0);
      const [inverted, setInverted] = React.useState(false);
      const onChange = (event) => {
        setAmount(event.target.value);
      };
      const reset = () => setAmount(0);
      const onInvert = () => {
        reset();
        setInverted((current) => !current);
      };
      return (
        <div>
          <h3>Min to Hour</h3>
          <div>
            <label htmlFor="minutes">Minutes</label>
            <input
              value={inverted ? amount * 60 : amount}
              id="minutes"
              placeholder="Minutes"
              type="number"
              onChange={onChange}
              disabled={inverted}
            />
          </div>
          <div>
            <label htmlFor="hours">Hours</label>
            <input
              value={inverted ? amount : Math.round(amount / 60)}
              id="hours"
              placeholder="Hours"
              type="number"
              onChange={onChange}
              disabled={!inverted}
            />
          </div>
          <button onClick={reset}>Reset</button>
          <button onClick={onInvert}>
            {inverted ? "Turn back" : "Invert"}
          </button>
        </div>
      );
    }
    function KmToMiles() {
      const [amount, setAmount] = React.useState(0);
      const [inverted, setInverted] = React.useState(false);
      const onChange = (event) => {
        setAmount(event.target.value);
      };
      const reset = () => setAmount(0);
      const onInvert = () => {
        reset();
        setInverted((current) => !current);
      };
      return (
        <div>
          <h3>KM 2 M</h3>
          <div>
            <label htmlFor="km">KM</label>
            <input
              value={inverted ? amount * 1.609 : amount}
              id="km"
              placeholder="KM"
              type="number"
              onChange={onChange}
              disabled={inverted}
            />
          </div>
          <div>
            <label htmlFor="miles">Miles</label>
            <input
              value={inverted ? amount : amount / 1.609}
              id="miles"
              placeholder="Miles"
              type="number"
              onChange={onChange}
              disabled={!inverted}
            />
          </div>
          <button onClick={reset}>Reset</button>
          <button onClick={onInvert}>
            {inverted ? "Turn back" : "Invert"}
          </button>
        </div>
      );
    }
    function App() {
      const [index, setIndex] = React.useState("xx");
      const onSelect = (event) => {
        setIndex(event.target.value);
      };
      return (
        <div>
          <h1>Super Converter</h1>
          <select value={index} onChange={onSelect}>
            <option value="xx">Select your units</option>
            <option value="0">Minutes & Hours</option>
            <option value="1">Km & Miles</option>
          </select>
          <hr />
          {index === "xx" ? "Please select your units" : null}
          {index === "0" ? <MinutesToHours /> : null}
          {index === "1" ? <KmToMiles /> : null}
        </div>
      );
    }

    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);
  </script>
</html>
```
