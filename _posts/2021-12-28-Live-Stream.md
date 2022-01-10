---
title: "라이브 스트리밍 RTSP RTMP HLS 에 관한 정리"

categories:
  - Live Stream
tags: 
  - Live Stream
  - RTSP
  - RTMP
  - HLS
  - M3U8
  - TS
last_modified_at: 2021-12-28
---

실시간 스트리밍에 대해 공부할 필요성을 느꼈다.

## 생방송 스트리밍 (Livestreaming)
생방송 스트리밍 또는 라이브 스트리밍은 스트리밍 기술을 응용하여 디브이 카메라 등을 사용하여 컴퓨터의 네트워크를 통해 전송하여 생방송으로 스트리밍을 하는 것을 말한다.

## 기존 라이브 스트리밍 프로토콜
   * **RTSP (Real-Time Streaming Protocol)**
      * IETF (Internet Engineering Task Force) 가 개발한 통신 규약
      * 스트리밍 데이터를 제어하기 위한 방법을 제공
         * RTP (Real-time Transport Protocol) : RTSP를 통해 제어되는 미디어 데이터를 전송하는 데 사용되는 전송 프로토콜
      * 오디오, 비디오 등 멀티미디어 데이터를 포함하는 미디어 서버를 원격 조작하기 위한 프로토콜
   * **RTMP (Real-Time Messaging Protocol)**
      * 어도비 시스템즈 (Adobe Systems) 사의 독점 컴퓨터 통신 규약
      * 오디오, 비디오 및 기타 데이터를 인터넷을 통해 스트리밍 할때 사용


## RTSP (Realtime Transport Streaming Protocol)

실시간 스트리밍 프로토콜(Real Time Streaming Protocol, RTSP)은 실시간 속성을 가진 데이터 전송을 제어하기 위한 응용 프로그램 수준의 프로토콜이다.

RTSP는 오디오 및 비디오와 같은 실시간 데이터의 제어된 주문형 전송을 가능하게 하는 확장 가능한 프레임워크를 제공한다. 

데이터 소스에는 실시간 데이터 피드 및 저장된 클립이 모두 포함될 수 있다.

이 프로토콜은 여러 데이터 전송 세션을 제어하고, UDP, 멀티캐스트 UDP, TCP와 같은 전송 채널을 선택할 수 있는 수단을 제공하며, RTP에 기반한 전송 메커니즘을 선택하기 위한 수단을 제공하기 위한 것이다.


## RTMP (Real-Time Messaging Protocol)

RTMP는 Macromedia (현재 Adobe 소유)에서 개발하였으며 지연 시간이 짧은 주문형 콘텐츠를 효율적으로 스트리밍한다다.

RTMP는 인터넷을 통해 멀티미디어 파일을 이동하는 표준화된 방법으로오늘날 라이브 스트리밍 콘텐츠에 가장 일반적으로 사용되었다.


## RTSP 와 RTMP 공통 단점 - **HTTP 비호환**

RTMP 프로토콜은 HTTP 연결을 통해 RTMP 피드를 직접 스트리밍 할 수 없다. 

웹 사이트에서 RTMP 스트림을 사용하려면 Flash Media Server와 같은 특수 서버에 연결하고 타사 CDN (콘텐츠 전송 네트워크)을 사용해야 한다.

마찬가지로 RTSP 프로토콜은 HTTP를 통해 RTSP를 직접 스트리밍 할 수 없습니다.

물론 RTSP 프로토콜의 경우  RTSP는 기업 내 보안 시스템과 같은 사설 네트워크에서 비디오 스트리밍을 위해 더 많이 설계되었기 때문에 쉽게 스트리밍할 수 없는 것이다.

## **HLS (HTTP Live Streaming)**

이제 드디어 HLS 의 차례다.

HLS는 애플에 의해 2009년 제안된 라이브 비디오 스트리밍 프로토콜이다.

별도로 고가의 스트리밍 전용 미디어 서버를 구축해야 하는 기존의 방식과 다르게 HLS는 일반 웹서버에서도 라이브 스트리밍이 가능하다는 특징을 가지고 있다.

하나의 영상을 10초 단위로 쪼개어 재생 목록을 만든 후 이렇게 잘라진 짧은 비디오 조각을 일반적인 다운로드해서 재생하는 방식으로 기존의 웹서버를 그대로 사용할 수 있다는 매우 큰 장점이 있다.


## HLS 작동 방식 요약

<figure class="align-center">
  <a href="/assets/images/2021-12-28-HLS.PNG"><img src="/assets/images/2021-12-28-HLS.PNG"></a>
  <figcaption>HLS  작동 원리 요약</figcaption>
</figure>

1. Capturing devices (cameras, microphones, etc.) capture the content. (캡처 장치(카메라, 마이크 등)는 콘텐츠를 캡처합니다.)

2. The content is sent from the capturing device to a live video encoder. (콘텐츠는 캡처 장치에서 라이브 비디오 인코더로 전송 됩니다. )

3. The encoder transmits the content to the video hosting platform via RTMP. (인코더는 RTMP 를 통해 콘텐츠를 비디오 호스팅 플랫폼으로 전송합니다 .)

4. The video hosting platform uses HLS ingest to transmit the content to an HTML5 video player. (비디오 호스팅 플랫폼은 HLS 수집 을 사용 하여 콘텐츠를 HTML5 비디오 플레이어 로 전송합니다.)


