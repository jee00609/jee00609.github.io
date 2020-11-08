---
title: "공공 인공지능 오픈 API 발음 교정 - 초등학생을 위한 발음교정 프로그램"

categories:
  - PronunciationCorrection
tags: 
  - API
  - Hanium
  - ETRI
last_modified_at: 2020-11-01
---

한이음 2차 제출이 끝났다.

그동안 새롭게 만든 기능인 발음 교정 프로그램을 로봇과 연동하면서 있었던 일들을 기록하고자 한다.

이번엔 퀵드로우 포스팅과는 달리 먼저 프로그램에 대한 설명을 먼저 하고자 한다.

## 발음교정 문서

   * Step 1. [공공 인공지능 오픈 API 발음 교정 - 초등학생을 위한 발음교정 프로그램 소개](https://jee00609.github.io/pronunciationcorrection/pronunciationCorrection/)
   * Step 2. [공공 인공지능 오픈 API 발음 교정 - ETRI API 발음 평가 사용법](https://jee00609.github.io/pronunciationcorrection/pronunciationCorrection-ETRIAPI-Error/)

## PronunciationCorrection

공공 인공지능 오픈 API·DATA 서비스 포털의 [발음 교정 API](http://aiopen.etri.re.kr/index.php) 를 이용하여 만든 초등학생 대상 영어 교육용 콘텐츠 입니다.

[초등학교 교사 블로거님](https://hsamnonsul.tistory.com/)의 블로그에서 2003년도 초등 실전 영어 회화의 문장을 이용하여 만들었으며 사용자의 영어 발음을 평가하여 점수를 시각적으로 표현합니다.

## 사용법

  1. pronunciationCorrection 파일을 실행한다.

  2. Level 을 선택한다.
      1. voice 버튼을 누르면 현재 발음해야할 문장을 들려준다.
      2. rec 버튼을 누르면 사용자의 문장을 최대 5초 녹음합니다.
      3. Go! 버튼을 누르면 사용자의 발음을 평가를 시각화합니다.

## 이미지

### 실제 플레이 화면

<figure class="align-center">
  <img src="/assets/images/2020-11-01-PC.png">
  <figcaption>사용 이미지</figcaption>
</figure>

### 실제 플레이 화면 동영상

<figure class="align-center">
  <img src="/assets/images/2020-11-01-PC-robot.gif">
  <figcaption>로봇에서 사용한 모습</figcaption>
</figure>

## 비고
  * [초등학교 영어 문장](http://webcache.googleusercontent.com/search?q=cache:Axn_gfuyaeAJ:hsamnonsul.tistory.com/attachment/cfile6.uf%4013560B374FFC53A427D2FC.hwp+&cd=4&hl=ko&ct=clnk&gl=kr)

  * [프로젝트 전문](https://github.com/jee00609/Pronunciation_Correction)