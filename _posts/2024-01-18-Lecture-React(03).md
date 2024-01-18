---
# 👨‍💻 (project) 📌 (fixed) 📖 (What to Learn)  🌱 (Link) 🧷(#3) 📌(#4) 👀(Recap)
title: ReactJS로 영화 웹 서비스 만들기 (03) - React의 State
author: bokyung
date: 2024-01-18 00:00:00 +0800
toc: true
pin: false
categories: [Lecture, ReactJS로 영화 웹 서비스 만들기]
tags: [React, State]
image: https://nomadcoders.co/_next/image?url=https%3A%2F%2Fd1telmomo28umc.cloudfront.net%2Fmedia%2Fpublic%2Fthumbnails%2Freact-for-beginners.jpeg&w=1920&q=75
---

> ## useState

React JS에서 데이터를 저장시켜 자동으로 리렌더링을 일으킬 수 있는 방법에 이용된다
<br>

![image](https://github.com/bokyung39/intro-me/assets/72790694/da695db4-6ef4-4172-9cf1-90df2940bf3a)

이렇게 `const data = React.useState();`를 `console.log` 찍어보면
![image](https://github.com/bokyung39/intro-me/assets/72790694/1114bbab-6ece-4ce1-8375-c7d7706b4f42)

`undefined`와 함수가 적힌 배열이 찍히는 것을 볼 수 있다<br>
`undefined`는 `data`이고, `f`는 `data`를 바꿀 때 사용하는 함수이다<br>
`React.useState()` 함수는 초기값을 설정할 수 있음 <br>
즉, `undefined`는 초기값! &nbsp;&nbsp; `React.useState(0);` 을 한다면 콘솔에는 `[0, ƒ]` 가 찍힐 것이다<br>
그리고 두 번째 요소인 `f`는 그 값을 바꾸는 함수!<br>

정리하자면, <br>
`React`의 `useState`는 우리한테 배열 하나를 주는데 그 배열의 첫번쨰 요소는 우리가 담으려는 `data`값이고,<br>
두번째 요소는 그 `data`값을 바꿀때 사용할 함수이다<br>
<br>

그리고 `const` **`data`** `= React.useState(0);` 대신 `const` **`[counter, setCounter]`** `= React.useState(0);` 을 준다면 `counter`와 `setCounter`에 각각 `0` 과 `ƒ` 가 할당되게 된다!<br>

방금 말한 것 처럼 보통 `data`에는 `counter`처럼 원하는대로 붙이고<br>
`ƒ`는 set 뒤에 데이터 이름을 붙여 `setCounter`로 사용한다<br>
어떤값을 부여하든 `setCounter` 함수는 그 값으로 업데이트하고 리렌더링 일으킨다!
<br>
<br>
> ## Vanilla JS  vs  React JS

그럼 이제 버튼을 클릭한 만큼 count가 증가되는 간단한 프로젝트로 VanillaJS와 ReactJS를 비교해보자!

<html lang="en">
    <body>
        <h3 id="click">Total clicks: 0</h3>
        <button id="btn">Click me</button>
    </body>
    <script>
        let counter = 0;
        const button = document.getElementById("btn");
        const h3 = document.getElementById("click");
        function handleClick(){
            counter = counter + 1;
            h3.innerText = `Total clicks: ${counter}`;
        }
        button.addEventListener("click", handleClick);
    </script>
</html>

<br>

- ### Vanilla JS ver.

```html
<!DOCTYPE html>
<html lang="en">
    <body>
        <h3 id="click">Total clicks: 0</h3>
        <button id="btn">Click me</button>
    </body>
    <script>
        let counter = 0;
        const button = document.getElementById("btn");
        const h3 = document.getElementById("click");
        function handleClick(){
            counter = counter + 1;
            h3.innerText = `Total clicks: ${counter}`;
        }
        button.addEventListener("click", handleClick);
    </script>
</html>
```

![제목 없는 동영상 - Clipchamp로 제작 (1)](https://github.com/bokyung39/intro-me/assets/72790694/4680480f-1518-4cad-b299-f8cf265248ce)

Vanilla JS에서는 h3 전체가 업데이트되고 있는 것을 확인할 수 있다.

<br>

- ### React JS ver.

```html
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
        function App() {
            const [counter, setCounter] = React.useState(0);
            const onClick = () => {
                setCounter(counter + 1);
            };
            return (
                <div>
                    <h3>Total clicks: {counter}</h3>
                    <button onClick={onClick}>Click me</button>
                </div>
            );
        };
        ReactDOM.render(<App />, root);
    </script>
</html>
```

![제목 없는 동영상 - Clipchamp로 제작 (6)](https://github.com/bokyung39/intro-me/assets/72790694/57f8d4d6-0c87-48de-b8bf-a90fa29ed7f6)


React에서는 **변경된 부분만** 리렌더링되는 것을 확인할 수 있다 !<br>
즉, React에서는 state가 바뀔 때마다 컴포넌트 전체가 rerendering이 일어나는데,<br>
eventlistener가 등록되거나 Total clicks을 다시 만드는 것이 아니라, 실제로 바뀌는 값인 `{counter}` 이 부분만 업데이트된다


#### **React는 state값이 바뀌면 새로운 값을 가지고 컴포넌트가 리렌더링된다 !!**

### ✅ 이게 왜 좋은건가?
- **`Vanilla JS`**에서는 DOM 변경을 직접 처리한다. 즉, 필요한 DOM 요소를 직접 선택하고, 요소의 속성을 변경하거나 새로운 요소를 추가하거나 기존 요소를 제거하는 등의 작업을 직접 수행한다. <br>
DOM 변경이 발생하면, 브라우저는 변경된 DOM 트리를 다시 계산하고, 렌더 트리를 다시 생성한 후 화면에 그립니다. 이 과정은 비용이 많이 드는 연산으로, 자주 발생하게 되면 성능을 저하시킬 수 있습니다.<br>
- 그렇지만 **`React JS`**는 DOM 변경을 처리하기 위해 가상 DOM(Virtual DOM)이라는 개념을 도입! <br>
상태 변경이 발생할 때마다 새로운 가상 DOM 트리를 생성하고, 이전의 가상 DOM 트리와 비교하여 변경된 부분을 파악한다 <br>
이렇게 파악된 변경 사항만 실제 DOM에 반영하는 방식을 사용하는데, 이 과정을 '재조정(Reconciliation)' 또는 'Diffing'이라고 함<br>
가상 DOM을 사용함으로써, 변경이 필요한 최소한의 요소만 실제 DOM에 반영되기 때문에 불필요한 연산을 줄이고 성능을 향상시킬 수 있다<br>

따라서, `ReactJS`는 복잡한 UI 업데이트를 효과적으로 처리할 수 있으며, 이를 통해 웹의 응답성을 향상시키고 사용자 경험을 개선할 수 있다!