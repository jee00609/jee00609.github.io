---
title: "라즈베리 파이 4 Step 2 노트북 모니터로 라즈베리파이 화면 띄우기"

categories:
  - Hanium
tags: 
  - Raspberry PI 4
  - Error
  - Hanium
last_modified_at: 2020-07-08
---

라즈베리 파이 4 를 모니터 연결 없이 무선 연결 하는 법을 작성했었다.

[STEP 1 라즈베리 파이 OS 설치 및 무선 연결](https://jee00609.github.io/hanium/Raspberry-error-solved/)

원래는 매우 쉽고 간단하게 Micro HDMI 를 통해 바로 연결하고자 했다.

물론 이 글을 쓰는 이유처럼 HDMI 로 연결 하지 못했다.

<figure class="align-center">
  <img src="/assets/jjal/ggang.jpg" width= '100'>
  <figcaption>누구나 그럴싸한 계획을 가지고 있다. 화면이 그대로이기 전까지는</figcaption>
</figure>

원격으로 다른 사람 모니터도 띄우는 요즘 세상이다.

인터넷만 연결되있으면 어떻게든 라즈베리 파이 화면을 노트북에 띄울 수 있다.

## 필요한 준비물

저번 준비물하고 달라진 점은 없다.

   * 라즈베리 파이 4
   * SD 카드
   * C타입 충전기
   * 노트북

## 실행 하는 방법

   1. 라즈베리 파이에 TightVNC server 설치
   2. 컴퓨터에 TightVNC 설치
   3. 라즈베리 파이에서 설정 변경
   4. 컴퓨터에서 연결하기

## 라즈베리 파이에 TightVNC server 설치

띄워쓰기 조심하자

   ```ruby
sudo apt-get install tightvncserver
   ```

## 컴퓨터에 TightVNC 설치

[TightVNC 설치 사이트](https://tightvnc.com/download.php)

컴퓨터 사양에 따라서 알맞게 다운받고 (본인은 64bit 로 설치함), Typical 타입 선택 후 변동없이 진행했다.

마지막엔 비밀번호 설정하라는데 늘 쓰던 비밀 번호로 작성했다.

<span style="color:red"> 8글자로 제한된다고 하니 조심할 것! </span>

## 라즈베리 파이에서 설정 변경

   * 첫 Password : 현재 라즈베리 파이 4 비밀번호를 의미
   * Password, Verify : 접속할 때 사용할 비밀번호, 비밀번호 확인용

   ```ruby
su pi -c /usr/bin/tightvncserver : 1
Password:

You will require a password to access your desktops.

Password:
Verify:
Would you like to enter a view-only password (y/n)? y
   ```

## 상세 이미지

<figure class="align-center">
  <img src="/assets/images/2020-07-08-success.PNG">
  <figcaption>성공!</figcaption>
</figure>

## 깨달은 점

   * 연결했을 때 와이파이 다른 걸로 바꿀려고 하지 말자
   * 소켓 연결 실패와 함께 SD 카드에 새로 라즈베리 OS 를 설치해야만 했다...

## 참고 사이트

[참고 사이트](https://hiiambk.tistory.com/499)