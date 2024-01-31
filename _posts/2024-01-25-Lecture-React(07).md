---
title: 🎬 ReactJS로 영화 웹 서비스 만들기 (07) - Props, Memo
author: bokyung
date: 2024-01-25 00:00:00 +0800
toc: true
pin: false
published: true
categories: [Lecture, ReactJS로 영화 웹 서비스 만들기]
tags: [React, Props, Memo]
image: https://nomadcoders.co/_next/image?url=https%3A%2F%2Fd1telmomo28umc.cloudfront.net%2Fmedia%2Fpublic%2Fthumbnails%2Freact-for-beginners.jpeg&w=1920&q=75
---

이번에는 부모 컴포넌트(`App()`)가 state(상태)를 변경할 때 다른 컴포넌트들에게는 어떤 일이 일어날지 알아보자 !
<br>
<br>

> ## props에 function

props에는 text나 boolean값만 보낼 수 있는게 아니라 **함수**도 보낼 수 있다!

```jsx
{% raw %}
function Btn({ text, onClick }) {
  return (
    <button
      onClick={onClick}
      style={{
        backgroundColor: "tomato",
        color: "white",
        padding: "10px 20px",
        borderRadius: 10,
        border: 0,
      }}
    >
      {text}
    </button>
  );
}
function App() {
  const [value, setValue] = React.useState("Save Changes");
  const changeValue = () => setValue("Revert Changes");
  return (
    <div>
      <Btn text={value} onClick={changeValue} />
      <Btn text="Continue" />
    </div>
  );
}

const root = document.getElementById("root");
ReactDOM.render(<App />, root);
{% endraw %}
```

`<Btn text={value} onClick={changeValue} />` 여기서 **`onClick`**은 이벤트 리스너가 아니다<br>
이 **`onClick`**은 그냥 내가 지은 이름이고! button html 태그 안에 들어가는 것이 아님<br>
이 전 게시물에서의 banana처럼 `function Btn({ text, onClick })` 이렇게 props에 내가 직접 넣어서 **`onClick`**이라는 prop을 갖게 하는 것이다<br>
그리고 button은 **`onClick`**이라는 `onClick 리스너`를 갖게 되는 것!
<br>
<br>

> ## React.memo()

부모 컴포넌트의 state를 변경하면 당연히 그 자식 컴포넌트들도 Re-render가 일어나게 된다<br>
불필요한 렌더링이 발생할 수도 있는데, 이 경우에는 `React.memo()`로 prop의 변경이 일어난 부분만 렌더링 시킬 수 있다<br>
많은 자식 컴포넌트를 가지고 있는 부모 컴포넌트인 경우에 효율적으로 사용할 수 있다!

![제목 없는 동영상 - Clipchamp로 제작 (8)](https://github.com/bokyung39/intro-me/assets/72790694/961c2d10-77a4-4cba-98f6-3ee78533d325){: width="100%" height="100%" .normal}

Btn 함수안에 콘솔로그를 찍어보면 버튼 두개 모두 리렌더링이 일어난 것을 알 수 있다.<br>
그치만 우린 두번째 버튼은 다시 그릴 필요가 없기 때문에 Memo라는 것을 사용해 필요한 것만 렌더링이 일어나도록 할 수 있다🤩<br>

```jsx
const MemorizedBtn = React.memo(Btn);
function App() {
  const [value, setValue] = React.useState("Save Changes");
  const changeValue = () => setValue("Revert Changes");
  return (
    <div>
      <MemorizedBtn text={value} onClick={changeValue} />
      <MemorizedBtn text="Continue" />
    </div>
  );
}
```

MemorizedBtn라는 것을 만들어 적용시켜주면

![제목 없는 동영상 - Clipchamp로 제작 (9)](https://github.com/bokyung39/intro-me/assets/72790694/951d75db-3a40-46da-bb39-3d52100b52bb){: width="100%" height="100%" .normal}

첫번째 버튼만 다시 그려진 것을 알 수 있다 !! <br>
Cooooool
