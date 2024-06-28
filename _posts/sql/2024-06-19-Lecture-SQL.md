---
title: 📟 SQL & Database - sql문 작성할 때 참고할 것들 모음📂
author: bokyung
date: 2024-06-19 00:00:00 +0800
toc: true
pin: false
published: true
categories: [Lecture, 한 번에 끝내는 SQL & Database]
tags: [SQL, MariaDB, Database, RDBMS]
image: https://codingapple.com/wp-content/uploads/2022/09/%EC%83%81%ED%92%88%EC%82%AC%EC%A7%84%EC%98%A8%EB%9D%BC%EC%9D%B8-%EB%B3%B5%EC%82%AC23.png
---
<!-- 글자색 넣기 <span style="color: #239ED0">    </span>  -->
<!-- 띄어쓰기   &nbsp;   -->
<br>
<br>
학습환경 : Windows, MariaDB, DBeaver
<br>
<br>

> ## MAX, MIN 대신 LIMIT 

<br>
데이터가 너무 많은 환경에서 MAX나 MIN을 쓰게되면 너무 오래 걸릴 수도 있음<br>
그럴땐 ORDER BY로 DESC나 ASC 정렬하고 LIMIT 1을 사용해 맨 위의 자료만 출력하면 같은 값을 도출함<br>

데이터가 많을 땐 둘 다 테스트 해보고 빠른걸 사용하도록 하자

 - MAX 사용시
 ```sql
  SELECT MAX(price) FROM product;
 ```
 - ORDER BY + LIMIT 사용시
 ```sql
  SELECT * FROM product ORDER BY price DESC LIMIT 1; 
 ```

 결과는 같음!
<br>
<br>

> ## 서브쿼리

<br>
문자나 숫자 데이터를 1개만 뱉는 쿼리문을 작성하여 서브쿼리로 사용할 수 있는데,
IN() 안에서는 예외적으로 여러개의 행을 뱉는 서브쿼리문 작성가능
<br>
<br>

> ## TABLE 대신 VIEW?

<br>
view는 실제 테이블처럼 사용할 수 있는 가상의 테이블이라고 할 수 있다<br>

- 언제 사용? <br>
     - join같은 작업을 하고 select해서 얻은 테이블을 저장해서 사용하고 싶을 때
     - table에 컬럼 변경이 필요할 때 미리 실험해보는 용도 등등
<br> 
    
create table해서 실제 테이블로 만들어 저장해도 되겠지만 view는 실제 테이블이 아니라서 테이블만큼 하드 용량을 많이 차지하지 않음! <br>
<br>
<br>
(적어둘 게 생길 때 마다 계속 업데이트 예정.. 🫠)