## HLS 작동 상세

> 먼저 HLS 프로토콜은 MP4 비디오 콘텐츠를 .ts 파일 확장명(MPEG2 Transport Stream)을 사용하여 짧은(10초) 청크로 잘라냅니다.<br/><br/> 그런 다음 HTTP 서버는 이러한 스트림을 저장하고 HTTP는 이러한 짧은 클립을 장치의 시청자에게 전달합니다. <br/><br/> HLS는 H.264 또는 HEVC/H.265 코덱으로 인코딩된 비디오를 재생합니다.<br/><br/> HTTP 서버는 또한 비디오 청크에 대한 인덱스 역할을 하는 M3U8 재생 목록 파일 (예: 매니페스트 파일)을 생성합니다.<br/><br/> 이렇게 하면 단일 품질 옵션만 사용하여 라이브 방송 을 선택하더라도 파일이 계속 존재합니다.<br/> 이제 HLS 비디오 스트리밍에서 재생 품질이 작동하는 방식을 고려해 보겠습니다.<br/><br/> 이 프로토콜을 사용하면 지정된 사용자의 비디오 플레이어 소프트웨어 (예: HTML5 비디오 플레이어)가 네트워크 상태의 악화 또는 개선을 감지합니다. <br/> 둘 중 하나가 발생하면 플레이어 소프트웨어는 먼저 기본 색인 재생 목록을 읽고 이상적인 품질의 비디오를 결정합니다.<br/><br/> 그런 다음 소프트웨어는 품질별 인덱스 파일을 읽고 시청자가 보고 있는 지점에 해당하는 비디오 청크를 결정합니다.

비디오의 품질은 1080p 라거나 720p 등을 의미한다.

즉 위에서 의미한 '이상적인 품질의 비디오를 결정'한다는 것은 사용자가 직접 선택한 품질 혹은 AUTO 모드를 의미하며, 해당 선택을 통해 비디오의 재생 품질이 결정된다.

<figure class="align-center">
  <a href="/assets/images/2021-12-28-HLS2.png"><img src="/assets/images/2021-12-28-HLS2.png"></a>
  <figcaption>화질 변환의 원리</figcaption>
</figure>


## HLS Playlist

HLS의 playlist는 M3U 형식으로 작성이 되어있으며 UTF-8로 encoding 된다. 

HLS playlist 는 Master playlist와 Media playlist로 구분된다. 

Media playlist는 재생해야하는 segment가 정보가 연속적으로 등장한다. 

Master playlist를 이용하면 더 복잡한 streaming을 구현할 수 있다. 

Master playlist는 다양한 bitrate의 video 혹은 다양한 언어에 대한 audio stream에 대한 Media playlist포함 할 수 있다.

Master playlist에서는 Media playlist에 대한 정보를 기술하고 있으며, Media playlist에서는 Media segment에 대한 정보를 기술하고 있다.

<figure class="align-center">
  <a href="/assets/images/2021-12-28-HLS3.png"><img src="/assets/images/2021-12-28-HLS3.png"></a>
  <figcaption>HLS Playlist 구조</figcaption>
</figure>

아래에선 위의 이미지를 통해 HLS Playlist 구조의 요소들을 설명할 것이다.



## M3U8 과 구조

플레이리스트의 경로들과 재생시간을 가진 영상 스트리밍용 파일

```ruby
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:35
#EXT-X-MEDIA-SEQUENCE:0
#EXTINF:10,
index0.ts
#EXTINF:10,
index1.ts
#EXTINF:10,
index2.ts
#EXTINF:5,
index3.ts
#EXT-X-ENDLIST
```

* #EXTM3U
   * m3u8 파일 선언

* #EXT-X-VERSION:3
   * m3u8 버전3

* #EXT-X-TARGETDURATION:35
   * 총 재생시간 35초 

* #EXT-X-MEDIA-SEQUENCE:0
   * 파일이 많다면 이 재생목록의 순서

* #EXTINF:10,
   * 재생시간 10초

* index0.ts
   * 파일경로
* #EXT-X-ENDLIST
   * 파일 종료


## MPEG-2 TS (Transport Stream)

MPEG-2 TS는 MPEG-2 Part 1, Systems (ISO/IEC 13818-1 또는 ITU-T H.222.0)로 오디오나 비디오, 방송의 채널 정보 등을 전송하거나 저장하기 위해 정의한 규격이다.

즉 쉽게 말해서 ts 파일은 실제 스트리밍 영상 데이터이며, 시간 단위로 작게 쪼개져 있다.


## 비고

동영상을 보면서 자동으로 화질이 바뀌는 경험을 하는데 어떻게 이 것이 가능한지 궁금했었다.

그러다가 동영상을 다운받으려고 하는 과정에서 다양한 파일 형식을 만났다.

따라서 한번 제대로 공부해보자고 생각해서 이런 글을 작성하게 되었다.

## 참고 자료

[HLS 공식 자료](/assets/files/211228/StreamingMediaGuide.pdf)

[RTSP 에 대한 IETF 문서](https://www.ietf.org/rfc/rfc2326.txt)

[RTP 에 대한 IETF 문서](https://www.ietf.org/rfc/rfc3550.txt)

[IP 비디오 전송 기술 – 4.프로토콜 정리](https://dvnest.com/user_20210809/)

[HLS Playlist 에 대한 Apple 문서](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/AboutHTTPLiveStreaming/about/about.html)

