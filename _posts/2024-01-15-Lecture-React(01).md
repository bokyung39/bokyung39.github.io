---
# 👨‍💻 (project) 📌 (fixed) 📖 (What to Learn)  🌱 (Link) 🧷(#3) 📌(#4) 👀(Recap)
title: ReactJS로 영화 웹 서비스 만들기 (01) - JSX
author: bokyung
date: 2024-01-15 00:00:00 +0800
toc: true
pin: false
categories: [Lecture, ReactJS로 영화 웹 서비스 만들기]
tags: [JSX, React]
image: https://nomadcoders.co/_next/image?url=https%3A%2F%2Fd1telmomo28umc.cloudfront.net%2Fmedia%2Fpublic%2Fthumbnails%2Freact-for-beginners.jpeg&w=1920&q=75
---

> ## JSX

### JSX란?

JavaScript를 확장한 문법

<html lang="en">
    <body>
        <div id="root"></div>
    </body>
    <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
    <script>
        const root = document.getElementById("root");
        const title = React.createElement(
            "h3", {
                id: "title",
                onMouseEnter: () => console.log("mouse enter"),
            }, 
            "Hello I'm a title"
        );
        const btn = React.createElement(
            "button", 
            {
                onClick: () => console.log("im clicked"),
                style: {
                    backgroundColor: "tomato",
                },
            }, 
            "Click me"
        );
        const container = React.createElement("div", null, [title, btn]);
        ReactDOM.render(container, root);
    </script>
</html>

<br>
기존 자바스크립트 코드를 jsx로 바꿔보자!

- 기존 javaScript 코드 (요소를 생성하는 오래된 방식)

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
        const h3 = React.createElement(
            "h3", {
                id: "title",
                onMouseEnter: () => console.log("mouse enter"),
            }, 
            "Hello I'm a title"
            );
    
        const btn = React.createElement(
            "button", 
            {
                onClick: () => console.log("im clicked"),
                style: {
                    backgroundColor: "tomato",
                },
            }, 
            "Click me"
        );

        // 배열을 이용해서 여러 요소를 한번에 render
        const container = React.createElement("div", null, [h3, btn]);
        ReactDOM.render(container, root);
    </script>
</html>
```
<br>
- jsx 이용한 코드

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
        const root = document.getElementById("root");
        const Title = () => (
            <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
                Hello I'm a title
            </h3>
        );
       const Button = () => (
        <button 
            {%- assign styles = "backgroundColor: tomato;" -%}
            style="{{ styles }}"
            onClick={() => console.log("im clicked")}
        >
            Click me
        </button>
       );
       
       const Container = () => (
            <div>
                <Title />
                <Button />
            </div>
        );
       ReactDOM.render(<Container />, root);
    </script>
</html>
```

- `JSX`는 기존의 `createElement`을 사용하지 않고, 일반적인 HTML작성방식과 유사한 방식으로 코드를 작성한다<br>
- `onMouseEnter`와 같은 `property`들도 마치 태그가 가진 하나의 속성인 것처럼 태그 안에 추가함

그런데 ! <br>
저렇게만 작성하고 결과를 확인해보면 아래 사진과 같은 에러가 발생한다 😕

![image](https://github.com/bokyung39/intro-me/assets/72790694/42a9d80b-132c-4d11-bfc4-f9727fd16bf6)
{: width="100%" height="100%" .normal}

그 이유는 바로 <br>
브라우저가 온전히 JSX를 이해하는 것은 아니기 때문! <br>
그래서 브라우저가 JSX를 이해할 수 있도록 **Babel**이라는 것을 사용한다 <br>
Babel은 JSX로 적은 코드를 브라우저가 이해할 수 있는 형태로 바꾸어주는 역할을 함

Babel의 [Try it out](https://babeljs.io/repl) 페이지에서 내가 작성한 JSX 코드를 입력하고 어떻게 자바스크립트로 변환되는지 확인해 볼 수 있다!
![image](https://github.com/bokyung39/intro-me/assets/72790694/393e4a3d-d8b9-49f3-8cfe-d3d571c78e03){: width="100%" height="100%" .normal}

결과를 확인해보면 기존의 javaScirpt로 작성했던 코드와 같다는 것을 알 수 있다

암튼 ! <br>
좀전의 에러를 해결하려면 babel을 설치해주어야 한다 <br>
일단은 간단하게 코드를 추가하는 방식으로 babel을 적용시켜보자 <br>

```jsx
<!DOCTYPE html>
<html lang="en">
    <body>
        <div id="root"></div>
    </body>
    <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script> 
    <!-- Babel 적용을 위해 코드 추가-->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <!-- Babel 적용을 위해 코드 추가-->
    <script type="text/babel"> 
        const root = document.getElementById("root");
        const Title = () => (
            <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
                Hello I'm a title
            </h3>
        );
       const Button = () => (
        <button 
            {%- assign styles = "backgroundColor: tomato;" -%}
            style="{{ styles }}"
            onClick={() => console.log("im clicked")}
        >
            Click me
        </button>
       );
       
       const Container = () => (
            <div>
                <Title />
                <Button />
            </div>
        );
       ReactDOM.render(<Container />, root);
    </script>
</html>
```

![제목 없는 동영상 - Clipchamp로 제작 (5)](https://github.com/bokyung39/intro-me/assets/72790694/12ef2701-6cd5-4373-9cba-34da110751f7)

<br>
잘 작동하는 것을 확인 할 수 있다 !