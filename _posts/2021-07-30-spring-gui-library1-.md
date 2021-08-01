---
title: "스프링 (Spring Framework) 기반의 도서 관리 - 도서관 사이트 프로그램 소개"

categories:
  - Spring
tags: 
  - Spring
  - Library
last_modified_at: 2021-07-30
---

저번 1학기에 Spring 수업을 들으면서 CLI 와 GUI 기반의 도서 관리 프로그램을 제작했었다.

이 두 프로젝트 덕분에 MVC 패턴으로 프로젝트를 구현하는 법과 Github 기반의 형상관리 및 협력 방식을 배울 수 있었고 좋은 점수 또한 받을 수 있었다.

오늘 [프로젝트 전문](https://github.com/jee00609/LibraryManage) 의 README 까지 최종적으로 작성했다.

따라서 1학기 Spring 수업을 들으면서 가장 기억에 남은 도서 관리 프로그램의 소개와 제작기를 포스팅하며 회고하려 한다.

## 도서 관리 프로젝트 목차

* Step 1. [스프링 (Spring Framework) 기반의 도서 관리 사이트 프로그램 소개](https://jee00609.github.io/spring/spring-gui-library1/)
* Step 2. 스프링 (Spring Framework) 기반의 도서 관리 - 도서관 사이트 프로그램 제작기 (추 후 업데이트)

## 도서 관리 프로그램 기본 세팅

   * 스프링 프레임워크 버전 : 5.3.7
   * MySQL 사용 - JavaConfig 에서 변경가능
      * UserName : root
      * Password : rootoor
   * LocalHost 8888 - application.properties 에서 변경 가능

## 사용법

1. [프로젝트](https://github.com/jee00609/LibraryManage) 를 자신의 컴퓨터에 Import 하여 실행해 주시면 됩니다.

2. 자세한 사용법은 [사용자 매뉴얼](https://github.com/jee00609/LibraryManage/blob/master/src/main/resources/static/pdf/Spring_MinGW's_%EC%82%AC%EC%9A%A9%EC%9E%90_%EB%A7%A4%EB%89%B4%EC%96%BC.pdf) 을 참고해주시길 바랍니다.


## 소개 동영상

<iframe width="560" height="315" src="https://www.youtube.com/embed/_joRphN1b_w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 프로젝트 구조 UML

<figure class="align-center">
  <a href="/assets/images/2021-07-30-libraryDEV_ClassDiagram_UML.png"><img src="/assets/images/2021-07-30-libraryDEV_ClassDiagram_UML.png"></a>
  <figcaption>UML</figcaption>
</figure>


## 관리자 기능

* 도서
   * 도서 추가 
   * 도서 삭제 
   * 도서 수정 
   * 연체 도서 확인
  
* 공지 사항
   * 공지 사항 추가 
   * 공지 사항 삭제 
  
* 추천 도서
   * 추천 도서 추가 
   * 추천 도서 삭제 
  
* 게시물 비공개 설정
   * 게시글 테이블 생성하기 
   * 댓글 테이블 생성하기 
   * 게시글 목록 페이지 생성하기 
   * 게시글 세부 페이지 생성하기 (With 댓글) 
   * 게시글 작성 페이지 생성하기 
   * 관리자 게시물 비공개 페이지 

* 회원
   * 회원 목록 
   * 회원 블랙리스트 
   * 회원 신청 도서 목록 조회 
   * 임시 비밀번호 이메일로 전송 


## 사용자 기능
    
* 회원
   * 회원가입
   * 로그인
   * 비밀번호 수정
   * 비밀번호 잊어버렸을 시 임시 비밀번호 요청
  
* 도서
   * 도서 대여
   * 도서 반납
   * 도서 검색
   * 도서 신청
  
* 내 서재
   * 연체 도서 확인
   * 대여 기간 연장

* 조회
    * 신간 도서 조회
    * 사서 추천 도서 조회
    * 공지사항 조회

## 비고

[프로젝트 전문](https://github.com/jee00609/LibraryManage)
