---
# 👨‍💻 (project) 📌 (fixed) 📖 (What to Learn)  🌱 (Link) 🧷(#3) 📌(#4) 👀(Recap)
title: ReactJS로 영화 웹 서비스 만들기 (03) - React의 State (2)
author: bokyung
date: 2024-01-18 00:00:00 +0800
toc: true
pin: false
categories: [Lecture, ReactJS로 영화 웹 서비스 만들기]
tags: [React, State]
image: https://nomadcoders.co/_next/image?url=https%3A%2F%2Fd1telmomo28umc.cloudfront.net%2Fmedia%2Fpublic%2Fthumbnails%2Freact-for-beginners.jpeg&w=1920&q=75
---

이전 글에서 state를 업데이트할 때

```javascript
const [counter, setCounter] = React.useState(0);
const onClick = () => {
  setCounter(counter + 1);
};
```

이런 식으로 counter에 1을 직접 더해 할당하는 방식을 사용하였는데, 이런 직접 할당하는 방법보다<br>

```javascript
const [counter, setCounter] = React.useState(0);
const onClick = () => {
  setCounter((current) => current + 1);
};
```

이렇게 함수를 사용해 할당하는 방식이 조금 더 안전하다고 할 수 있다.<br>

두 방식 모두 현재의 state를 가지고 새로운 값을 계산해내는데, 함수를 사용하는 방식은 리엑트가 저 `current`가 확실히 현재 값이라는 것을 보장해준다!
그렇기 떄문에 우리가 현재 state를 기반으로 다음 state를 계산하고 싶다면 함수를 이용하는 것이 좀 더 바람직하다
