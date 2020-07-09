---
title: "라즈베리 파이 4 Step 3 라즈베리 파이 한글 설정"

categories:
  - Hanium
tags: 
  - Raspberry PI 4
  - Error
  - Hanium
last_modified_at: 2020-07-09
---

이번 에러는 한글 깨짐 오류다.

라즈베리 파이 화면에서 라즈베리 아이콘을 누르면 Preferences 라는 것이 보일 것이다.

클릭 시 Rasberry Pi Configuration 이라는 버튼이 있을 텐데 Localisation 을 클릭하자.

Set Timezone 은 한국으로 변경해도 눈에 보이는 에러는 없다.

Locale 에서 Language: ko , Character Set: UTF-8 로 변경했을 때 한글 깨짐을 발견할 수 있다.

사각형 안에 4개의 숫자로 된 주사위 같은 문자들이 화면에 나타날 것이다.

이번엔 이 문제를 해결해보고자 한다.

<span style="color:gray"> 언젠가 이 Character Encoding 의 이름을 찾아볼 것!. </span>

[STEP 1 라즈베리 파이 OS 설치 및 무선 연결](https://jee00609.github.io/hanium/Raspberry-error-solved1/)

[STEP 1 라즈베리 파이 화면을 노트북에 띄우기](https://jee00609.github.io/hanium/Raspberry-error-solved2/)

## 필요한 준비물

늘 똑같다.

   * 라즈베리 파이 4
   * SD 카드
   * C타입 충전기
   * 노트북

## 실행 하는 방법

이번 문제는 시간이 좀 걸릴뿐 설치만 하면 된다.

   1. 라즈베리 파이 설정 변경
      * GUI 환경에서 변경
      * CLI 환경에서 변경
   2. 라즈베리 파이 업데이트 및 업그레이드
   3. 라즈베리 파이에 한글 폰트 설치

## 라즈베리 파이 설정 변경 (GUI)

   1. 라즈베리 파이 아이콘 클릭
   2. Preferences 버튼 클릭
   3. Rasberry Pi Configuration 버튼 클릭
   4. Localisation 버튼 클릭
      1. Locale 에서 Language: ko , Character Set: UTF-8 로 변경
      2. Keyboard 에서 Layout: Korean , Variant: Korean 으로 변경
   5. 재시작 해준다.

   ```ruby
sudo reboot
   ```

## 라즈베리 파이 설정 변경 (CLI)

나는 이 방식으로 하지 않았지만 CLI 에서 Localisation 을 변경할 수 있는 것 같다.

참고 가능한 사이트 : <https://freehoon.tistory.com/46>


## 라즈베리 파이 업데이트 및 업그레이드

띄워쓰기 조심하자

   ```ruby
sudo apt-get update
sudo apt-get upgrade
   ```

## 라즈베리 파이에 한글 폰트 설치

   ```ruby
sudo apt-get install fonts-unfonts-core ibus ibus-hangul -y 
sudo reboot
   ```

## 상세 이미지

<figure class="align-center">
  <img src="/assets/images/2020-07-09-success.PNG">
  <figcaption>성공!</figcaption>
</figure>

## 깨달은 점

   * 변경된 점이 없는 것 같으면 한번 재시작 해주는 것도 좋은 방법 같다.
   * 라즈베리 파이 전원을 C타입 충전기 뽑는 방식으로 끄지 말자.
   * 업글이랑 업뎃할 때 시간이 걸리는데, 용량이 부족한 건 아니다. 걱정 말자.

   ```ruby
// 재시작
sudo reboot

// 종료
sudo shutdown -h now

// 디스크 남은 용량 확인
df -h
   ```

## 참고 사이트

[참고했던 사이트인데 실패함 - 화면 띄우기](https://hiiambk.tistory.com/499)

[참고하면 좋은 사이트 - 라즈베리 파이 한글 설정하기](http://makeshare.org/bbs/board.php?bo_table=raspberrypi&wr_id=61)

[UNIX/LINUX : 용량 확인 명령어](https://ra2kstar.tistory.com/135)

[라즈베리파이 Raspbian 종료&재시작 명령어](https://mungrrrr.wordpress.com/2015/04/30/%EB%9D%BC%EC%A6%88%EB%B2%A0%EB%A6%AC%ED%8C%8C%EC%9D%B4-raspbian-%EC%A2%85%EB%A3%8C%EC%9E%AC%EC%8B%9C%EC%9E%91-%EB%AA%85%EB%A0%B9%EC%96%B4/)