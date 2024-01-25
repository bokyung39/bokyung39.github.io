---
title: 🎬 ReactJS로 영화 웹 서비스 만들기 (06) - Props
author: bokyung
date: 2024-01-23 00:00:00 +0800
toc: true
pin: false
published: true
categories: [Lecture, ReactJS로 영화 웹 서비스 만들기]
tags: [React, Props]
image: https://nomadcoders.co/_next/image?url=https%3A%2F%2Fd1telmomo28umc.cloudfront.net%2Fmedia%2Fpublic%2Fthumbnails%2Freact-for-beginners.jpeg&w=1920&q=75
---

> ## Props

Props는 부모 컴포넌트로부터 자식 컴포넌트에 데이터를 보낼 수 있게 해주는 방법이라고 할 수 있다!<br>
(여기서 말하는 컴포넌트란 function(함수)를 의미)
<br>

예를 들어, 버튼 안의 텍스트 내용만 다르고 스타일은 똑같은 버튼 두개를 만들고 싶은데 그럴때마다 각각의 버튼에 똑같은 내용의 스타일 코드를 복붙하는건 매우 비효율적.<br>
그 대신 이런 스타일을 모두 갖는 하나의 컴포넌트를 만들어 필요할 때마다 재사용하면 된다

#### **🔽 예시 🔽**

```jsx
{% raw %}
function Btn() {
  return (
    <button
      style={{
        backgroundColor: "tomato",
        color: "white",
        padding: "10px 20px",
        borderRadius: 10,
        border: 0
      }}
    >
      Save Changes
    </button>
  );
}
{% endraw %}
```

`Btn`이라는 함수형 컴포넌트를 만들어서 내가 원하는 스타일들을 지정하고,<br>

```jsx
function App() {
  return (
    <div>
      <Btn banana="Save Changes" />
      <Btn banana="Continue" />
    </div>
  );
}
```

버튼 안의 텍스트는 `<Btn text="Save Changes" />` 이런 식으로 syntax를 추가해 텍스트를 각각 다르게 입력할 수 있다. 여기서 `text`는 꼭 text가 아니어도 된다. potato라고 짓든, banana라고 짓든 내맴임<br>

여기까지의 결과물을 확인해보면,

![image](https://github.com/bokyung39/intro-me/assets/72790694/ee005f96-1687-426c-9a60-2ff473c75679){: width="100%" height="100%" .normal}

버튼 안의 텍스트 내용이 똑같다 🤔<br>
왜냐하면 나는 banana를 Btn에게 보냈는데, Btn은 banana를 사용하지 않고 있기 떄문!<br>

내가 만들고 사용하는 모든 컴포넌트들은 인자(argument)를 받는데, 이 인자의 이름 또한 내 맘대로 지을 수 있지만 보통 사람들은 이걸 props라고 한다<br>
Btn으로부터 전달받는 properties<br>
그리고 콘솔로그를 찍어보면 알겠지만 `props`는 오브젝트이다. 우리가 넣은 모든 것을 갖는 오브젝트!<br>
암튼 그래서 ! banana를 Btn의 인자로 넣어주어야 한다

```jsx
{% raw %}
function Btn(props) {
  return (
    <button
      style={{
        backgroundColor: "tomato",
        color: "white",
        padding: "10px 20px",
        borderRadius: 10,
        border: 0
      }}
    >
      {props.banana}
    </button>
  );
}
{% endraw %}
```

이렇게 ! 그럼 이제

![image](https://github.com/bokyung39/intro-me/assets/72790694/dda9d017-504a-4250-b833-242ccf1884b7){: width="100%" height="100%" .normal}

텍스트 내용이 반영된 것을 확인 할 수 있다!

```jsx
{% raw %}
function Btn({ banana }) {
  return (
    <button
      style={{
        backgroundColor: "tomato",
        color: "white",
        padding: "10px 20px",
        borderRadius: 10,
        border: 0
      }}
    >
      {banana}
    </button>
  );
}
{% endraw %}
```

이렇게 더 짧게 적는 방법도 있당
