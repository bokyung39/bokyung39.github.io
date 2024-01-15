---
# 👨‍💻 (project) 📌 (fixed) 📖 (What to Learn)  🌱 (Link) 🧷(#3) 📌(#4) 👀(Recap)
title: ReactJS로 영화 웹 서비스 만들기 (01)
author: bokyung
date: 2024-01-15 00:00:00 +0800
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

> ## Vanilla JS  vs  React JS

버튼을 클릭한 만큼 count가 증가되는 간단한 프로젝트를 만들어 VanillaJS와 ReactJS를 비교해보자!

<br>

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

- Vanilla JS ver.

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

<br>

- React JS ver.

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



<br>

### 🧷 parsedToDos.forEach
- `forEach` : 각각의 배열의 요소들을 한 번씩 실행 해준다.
    - `parsedToDos.forEach((item) => console.log("this is the turn of", item));`

![image](https://github.com/JEONGSUJONG/Readme_main/assets/142254876/b06bb904-602b-4344-83d6-33343626bb0e){: width="400" height="250" .normal}

<br>

> ## 👀 Recap

- `ToDoList` 작성 시 localStorage 에 저장이 된다. 하지만, string 타입으로 저장됨.
- `JSON.parse` 를 통해 object 타입으로 바꿔준다. -> index를 통해 각각의 value에 접근이 가능하다.
- `forEach` 를 통해 object의 모든 index를 순찰(?)하며 함수를 실행한다.

<br>

> ## forEach

`forEach` 사용 -> 문제해결

```javascript
parsedToDos.forEach(paintToDo);
```

- 새로고침 하여도 localStorage 에 남아있는 요소들을 다시 보여주기 위함.
    - 단, 새로고침한 페이지에서 `ToDoList`를 작성하고 다시 새로고침하면 전에 작성한 localStorage 가 사라진다. (덮어써짐)
    - javascript 시작할 때 `const toDos = [];` 항상 비어있기 때문
        - 해결 : application이 시작될 때 toDos array를 빈 값으로 시작하는 대신에, `const`를 `let`으로 바꿔서 업데이트가 가능하도록 만들고, localStorage에 `toDo` 들이 있으면 `toDos`에 `parsedToDos`를 넣어서 전에 있던 `toDo`들을 복원하면된다.

```javascript 
let toDos = [];

if (savedToDos !== null) {
    const parsedToDos = JSON.parse(savedToDos);
    toDos = parsedToDos;
    parsedToDos.forEach(paintToDo);
}
```

<br>

> ## Deleting ToDos

id값을 지정하고 id값을 html li 태그에 넣기

- localStorage에 toDos를 저장하는 것까진 완료했지만 localStorage에서의 삭제가 이루어지지 않음.


1. toDos에게 id를 준다.
```javascript
{id:1234, toDo:"Eat"}
```
- `Date.now()` 를 사용하여 랜덤한 id를 준다.
- id값을 주기 위해서 object로 값을 전달해줘야한다.
- `handleToDoSubmit`
```javascript
    const newTodoObj = {
        text:newTodo,
        id:Date.now();

        toDos.push(newTodoObj);
    };
```

![image](https://github.com/JEONGSUJONG/Readme_main/assets/142254876/f4f4c027-b1b9-46e2-8ffa-cd85c3324125){: width=100% height=100% .normal}

<br>

- id를 사용하기 위해 id 값을 html에 놔두고싶음.

1. paintToDo : object를 인자로 받아야함.

```javascript
paintToDo(newTodoObj);
```

![image](https://github.com/JEONGSUJONG/Readme_main/assets/142254876/a5f80f1c-a1d8-40cf-abe9-a1b793753983){: width="400" height="250" .normal}

<br>

2. Object 안의 text 를 보여주고싶음.

3. 아래와 같이 paintToDo 함수 수정 하면 다시 정상적으로 보임.
```javascript
span.innerText = newTodo.text;
```
3. id를 아직 사용하지 않음... ㅠㅠ
```javascript
li.id = newTodo.id;
```

![image](https://github.com/JEONGSUJONG/Readme_main/assets/142254876/a948ef3f-3cc7-4e02-a33f-41658b4a5238){: width="400" height="250" .normal}

<br>

> ## Which Id Do u want to Delete?

- `filter` 사용
```javascript
let array = [3, 5, 11, 0, 9, 'string'];
et result = array.filter((value) => value < 10)
console.log(result);  // [3, 5, 0, 9]
```
- 
    - true를 return 해야만한다.
    - 만약 false를 return하면 그 item은 새로운 배열에 포함되지 않는다.
    ```javascript
    function deleteToDo(event) {
        const li = event.target.parentElement;
        toDos = toDos.filter((toDo) => toDo.id !== parseInt(li.id));
        li.remove();
        saveToDos();
    }
    ```