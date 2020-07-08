---
title: "라즈베리 파이 4 Step 1 모니터 없이 무선 연결 하기"

categories:
  - Hanium
tags: 
  - Raspberry PI 4
  - Error
  - Hanium
last_modified_at: 2020-07-06
---

한이음에서 라즈베리 파이를 사용해야 했다.

라즈베리 파이 4 를 모니터 연결 없이 무선 연결 하는 법을 기억하기 위해 작성한다.

## 라즈베리 파이 생김새

<figure class="align-center">
  <img src="/assets/images/2020-07-06-Ras.jpg">
  <figcaption>라즈베리 파이는 뒷면에 SD 카드, 앞면에선 C타입으로 충전 가능하다</figcaption>
</figure>

현재 사용한 라즈베리 4는 Raspberry Pi 4 Computer Model B 4GB RAM 이다.

SD 카드 넣는 곳은 뒷면에 친절히 적혀 있기 까지 했다. 뒷면을 잘 살펴보자

충전은 집에서 핸드폰 충전하는 C타입 충전기로도 충전 가능했다.

## 필요한 준비물

   * 라즈베리 파이 4
   * SD 카드
   * C타입 충전기
   * 노트북

## 설치 방법
  
   1. [라즈베리 파이 사이트](https://www.raspberrypi.org/downloads/)에서 OS를 노트북에 다운받는다.
      1. 다운 받은 것은 recommended software 라고 적힌 것으로 다운로드 시간이 꽤 길었다.
   2. SD 카드를 노트북에 꽂고 포맷시킨다.
      1. SD 카드 인식 오류 시 [해결법](https://jcom.tistory.com/17) 으로 해결 가능하다.
   3. [etcher](https://www.balena.io/etcher/)를 통해 SD카드에 OS를 쓰기 시킨다.
      1. 쓰기 완료 후 SSH, wpa_supplicant.conf 파일을 만든다.
      2. [다운로드-SSH](/assets/files/200706/SSH)
      3. [다운로드-wpa](/assets/files/200706/wpa_supplicant.conf)
   4. 쓰기 완료 된 SD 카드를 라즈베리 파이에 꽂는다.
   5. 라즈베리 파이에 전원을 연결한다.

## 무선 연결 방법

   1. 윈도우 검색 창에서 '핫스팟'을 검색한다.
   2. 모바일 핫스팟에서 '인터넷 연결 공유 킴' 으로 설정한다.
   3. 전원이 켜진 라즈베리 파이가 연결된 장치에 뜨길 기다린다.
   4. 라즈베리 파이가 연결되길 기다리면서 [PUTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) 를 다운받는다.
   5. 라즈베리 파이가 연결된 장치에 이름이 뜨면 IP 주소를 복사한다.
   6. IP 주소를 PUTTY 의 Host주소에 적고 open 한다.
   7. 라즈베리 파이의 기본 ID는 pi, PW 는 raspberry 다.
   8. 성공하길 빌자

## 참고 이미지

<figure class="align-center">
  <img src="/assets/images/2020-07-06-Hotspot-explain.PNG">
  <figcaption>네트워크 이름과 암호는 쉬운걸로 하자</figcaption>
</figure>

<figure class="align-center">
  <img src="/assets/images/2020-07-06-success.PNG">
  <figcaption>라즈베리 파이 SSH 연결 성공</figcaption>
</figure>

## 깨달은 점

   * 라즈베리 파이 전원은 SD 카드를 꽂은 후 연결하자

## 참고 사이트

[라즈베리 파이](https://www.raspberrypi.org/)

[Etcher](https://www.balena.io/etcher/)

[SD 카드 인식 불가](https://jcom.tistory.com/17)

[PUTTY](https://www.putty.org/)

[내용이 이해가 안되면 참고해야 하는 사이트](https://developer-mistive.tistory.com/2)

[라즈베리 파이 암호 변경](https://withcoding.com/49)