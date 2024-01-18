---
# 👨‍💻 (project) 📌 (fixed) 📖 (What to Learn)  🌱 (Link) 🧷(#3) 📌(#4) 👀(Recap)
title: ReactJS로 영화 웹 서비스 만들기 (02) - React
author: bokyung
date: 2024-01-16 00:00:00 +0800
toc: true
pin: false
categories: [Lecture, ReactJS로 영화 웹 서비스 만들기]
tags: [React]
image: https://nomadcoders.co/_next/image?url=https%3A%2F%2Fd1telmomo28umc.cloudfront.net%2Fmedia%2Fpublic%2Fthumbnails%2Freact-for-beginners.jpeg&w=1920&q=75
---

<!--  > 🌱 [Vanilla JS로 크롬 앱 만들기](https://nomadcoders.co/javascript-for-beginners/lobby) -->


> ## React JS를 사용하는 이유?

UI를 interactive(상호작용)하게 만들어준다!

<br>

<details>
<summary>이해를 위한 복잡한 React ver.</summary>
<div markdown="1">

```html
<!DOCTYPE html>
<html lang="en">
    <body>
        <div id="root"></div>
    </body>
    <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
    <script>
        const root = document.getElementById("root");
        // React.createElement("span", {span의 property}, “span의 내용”) -> property는 class name, id, style 등 가능
        const h3 = React.createElement("h3", null, "Hello I'm a h3");
        const btn = React.createElement("button", {
            onClick: () => console.log("im clicked"),
        }, "Click me");
        // 배열을 이용해서 여러 요소를 한번에 render
        const container = React.createElement("div", null, [h3, btn]);
        ReactDOM.render(container, root);
    </script>
</html>
```

</div>
</details>

<br>

```html
<!DOCTYPE html>
<html lang="en">
    <body>
        <div id="root"></div>
    </body>
    <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
    <script>
        const root = document.getElementById("root");
        // React.createElement("span", {span의 property}, “span의 내용”) -> property는 class name, id도 가능 style도 가능
        const span = React.createElement("span", { id: "sexy-span" }, "Hello I'm a span");
        ReactDOM.render(span, root);
    </script>
</html>
```


#### ✅ react-dom이란?

`React JS`는 어플리케이션이 interactive하도록 만들어주는 library이고, <br>
`react-dom`은 library 또는 package인데, 모든 `React element`들을 `HTML body`에 둘 수 있도록 해주는 역할을 한다. <br><br>
`ReactDOM.render()` : `render`의 의미는 `React element`를 가지고 `HTML`로 만들어 배치한다는 것. 즉, 사용자에게 보여준다는 의미 <br>
`ReactDOM.render(span, span이 가야할 위치)` <br>
-> 그래서 보통 body에 id=“root” 만들어서 span을 root 안에 두라고 함 

<br>

### Vanilla JS와 React JS의 차이!

```
Vanilla는 HTML -> JS 순서
React는 JS -> HTML 순서
```

Vanilla는 **HTML -> JS** 순서 <br>
React는 **JS -> HTML** 순서

> ### Vanilla JS와 React JS의 차이!
> Vanilla는 **HTML -> JS** 순서 &nbsp;&nbsp;/&nbsp;&nbsp;
> React는 **JS -> HTML** 순서

바닐라 JS에서는 HTMLS을 먼저 만들고, 그걸 자바스크립트로 가져와서 HTML을 수정하는 식이었다면,<br>
리액트에서는 모든 것이 자바스크립트로써 시작하고, 그 다음이 HTML이다. <- 이게 핵심!!! <br>
리액트를 사용하여 element를 생성한다. 이 말은, 리액트는 업데이트가 필요한 element를 업데이트할 것이라는 말.
업데이트가 필요하면 리액트가 결과물인 HTML을 업데이트할 수 있다는 것. 
**리액트는 유저에게 보여질 내용을 컨트롤할 수 있다는 뜻!**

HTML을 만들고, 찾아서 가져오고, 그리고 나서 업데이트하고,,,~ 이런 식으로 하지 않는다!
리액트한테 업데이트해야 하는 HTML을 업데이트하라고 할 것임!
**Javascript를 이용해 element를 생성하고, React JS가 그걸 HTML로 번역하는 것**