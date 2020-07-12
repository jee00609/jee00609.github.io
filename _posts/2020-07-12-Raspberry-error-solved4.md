---
title: "라즈베리 파이 4 Step 4 공식 7 인치 디스플레이와 연결하기"

categories:
  - Hanium
tags: 
  - Raspberry PI 4
  - Error
  - Hanium
last_modified_at: 2020-07-08
---

한이음에서 디스플레이를 주문했지만 아직 도착하진 않았다.

그래서 같은 팀의 선배님이 자기가 가진 라즈베리 파이 용 공식 LCD 7인치 디스플레이를 빌려주셨다.

<figure class="align-center">
  <img src="/assets/jjal/fan.jpg" width= "150px">
  <figcaption>감사합니다!</figcaption>
</figure>

[STEP 1 라즈베리 파이 OS 설치 및 무선 연결](https://jee00609.github.io/hanium/Raspberry-error-solved1/)

[STEP 2 라즈베리 파이 화면을 노트북에 띄우기](https://jee00609.github.io/hanium/Raspberry-error-solved2/)

[STEP 3 라즈베리 파이 한글 설정](https://jee00609.github.io/hanium/Raspberry-error-solved3/)

## 필요한 준비물

저번 준비물하고 달라진 점은 없다.

   * 라즈베리 파이 4
   * SD 카드
   * C타입 충전기
   * [7인치 LCD Display](https://www.raspberrypi.org/products/raspberry-pi-touch-display/)

## 실행 하는 방법

   1. LCD Display 부품 합치기
   2. 라즈베리 파이와 연결하기
   3. 라즈베리 파이의 전원 켜기

## LCD Display 부품 합치기

<figure class="align-center">
  <img src="/assets/images/2020-07-12-displays.png">
  <figcaption>여러 부품들이 보인다.</figcaption>
</figure>

[회로에 선 꼽기 전까진 이 방법으로 합쳐주기](https://www.youtube.com/watch?time_continue=219&v=cUScoj-n6zg&feature=emb_title)

위 사이트 대로 회로 선을 꼽아주면 화면이 검정색으로만 존재한다.

DSI 리본 케이블 붙이는 방법 + 라즈베리 파이와 LCD 디스플레이 볼트로 연결하는 법까지만 참고하자

## <span style="color:red"> 라즈베리 파이와 연결하기 </span>

솔직히 여기서 도대체 어디와 연결하는지 눈앞이 캄캄해진다.

꼽는데는 많고 뭐가 뭔지는 감이 안잡힌다.

그래서 여러 자료를 찾아봤다.

<figure class="align-center">
  <img src="/assets/images/2020-07-12-GPIO-Pinout-Diagram.png">
  <figcaption>라즈베리 파이 회로</figcaption>
</figure>

<figure class="align-center">
  <img src="/assets/images/2020-07-12-display.PNG">
  <figcaption>LCD 디스플레이 뒷면</figcaption>
</figure>

위의 사진들이 이 포스팅의 핵심이다.

라즈베리 파이 회로 사진 보면 각 핀들이 무엇을 의미하는지 나와있다.

따라서 핀에 알맞게 꽂아주면 게임 끝이란 소리!

말로 설명하기 힘드니 직접 그림을 그렸다.

<figure class="align-center">
  <img src="/assets/images/2020-07-12-connect.jpg">
  <figcaption>연결 방법</figcaption>
</figure>

## 라즈베리 파이의 전원 켜기

라즈베리 파이에 C타입 충전기로 전원을 연결해주면 화면이 켜진다.

<figure class="align-center">
  <img src="/assets/images/2020-07-12-success.jpg">
  <figcaption>성공!</figcaption>
</figure>

## 깨달은 점

   * 알맞은 핀에 꼽자.
   * 핀을 모두 꼽고 나서 전원을 켜주자

## 참고 사이트

[참고 사이트 - Official Raspberry Pi 4 7" Touchscreen Display Review](https://www.youtube.com/watch?v=J69-bxOSMC8&t=246s)