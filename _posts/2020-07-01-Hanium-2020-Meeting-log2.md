---
title: "한이음 회의 준비 교육용 프로그램 자료 수집"
categories:
  - Life
  - Hanium 
tags:
  - Life
  - Raspberry pi 

last_modified_at: 2020-07-01
---

# 어린이들을 위한 교육용 기능 추가하기

## 어떻게 만들 것인가?

   * 알렉사 커스텀 스킬로 만든다.
      * Stroyline 무료툴이 존재
   * 안드로이드에서 어플리케이션을 만든다.
      * 직접 커스텀 할 수 있다는 장점이 존재

## 알렉사 스킬에 대하여

   * 클라우드 내에서 실행되는 프로그램과 같은 것
   * <span style="color:red"> 디스플레이없이 오로지 소리로만 인식, 대답하는 프로그램 </span>
   * 알렉사 커스텀 스킬은 사용자가 직접 스킬을 제작하는 것을 의미한다.
   * 아마존 알렉사와 연동이 가능한 Prototype SDK가 존재하는 것 같다

[참고하기 좋은 사이트 - 알렉사 SDK](https://developer.amazon.com/en-US/docs/alexa/alexa-voice-service/register-a-product.html)

## 알렉사 커스텀 스킬을 통해 만들 수 있는 교육용 프로그램

알렉사를 이용하게 된다면 음성만을 이용한 프로그램을 만들어야 한다. 

   * 동물의 음성을 들려주고 그 동물이 무엇인지 맞추는 게임
   * 알렉사가 물건 (또는 직업?) 등을 설명하고 그 것이 무엇인지 맞추는 게임

## 알렉사 커스텀 스킬 시나리오

   1. 준비 단계
      1. 서버 데이터베이스에 (넘버 , 음성, 정답) 테이블을 만들어 데이터 삽입
   
   2. 알렉사를 작동 시작
      1. 알렉사 run Custom_Name
      2. 알렉사가 특정 물건,동물,직업과 같은 무언가를 영어로 설명한다.
      3. 사용자가 대답한다.
      4. 알렉사가 듣고 대답이 맞는지 아닌지 확인한다.
         1. 참 
            1. Correct 라는 음성을 뿌린다
         2. 거짓 
            1. Incorrect 라는 음성을 뿌리고 정답을 알려준다.

## 안드로이드 스튜디오 또는 비주얼 스튜디오와 같은 IDE 를 이용한 프로그램

   * 라즈베리 파이와 연동 가능
   * AWS 와 연동 가능
   * Alexa 와 연동 가능 

[참고하기 좋은 사이트 - Alexa SDK](https://developer.amazon.com/en-US/docs/alexa/avs-device-sdk/android.html)

## 안드로이드 스튜디오 프로그램 시나리오

   1. 핸드폰 어플리케이션 시작
   2. 사용자 화면에서 2가지 혹은 4가지의 물건, 동물의 이미지 출력
   3. 사용자 화면에서 특정 물건에 대한 음성 설명 출력
   4. 사용자가 화면을 클릭
      1. 참
         1. Correct 라는 음성을 뿌린다.
         2. 라즈베리 파이 디스플레이에 기쁜 Emotion 출력
      2. 거짓
         1. InCorrect 라는 음성을 뿌린다.
         2. 라즈베리 파이 디스플레이에 슬픈 Emotion 출력