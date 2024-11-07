---
title: 🧰 Redis (02) - 캐시(Cache), 캐싱(Caching) 전략
author: bokyung
date: 2024-11-07 00:00:00 +0800
toc: true
pin: false
published: true
categories: [Lecture, Redis 입문/실전]
tags: [Redis]
image: https://github.com/user-attachments/assets/42e1e2ff-597c-4135-b3c9-45607e683a72
---

<!-- 글자색 넣기 <span style="color: #239ED0">    </span>  -->
<!-- 띄어쓰기   &nbsp;   -->
<!-- 이미지 사이즈   {: width="80%" height="80%" .normal} -->
<!-- 이미지 {: .normal} <br> -->
<!-- 이미지 ![img]() -->

<br>
<br>
학습 환경 : Mac, iTerm
<br>
<br>

> ## 캐시(Cache), 캐싱(Caching)이란?

### ✔️ &nbsp;캐시(Cache)

원본 저장소보다 빠르게 가져올 수 있는 <U>임시 데이터 저장소</U>를 의미한다.

![img](https://github.com/user-attachments/assets/14de7ea2-6600-4994-b2a4-ade043b065f1)

Cache Aside (= Look Aside, Lazy Loading) 전략

캐시(임시 데이터 저장소)에 접근해 데이터를 빠르게 가져오는 방식을 의미한다.
<br>

예를 들어 실무에서는 API 응답 속도가 너무 느리다면 조회 속도를 향상기 위해 응답 데이터를 캐싱해 두고 쓰는 경우가 많다.
<br>
<br>

> ## 데이터를 캐싱할 때 사용하는 전략 (Cache Aside, Write Around)

Redis를 캐시로 쓸 때 쓸 수 있는 전략은 아주 다양하다. 그중에서 실무에서 가장 많이 사용되는 2가지만 알아보고 나머지 전략들은 익숙해진 뒤 추가로 학습하면 된다. 다양한 전략을 같이 사용할 수도 있다.

### ✔️ Cache Aside (= Look Aside, Lazy Loading) 전략

> **<U>Cache Aside 전략</U>**은 **<U>캐시에서 데이터를 확인하고, 없다면 DB를 통해 조회해오는 방식</U>**이다.

 <br>
데이터를 조회할 때 주로 사용하는 전략이 이 <U>Cache Aside</U> 전략이다. <br>
게시판에서 조회 기능을 구현하고 이를 배포했다고 가정하고 Cache Aside 작동 방식을 이해해보자.<br>
<br>

1. 처음 게시판 서비스를 배포하면 게시글이 존재하지 않는 상태이기 때문에 데이터베이스와 레디스에 아무런 데이터가 저장되어 있지 않다.
2. 일부 사용자가 들어와 게시글 작성을 함으로써 데이터를 저장한다. 이 데이터는 데이터베이스에 저장한다. (레디스에는 저장되지 않는다.)
3. 사용자가 게시물을 조회하려고 요청한다. 이 때, 데이터베이스로부터 바로 데이터 조회를 하기 전에 레디스에 있는 지 먼저 확인한다.
4. 레디스에 데이터가 없는 걸 확인한 뒤에 데이터베이스로부터 데이터를 조회해서 응답한다.
5. 데이터베이스로부터 조회한 데이터를 응답한 뒤에 레디스에도 데이터를 저장해둔다.
6. 다시 한 번 사용자가 데이터를 조회하려고 요청한다.
7. 레디스에 조회하고자 하는 데이터가 있는질 확인했더니 데이터가 존재해서 레디스로부터 데이터를 바로 가져온다.
   <br>

그러니까 정리하자면,<br>

**1. 캐시에 데이터가 있을 경우 (= Cache Hit)**
![다운로드 (1)](https://github.com/user-attachments/assets/e925d416-d8f9-4a5d-985a-71262457863a)
데이터를 요청했을 때 캐시(Redis)에 데이터가 있는 경우를 **<U>Cache Hit</U>**라고 한다.
<br>

**2. 캐시에 데이터가 없는 경우 (= Cache Miss)**
![다운로드 (2)](https://github.com/user-attachments/assets/1f273ec5-f7fc-4cee-b5b9-f6889477fb4c)
데이터를 요청했을 때 캐시(Redis)에 데이터가 없는 경우를 **<U>Cache Miss</U>**라고 한다.
<br>

### ✔️ Write Around 전략

> **<U>Write Around 전략</U>**은 **<U>쓰기 작업(저장, 수정, 삭제)을 캐시에는 반영하지 않고, DB에만 반영하는 방식</U>**이다.

 <br>
Cache Aside 전략이 데이터 조회와 관련된 전략이라면 Write Around 전략은 데이터를 어떻게 쓸 지(저장, 수정, 삭제)에 관련된 전략이다. <br>

![다운로드 (3)](https://github.com/user-attachments/assets/cbdd8c63-9373-4465-bf57-a69dca8ce949)

Write Around 전략은 데이터를 저장할 때 레디스에 저장하지 않고 데이터베이스에만 저장하는 것을 말한다. 그러다 데이터를 조회할 때 레디스에 데이터가 없으면 데이터베이스로부터 데이터를 조회해와서 레디스에 저장시켜주는 방식이다.
<br>
<br>

> ## Cache Aside, Write Around 전략의 한계와 해결 방법

### ✔️ Cache Aside, Write Around 전략의 한계점

#### **1. 캐시된 데이터와 DB데이터가 일치하지 않을 수 있다.**

Cache Aside와 Write Around 전략을 같이 썼을 때의 한계점 중 하나는 <span style="color: #FA5858">캐시된 데이터와 DB의 데이터가 일치하지 않을 수 있다</span>는 점이다. 즉, <span style="color: #FA5858">데이터의 일관성을 보장할 수 없다는 뜻</span><br>

두 방식을 같이 쓰는 건 현업에서도 많이 쓰는 방식이지만, 데이터를 수정할 때 DB만 업데이트 시키기 때문에 기존에 저장된 Redis의 데이터와 DB의 데이터는 다를 수밖에 없다.<br>

ex) 프로필 수정에서 내 이름을 '김보경'에서 '김보갱'으로 바꿨는데, 내 프로필 조회를 해봤더니 내 이름이 여전히 '김보경'이라고 표시되는 문제가 발생<br>

#### **2. 캐시에 저장할 수 있는 공간이 비교적 협소**

DB는 디스크(Disk)에 저장해서 많은 양을 저장하기 용이하지만, 캐시는 메모리(RAM)에 저장하기 때문에 DB에 비해 많은 양을 저장 할 수 없다.<br>
<br>

### 🤔 이 한계를 어떻게 극복할까?

**1. 캐시된 데이터와 DB데이터가 일치하지 않을 수 있다.**
: 캐시와 DB의 데이터를 일치시키기 위해, 데이터를 수정할 때마다 Redis와 DB에 동시에 업데이트시키면?<br>
→ 데이터는 일치할 것. 그러나 성능이 느려질 것<br>
그렇다고 성능 향상을 위해 DB의 데이터만 업데이트하면 캐시와 DB의 데이터가 불일치<br><br>
하지만 어쩔 수 없다. 어떤 선택을 하든 기회 비용(Trade Off)이 발생한다. 무언가를 얻으면 무언가를 포기해야 한다. 따라서 데이터 조회 성능 개선 목적으로 레디스를 쓰는 경우에는 데이터의 일관성을 성능 향상을 택한 것이다. <br>
<br>
이러한 이유로 캐시를 적용시키기에 적절한 데이터는 다음과 같다.<br>

- 자주 조회되는 데이터
- 잘 변하지 않는 데이터
- 실시간으로 정확하게 일치하지 않아도 되는 데이터
  <br>
  하지만 장기간 데이터가 일치하지 않는 건 문제가 될 수 있다. 따라서 적절한 주기로 데이터를 동기화시켜주어야 한다. 이 때 활용하는 기능이 레디스의 <span style="color: #239ED0">**<U>TTL 기능(만료 시간 설정 기능)</U>**</span>이다.<br>
  <br>
  일정 시간이 지나면 데이터가 캐시에서 삭제된다. 그럼 특정 사용자가 조회를 하는 순간 Cache Miss가 발생하여 DB의 데이터를 새로 조회해와서 캐시에 데이터를 넣게 된다. 즉, 데이터가 새롭게 갱신되는 효과가 있는 것!<br><br>

**2. 캐시에 저장할 수 있는 공간이 비교적 작다.**
: 위에서 활용했던 **<U>TTL 기능(만료 시간 설정 기능)</U>**을 활용하면 캐시의 공간을 효율적으로 쓸 수 있다. 자주 조회하지 않는 데이터는 만료 시간에 의해 데이터가 삭제될 테니까!

### ✅ 한줄 요약

Cache Aside, Write Around 전략을 사용할 때 주로 TTL을 같이 활용한다.

<br>
<br>

#### 🔗 &nbsp;학습 강의 영상

<iframe width="560" height="315" src="https://www.youtube.com/embed/PAXK20AxMMI?si=VxJoCyBNg5YDT_BM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
