---
title: 🔨 깃허브 블로그 Liquid Warning 스타일 코드 안보이는 문제
author: bokyung
date: 2024-01-25 00:00:00 +0800
toc: true
pin: false
published: true
categories: [Blogging, Etc]
image: https://github.com/bokyung39/intro-me/assets/72790694/51ca1bda-08b1-4939-a975-36c4bd0ffd1e
---

#### **에러 코드**

Liquid Warning: Liquid syntax error (line 16): Expected end_of_string but found colon in ~

<br>
![image](https://github.com/bokyung39/intro-me/assets/72790694/a4ac457c-afb7-48a0-a642-58aecb0e9ff4){: width="80%" height="80%" .normal}

내가 작성한 코드를 이런 식으로 코드 블럭으로 게시물에 넣고싶은데,,,
저장하고 확인해보면

![image](https://github.com/bokyung39/intro-me/assets/72790694/3dee87df-f481-42f1-9ed6-734ce6eb8b52)

스타일 코드들이 다 사라져있고...
터미널 창엔 ..

![image](https://github.com/bokyung39/intro-me/assets/72790694/6cfdb12a-86d1-4552-9f70-d3abd05bf135)

저장할때마다 떠서 넘 꼴보기가 싫음
<br>
<br>

#### **해결 방법**

코드블럭 안의 코드 앞뒤로

![image](https://github.com/bokyung39/intro-me/assets/72790694/05a276a9-5980-4193-a11f-d09f73585d81){: width="100%" height="100%" .normal}

입력!

![image](https://github.com/bokyung39/intro-me/assets/72790694/71fe400c-e0a5-4966-b2a7-dd6faf8a5bfc){: width="80%" height="80%" .normal}

이렇게 ! <br>

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

![image](https://github.com/bokyung39/intro-me/assets/72790694/eabdba37-bbf9-46d9-8dfd-84bd186bab7d){: width="100%" height="100%" .normal}

이제 터미널창도 깨끗♡

![image](https://github.com/bokyung39/intro-me/assets/72790694/95b5dab9-fe7b-416c-8b1e-9d917a47f830){: width="100%" height="100%" .normal}

<br>
초간단 히히<br>
