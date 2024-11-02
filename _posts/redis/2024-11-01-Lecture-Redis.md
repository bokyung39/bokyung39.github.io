---
title: 🧰 Redis (01) - Redis 기본 명령어, Key 네이밍 컨벤션
author: bokyung
date: 2024-11-01 00:00:00 +0800
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

<br>
<br>
학습환경 : Mac, iTerm
<br>
<br>

> ## Redis 기본 명령어

### ✔️ &nbsp;Redis 실행 / 실행 여부 확인 / 중지

```shell
# redis 실행
brew services start redis

# redis 실행 여부 확인
brew services info redis

# redis 중지
brew services stop redis
```

<img width="724" alt="image" src="https://github.com/user-attachments/assets/d91a5baa-9f35-4c8a-9406-8a8906cb487d">{: width="80%" height="80%" .normal}

### ✔️ &nbsp;Redis 접속

```shell
redis-cli # Redis에 접속

127.0.0.1:6379> ping
PONG # 이렇게 출력되면 정상적으로 Redis가 실행되고 있다는 뜻
```

<img width="723" alt="image" src="https://github.com/user-attachments/assets/9143a3fd-d229-4ef4-acc3-718d314d7981">{: width="80%" height="80%" .normal}

<br>

### ✔️ &nbsp;데이터(Key, Value) 저장하기

```shell
# set [key 이름] [value]
# 데이터 저장 성공 시 OK가 출력됨

set bokyung:name "bokyung kim" # 띄어쓰기해서 저장하려면 쌍따옴표로 묶어주면 됨
set bokyung:hobby game
```

### ✔️ &nbsp;데이터 조회하기 (Key 값으로 Value 값 조회하기)

```shell
# get [key 이름]
# key 값에 해당하는 value 값이 출력됨

get bokyung:name # "bokyung kim" 출력됨
get bokyung:hobby # game 출력됨

get bk:name # 없는 데이터를 조회할 경우 (nil)이라고 출력됨
```

### ✔️ &nbsp;저장된 모든 key 조회하기

```shell
keys *

# 1) "bokyung:name"
# 2) "bokyung:hobby"

# key가 없는 경우 (empty array) 출력
```

### ✔️ &nbsp;데이터 삭제하기 (Key 값으로 데이터 삭제하기)

```shell
# del [key 이름]
# 삭제된 key의 index를 출력

del bokyung:hobby # (integer) 1 출력

get bokyung:hobby # 삭제됐는 지 확인 -> (nil) 출력
```

### ✔️ &nbsp;데이터 저장 시 만료시간(TTL) 정하기

```shell
# set [key 이름] [value] ex [만료 시간(초)]
# 영구적으로 데이터를 저장하지 않고 임계점을 정해 저장할 수 있음
# (인메모리 공간이기 때문에 디스크보다 작기 때문에 TTL을 자주 적용)

set bokyung:pet cat ex 15
```

### ✔️ &nbsp;만료시간(TTL) 확인하기

```shell
# ttl [key 이름]
# 만료 시간이 몇 초 남았는 지 반환
# 키가 없는 경우 -2를 반환
# 키는 존재하지만 만료 시간이 설정돼 있지 않은 경우에는 -1을 반환

ttl bokyung:pet # 남은 시간 출력 -> 예) (integer) 10 , 만료되었다면 (integer) -2 출력
ttl bokyung:name # (integer) -1 출력
ttl bk:name # (integer) -2 출력
```

<img width="514" alt="image" src="https://github.com/user-attachments/assets/00326adb-04c9-4ccf-afae-bc025e081571">{: width="80%" height="80%" .normal}

### ✔️ &nbsp;모든 데이터 삭제하기

```shell
flushall # 성공 시 OK 출력
```

<br>
<br>

> ## Key 네이밍 컨벤션

### ✔️ &nbsp;콜론(**:**)을 활용해 계층적으로 의미를 구분해 사용

- **users:100:profiles** : 사용자들(users)중에서 PK가 100인 사용자(user)의 프로필(profile)
- **products:123:details** : 상품들(products)중에서 PK가 123인 상품(product)의 세부사항(details)
