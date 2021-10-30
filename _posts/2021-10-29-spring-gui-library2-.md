---
title: "스프링 (Spring Framework) 기반의 도서 관리 - 도서관 사이트 프로그램 제작기"

categories:
  - Spring
tags: 
  - Spring
  - Library
last_modified_at: 2021-10-29
---

드디어 졸업 작품을 완성했고 이제 밀렸었던 포스팅들을 하나씩 해보고자 한다.

이제 졸업 작품 전시전과 대학생활 마지막 학기의 기말고사만 남겨두고 있어 아직 일정이 비어있는 오늘 포스팅을 한다.

이전 포스팅 이후로 엄청 많은 시간이 지났다.

이 프로젝트를 진행하면서 작성했던 A4 용지를 못 찾았었기 때문이다.

물론 GIT 에서 README 를 통해 명세한 일지가 존재하지만 그래도 힘들게 완성했던 이 프로젝트의 추억이 있는 기록들을 잃어버리고 싶지 않았다.

참 다행히 사진으로도 해당 기록들을 찾을 수 있었고 이 글을 다시 작성해보고자 한다. 

## 도서 관리 프로젝트 목차

* Step 1. [스프링 (Spring Framework) 기반의 도서 관리 사이트 프로그램 소개](https://jee00609.github.io/spring/spring-gui-library1/)
* Step 2. [스프링 (Spring Framework) 기반의 도서 관리 - 도서관 사이트 프로그램 제작기](https://jee00609.github.io/spring/spring-gui-library2/)

## 도서 관리 프로젝트 구현 전 세팅

교수님께선 도서 관리 프로젝트는 2인 협력으로 구현하길 원하셨다.

따라서 4년동안 대학을 다니면서 나의 혈육보다 더 친하게 지낸 믿을만한 동기를 팀원으로 꼬셨고 참 다행히 함께 스프링 프로젝트를 완성할 전우를 구할 수 있었다.

2인 프로젝트와 1인 프로젝트의 차이점은 바로 동시에 개발을 해야한다는 점이다.

우리는 프로젝트 형상관리를 위해 Git 을 이용하기로 했다.

꾸준히 Git 을 통해 나의 프로젝트를 백업해왔지만 실제로 협업을 위해 사용해본건 처음이라 기대됬다.

## 도서 관리 프로젝트를 위한 아이디어 창출

우리 두명은 교수님이 필수로 구현하라고 했던 기능을 제외하고 더 많은 기능을 추가하고 싶었다.

10일 정도라는 아주 적은 시간 안에 프로젝트 완성 및 동영상 제작까지 해야했기 때문에 실제 도서관 사이트에서 제공하는 모든 기능을 구현할 순 없었다.

따라서 A4 용지를 하나 가져와서 프로젝트 제출 기간 내에 우리가 구현해보고 싶은 기능들을 써보면서 다양한 아이디어들을 얻을 수 있었다.

<figure class="align-center">
  <a href="/assets/images/2021-10-29-function.jpg"><img src="/assets/images/2021-10-29-function.jpg"></a>
  <figcaption>사용자와 관리자를 나눠 아이디어를 생각했다.</figcaption>
</figure>

교수님께선 사용자에 대한 기능만을 필수로 하셨지만 우리는 A+ 학점용 프로젝트를 완성하고 싶었고 관리자 기능까지 구현해보자고 결정했다.

## 사이트 디자인 구현

사이트 디자인은 국립 중앙 도서관과 경기도 사이버 도서관 웹사이트를 모티브로 디자인하였다.

국립 중앙 도서관에서는 헤더 네비게이션의 디자인을 참고하였고, 경기도 사이버 도서관에서는 신간,추천도서 섹션의 디자인을 참고했다.

<figure class="align-center">
  <a href="/assets/images/2021-10-29-motive.PNG"><img src="/assets/images/2021-10-29-motive.PNG"></a>
  <figcaption>국립 중앙 도서관 웹사이트 페이지</figcaption>
</figure>

<figure class="align-center">
  <a href="/assets/images/2021-10-29-motive2.PNG"><img src="/assets/images/2021-10-29-motive2.PNG"></a>
  <figcaption>경기도 사이버 도서관 웹사이트 페이지</figcaption>
</figure>

<figure class="align-center">
  <a href="/assets/images/2021-10-29-layout.jpg"><img src="/assets/images/2021-10-29-layout.jpg"></a>
  <figcaption>두 사이트를 참고했던 초기 디자인</figcaption>
</figure>
## 도서 관리 DB 구현

이 다음으로 DB 의 구조를 짰다.

DB는 처음에는 회원,도서 2가지를 구성하였으나, 관리자 기능을 제공하기 위해 더 많은 DB 를 구현해야 했다.

<figure class="align-center">
  <a href="/assets/images/2021-10-29-DB.jpg"><img src="/assets/images/2021-10-29-DB.jpg"></a>
  <figcaption>초기 DB 구조</figcaption>
</figure>

## 역할 구분

협업을 효율적으로 하려면 역할을 나눠 서로의 일을 해야한다.

그런데 가장 중요한 역할 분담이 쉽지 않았다.

왜냐하면 우리 팀원 모두 Web View 를 작성하는데 젬병이었기 때문이다.

우리는 서로의 코딩 실력이 더 낫다는 칭찬을 하며 서로가 Java 를 이용한 Service 를 구현하고 남에게 JavaScript 와 JSP 를 이용한 Web View 역할을 미루려고 했다.

그러나 나의 팀원이 진실된 눈빛을 하며 "난 정말로 Web View 는 자신이 없어" 라는 한 점 거짓없는 말의 진정성을 느끼고 결국 내가 Web View 를 담당하기로 했다.

물론 프로젝트가 Service 와 Veiw 만 있는 것도 아니고 다른 부분들은 서로 서로 도와가며 만들었다.

## 기능 구현

우리는 대략 7일만에 프로젝트를 완성했다.

10일이라는 기한에서 3일이나 단축할 수 있었던 이유는 우리 두명이 학과 근로로 일하고 있었기 때문이다.

근로라는 특권으로 학과 사무실에서 5일간 숙식을 제외한 모든 시간 동안 프로젝트를 구현했다.

그 7일 동안의 기록이 [Git 의 Push 목록](https://github.com/jee00609/LibraryManage/blob/master/src/main/resources/static/push/pushAlert.md)으로 남아있다.

<figure class="align-center">
  <a href="/assets/images/2021-10-29-contributors.PNG"><img src="/assets/images/2021-10-29-contributors.PNG"></a>
  <figcaption>7일 동안 269번이 넘는 Commits...</figcaption>
</figure>

## 느낀점

처음으로 Git 을 통해 형상관리 뿐만 아니라 협업도구로써 PR 을 해보았다.

팀원이 두명 뿐이다만 PR이  Merge 했을 때의 고양감이 있었다. 오픈소스 프로젝트들의 컨트리뷰터들이 열심히 Commit 및 PR 을 하는 이유를 알게 된 것 같다.

<figure class="align-center">
  <a href="/assets/images/2021-10-29-score.PNG"><img src="/assets/images/2021-10-29-score.PNG"></a>
  <figcaption>자랑스러운 A+</figcaption>
</figure>

프로젝트를 완성했을 때도 기분이 정말 좋지만 성적도 좋으면 기분이 두배로 행복해진다.

2인으로 협력해서 프로젝트를 진행함에 있어서 정말 좋은 경험을 한 것 같다.


## 비고

[프로젝트 전문](https://github.com/jee00609/LibraryManage)