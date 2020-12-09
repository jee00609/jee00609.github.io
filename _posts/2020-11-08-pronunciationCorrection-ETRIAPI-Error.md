---
title: "ETRI 공공 인공지능 오픈 API 발음 교정 - ETRI API 발음 평가 사용법"

categories:
  - PronunciationCorrection
tags: 
  - API
  - Hanium
  - ETRI
last_modified_at: 2020-11-08
---

발음 교정 프로그램의 소개 다음으로 말하고 싶었던 건 ETRI API 를 사용하는 방법을 말하는 것이다.

ETRI의 음성 인식 기술이나 발음 평가 기술을 이용할 때 홈페이지 속 구현 예제에 비해 알아야할 것이 있었기 때문이다.


## 발음교정 문서

   * Step 1. [ETRI 공공 인공지능 오픈 API 발음 교정 - 초등학생을 위한 발음교정 프로그램 소개](https://jee00609.github.io/pronunciationcorrection/pronunciationCorrection/)
   * Step 2. [ETRI 공공 인공지능 오픈 API 발음 교정 - ETRI API 발음 평가 사용법](https://jee00609.github.io/pronunciationcorrection/pronunciationCorrection-ETRIAPI-Error/)

## ETRI 구현 예제

먼저 홈페이지에 나와있는 파이썬 구현 예제를 보자

   ```ruby
#-*- coding:utf-8 -*-
# 미리 설치해야 하는 모듈이다. 바로 아래 명령문 3개를 사용해서 설치해주자.
# pip install urllib3
# pip install jsonlib
# pip install pybase64

import urllib3
import json
import base64
openApiURL = "http://aiopen.etri.re.kr:8000/WiseASR/Pronunciation"
accessKey = "발급받은 API 키" #필수
audioFilePath = "자기 오디오 파일 위치" #필수 (예시 : audio/test.raw)
languageCode = "LANGUAGE_CODE" #필수, 어차피 english 밖에 없다.
script = "PRONUNCIATION_SCRIPT" #필수가 아니지만 발음 평가할 때 기준이 되는 문장을 의미한다.
 
file = open(audioFilePath, "rb")
audioContents = base64.b64encode(file.read()).decode("utf8")
file.close()
 
requestJson = {
    "access_key": accessKey,
    "argument": {
        "language_code": languageCode,
        "script": script, #필수가 아니기에 지워줘도 사용 가능하다.
        "audio": audioContents
    }
}
 
http = urllib3.PoolManager()
response = http.request(
    "POST",
    openApiURL,
    headers={"Content-Type": "application/json; charset=UTF-8"},
    body=json.dumps(requestJson)
)
 
print("[responseCode] " + str(response.status))
print("[responBody]")
print(str(response.data,"utf-8"))
   ```

## 음성 파일 주의 사항

발음 평가 API 를 사용할 때 가장 중요한 기준이 무엇일까?

바로 '사용자의 음성을 제대로 인식하고 있는가' 다.

처음 이 ETRI API 를 사용했을 때 5점 만점의 결과 중 1점만 나오는 문제가 있었다.

> 발음평가 API는 REST API이며, 발음평가에 사용하기 위해 샘플링 주파수(sampling rate 또는 sampling frequency) 16kHz로 녹음된 음성 파일을 Base64로 Encoding 하여 HTTP 통신으로 ETRI Open API 서버에 전달하면 됩니다. 

하지만 분명 16kHz 로 녹음한 음성 파일인데 제대로 인식을 못하는 문제가 발생한 것이다.

내 발음의 문제라고 생각했지만 홈페이지 데모에 있는 음성 파일을 가지고 실험했는데도 1점만 나오는 문제를 해결하고자 문의를 했었다.

> 음성 인식 API를 사용하기 위해서는 raw pcm data (16kHz Sampling rate, 16 bit short-int, little-endian) 포맷의 음원(60초 이내)을 사용하셔야 합니다.

덕분에 음성 파일의 구조 형식에 대해서 알게 되었다.

## RAW PCM

> PCM and WAV both format contains raw PCM data, the only difference is their header(wav contains a header where pcm doesn't).

PCM Data 란 무엇일까? 

PCM 데이터란 Header 없이 Raw Data 만 저장된 파일을 의미한다.

오디오 드라이버에서 오디오 데이터를 캡쳐했다면, 당연히 header가 없는 pcm 포맷이며 이때 오디오 드라이버가 어떤 상태(sampling rate, bit size, endian, channels)로 동작 중이 였는지에 따라 pcm 포맷을 해석해야 한다.

만일 데이터가 RIFF 포맷이라면 Little endian 형식이므로, wav header만 붙여주면 wav 오디오의 play가 가능해진다.

<figure class="align-center">
  <img src="/assets/images/2020-11-08-wav.jpg"/>
  <figcaption>WAV 형식 구조를 알아두자</figcaption>
</figure>

그렇다면 음성파일을 어떻게 만드는 것이 좋을까?

<span style="color:red">대략적으로 두가지 방법이 있다.<span/>

   * <span style="color:red">기존의 SW 프로그램인 Audacity 를 설치하여 제작하기 <span/>
      *  Audacity 를 이용하여 PCM 을 만드는 방법은 비고의 pcm음성파일제작 PDF 을 보면 된다.
   * <span style="color:red">직접 코드로 구현하기<span/>
      * 아래 나와있는 파이썬 코드가 PCM 형식의 RAW 파일로 음성을 녹음하는 코드다. 

## PCM 음성 파일 제작기 - SW 이용

가장 쉬운 방법이다. 자세한 내용은 비고에 PDF 를 올려둘 것이다.

오픈소스 기반 녹음 SW 인 [Audacity](https://www.audacityteam.org/)를 이용하는 것이다.

   1. Audacity 설치

   2. ### 녹음하기
      1. 녹음 채널 : 모노
      2. Sampling 주파수 : 16kHz
      3. 녹음 하기
      4. 파일 -> 내보내기 -> 오디오 내보내기
      5. 파일 형식 : 기타 비압축 파일
      6. 헤더 : RAW (header-less)
      7. 인코딩 : Signed 16bit PCM

   3. ### MP3 파일 열기
      1. Sampling 주파수 변경 (트랙 메뉴 -> 리샘플링(16000))
      2. 모노 채널 형태로 분할 (파일이름 클릭 -> 스테레오를 모노로 분할)
      3. 프로젝트 속도 설정 (16000)
      4. 파일 -> 내보내기 -> 오디오 내보내기
      5. 파일 형식 : 기타 비압축 파일
      6. 헤더 : RAW (header-less)
      7. 인코딩 : Signed 16bit PCM

## <span style="color:red">PCM 음성 파일 제작기 - 코드 구현<span/>

처음 녹음했던 방식의 코드는 꽤 길기 때문에 본 포스팅에는 내가 성공한 코드만 쓸 것이다.

이전의 코드는 깃허브 [히스토리](https://github.com/jee00609/Hanium_2020/commit/2668759b951123d3136670c5291ccd787b27ac20#diff-fccffd78ed617d9fa908a4bdde6beb2db98912d02f0a5294109c3341f57e75ad)로, 이전에 stereo 로 녹음한 wav 파일 만드는 법이 적혀있다.

   ```ruby
# 이 파이썬 코드를 실행하면 마이크를 통해 녹음한 음성을 PCM 형식의 음성파일로 바꿔서 저장합니다.
# sounddevice 모듈을 먼저 설치 하자!
# sounddevice 설치 방법 -> pip install sounddevice 으로 설치!

import sounddevice as sd

duration = 10 # seconds 녹음 시간 (초)
fs = 16000 # sampling frequency 샘플링 주파수

# default channel 은 2로, stereo 타입이니 변경 필요!
rec = sd.rec(duration * fs, samplerate=fs, channels=1, dtype='int16')
sd.wait()
pcm = rec.tostring()

# ETRI 에서 답변받은 것처럼 PCM 으로 된 RAW 파일을 저장!
with open('sampleAudio.raw', 'wb') as w: 
    w.write(pcm)
   ```

## 비고

   * [프로젝트 전문](https://github.com/jee00609/Pronunciation_Correction)

   * [convert-from-pcm-to-wav-is-it-possible](https://stackoverflow.com/questions/21131595/convert-from-pcm-to-wav-is-it-possible)

   * [WAV 파일의 헤더 구조와 Raw Data](https://anythingcafe.tistory.com/2)

   * [pcm음성파일제작 PDF](http://aiopen.etri.re.kr/data/pcm%EC%9D%8C%EC%84%B1%ED%8C%8C%EC%9D%BC%EC%A0%9C%EC%9E%91.pdf)