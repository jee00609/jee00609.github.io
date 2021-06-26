---
title: "윈도우 11 과 TPM2.0, TMP2.0 이란 무엇일까"

categories:
  - IT News
tags: 
  - TPM
  - Window 11

last_modified_at: 2021-06-26
---

2021년 6월 25일 [Window 11 의 시스템 요구 사항](https://www.microsoft.com/ko-kr/windows/windows-11-specifications) 에서 TPM 2.0 이 명시되었다.

Microsoft는 2016 년의 시점에서 Windows 10 탑재기에 TPM 2.0 구현의 필요성을 이야기 했었고, 올해 (2021년) 후반의 Windows 11의 출시를 계기로 본격적으로 TPM 필수화를 목표로하고 있다고 생각된다.

<figure class="align-center">
  <a href="/assets/images/2021-06-26-window11.PNG"><img src="/assets/images/2021-06-26-window11.PNG"></a>
  <figcaption>윈도우 11 의 하드웨어 요구 사항 및 최소 사양</figcaption>
</figure>

특히 마이크로소프트가 7월 28일부터 PC는 물론 스마트폰과 태블릿 등 윈도우 10을 탑재하는 모든 디바이스에 TPM (Trusted Platform Module) 2.0 하드웨어 기반 보안 계층을 의무화한다.

본인은 이번에 처음으로 TPM 이란 개념을 들었기 때문에 여러 자료를 찾아보았고 아주 조금이나마 이해할 수 있었다.

그래서 나와 같은 사람을 위해 이번 포스팅을 통해 TPM 이 무엇인지 알아보고자 한다.

## TPM 이란?

TPM 은 Trusted Platform Module 의 약자로, 신뢰할 수 있는 플랫폼 모듈을 뜻합니다.

TPM (신뢰할 수 있는 플랫폼 모듈) 기술은 하드웨어 기반의 보안 관련 기능을 제공하도록 설계되었습니다.

TPM 칩은 암호화 작업을 수행하도록 설계된 보안 암호화 프로세서입니다. 

칩에는 변조를 방지하는 여러 가지 실제 보안 메커니즘이 포함되어 있으며, 악성 소프트웨어가 TPM의 보안 기능을 변조할 수 없습니다.

## TPM 의 역할

간단히 말하면, 암호화에 사용하는 키를 안전한 장소에서 관리하기위한 구조입니다.

암호화 알고리즘 엔진, 해시 엔진, 키 생성기, 난수 생성기, 비 휘발성 메모리 (열쇠 등을 보관) 등을 갖춘 모듈에서 TPM의에 암호화 키 생성 및 사용 제한을하기 위해 이용되고 합니다.

<figure class="align-center">
  <a href="/assets/images/2021-06-26-TPM.PNG"><img src="/assets/images/2021-06-26-TPM.PNG"></a>
  <figcaption>TPM 의 활용</figcaption>
</figure>

예를 들어 금고를 잠글 경우, 금고와 열쇠를 같은 위치에 두면 금고가 열릴 가능성이 높습니다.

그러나 열쇠를 금고와는 다른 위치 (예 : TPM)에 보관하고 열쇠를 꺼낼 사람을 엄격하게 관리한다면 안전하게 내용을 보호할 수 있습니다.

TPM 2.0 보안 계층은 칩이나 펌웨어 형태로 구현되며, 신뢰할 수 있는 컨테이너에 암호화 키를 저장해 관리하여 사용자 데이터 보호 수준을 높이는 기능을 수행합니다.

## TPM1.2 와 TPM2.0

TPM은 1.2 와 2.0이 존재합니다.

TPM 2.0은 TPM 1.2 에 비해 기능이 대폭 강화되었고 사양도 크게 다릅니다. 

TPM 2.0은 TPM 1.2 보다 정교한 암호화 알고리즘을 지원합니다.

또한 보다 표준화 된 경험을 제공하며 가장 중요한 것은 CPU에 통합 될 수 있습니다.

구체적으로는 암호화 알고리즘으로 기존의 RCA 이외에 ECC를 이용할 수 있게 되었습니다.

더 자세한 차이를 알고자 한다면 [TPM 1.2와 2.0의 기능 비교](https://www.dell.com/support/kbdoc/ko-kr/000131631/tpm-1-2%EC%99%80-2-0%EC%9D%98-%EA%B8%B0%EB%8A%A5-%EB%B9%84%EA%B5%90)가 좋은 자료가 될 것 같습니다.


## TPM 기술의 이점

* TPM 기술을 이용할 시 장점
   * 암호화 키를 생성, 저장 및 사용을 제한합니다.
   * TPM의 고유한 RSA 키(자체에 구워짐)를 사용하여 플랫폼 장치 인증에 TPM 기술을 사용합니다.
   * 보안 측정값을 가져와서 저장하여 플랫폼 무결성을 보장합니다.


## TPM의 이용 예시

TPM은 또 소프트웨어 업데이트 보호, 가상머신 보호, 스마트카드 인증 등에 다양하게 사용되고 있습니다.

TPM 의 가장 대표적인 예시는 Window 의 BitLocker 입니다.

BitLocker란 Windows OS에 내장된 HDD, USB와 같은 저장 매체를 암호화하여 데이터를 보호하는 기술입니다. 

전체 디스크를 암호화하는 Full Disk Encrytion(FDE) 기술이라고도 합니다. 

특정한 폴더나 파일이 아니라 디바이스 전체나 파티션 전체를 암호화하는 것이 특징입니다.

이러한 BitLocker 에서는 이미 암호화 키를 보호하는 데 TPM 을 이용하고 있습니다.

[BitLocker 드라이브 암호화와 TPM 하드웨어 보안 기술](https://shinb.tistory.com/314)에서 자세하게 알아볼 수 있습니다.

이 밖에도 Credential Guard 및 Windows Hello for Business 등 에서도 이용되고 있으며 Windows의 보안 기능에서 널리 활용되고있다.

## 비고

TPM 의 개념을 알기 위해 참고한 사이트들

[마이크로소프트, 윈도우 10 디바이스에 하드웨어 기반 보안 계층 의무화](https://www.itworld.co.kr/news/100509)

[Windows 11で必須になった「TPM 2.0」って何？TPMの役割や確認方法を紹介](https://pc.watch.impress.co.jp/docs/topic/feature/1334277.html)

[Microsoft explains why you'll need a TPM for Windows 11](https://www.pcworld.com/article/3623013/why-windows-11-requires-a-tpm-for-your-pc.html#tk.rss_all)

[BitLocker란? 개념 정리](http://melonicedlatte.com/2020/06/16/113200.html)