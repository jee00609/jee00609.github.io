---
title: "나의 컴퓨터 PC 에서 Windows 11 업그레이드 호환성 체크하기"

categories:
  - IT News
tags: 
  - TPM
  - Window 11

last_modified_at: 2021-06-26
---

윈도우 11 이 출시되었고 본인은 윈도우 11 과 관련해서 업그레이드가 가능한지 알아보았다.

그러나 어떻게 된일인지 윈도우 11 과 호환성이 없다는 결과를 통보받아 이를 어떻게 해결해야 하는지를 기록해보고자 한다.

## Windows 11 의 최소 요구사항

Windows 11의 최소 요구 사항은 1GHz 이상으로 2 개 이상의 코어의 64bit CPU, 메모리 4GB 스토리지 64GB 이상, DirectX 12 호환 GPU 9 인치 / 720p 이상의 디스플레이와 인터넷 연결이 되어야만 합니다.

또한 TPM (신뢰할 수있는 플랫폼 모듈) 2.0에 대한 지원도 필요합니다.

TPM 2.0 칩을 탑재하지 않은 PC도 있지만, CPU의 펌웨어로 내장 되어있습니다.

Intel이라면 Haswell 세대 및 Clover Trail 이후의 세대에는 내장되어 있습니다.

AMD라면 Mullins / Beema / Carrizo 세대에 구현되어 있습니다.


## 내 PC 에서는 Windows 11 (윈도우 11) 과 호환되는가?

먼저 자신의 PC 에서 Windows 11 이 호환되는지 알고 싶을 것입니다.

[Windows 11 호환성 검사 프로그램](https://aka.ms/GetPCHealthCheckApp) 를 다운받아 자신의 PC 를 검사할 수 있습니다.

<figure class="align-center">
  <a href="/assets/images/2021-06-26-PC-HEALTH.PNG"><img src="/assets/images/2021-06-26-PC-HEALTH.PNG"></a>
  <figcaption>이 PC 에서는 Windows 11 을 실행할 수 없습니다.</figcaption>
</figure>

저의 PC 에서는 Windows 11 과 호환이 되지 않는다는 창만 뜨는군요.

해결방법을 알고자 해도 이 도구는 왜 호환이 안되는지 제대로 알려주지 않습니다.

<figure class="align-center">
  <a href="/assets/images/2021-06-26-window11-error.PNG"><img src="/assets/images/2021-06-26-window11-error.PNG"></a>
  <figcaption>이유 정도는 정확히 알려줘...</figcaption>
</figure>

## 자신의 TPM 2.0 인지 확인하기

<figure class="align-center">
  <a href="/assets/images/2021-06-26-window11-error2.PNG"><img src="/assets/images/2021-06-26-window11-error2.PNG"></a>
  <figcaption>TPM 확인하기</figcaption>
</figure>

현재 자신의 PC가 위 두 기능을 지원하는지 확인하려면 우선 작업표시줄 검색창에 ‘장치 보안’이라고 입력한 뒤 해당 항목을 확인합시다.

여기서 보안 프로세서(TPM) 버전과 보안 부팅 기능이 있는지 확인하면 됩니다. 

이를 지원한다면 해당 항목이 표시되면서 ‘장치가 표준 하드웨어 보안 요구사항을 충족합니다’라는 메시지가 표시되고, 지원하지 않는다면 이 창에서 아무런 표시가 없으며 ‘표준 하드웨어 보안이 지원되지 않습니다’라는 메시지가 표시됩니다.

본인은 1.16 이라 2.0 이 아니어서 호환이 안되는 듯 싶습니다.


## "이 PC에서 Windows 11를 실행할 수 없습니다" 해결 방법

호환이 안되는 이유는 명확하게 나타나지 않기 때문에 가장 유력한 이유인 TPM2.0 과 관련하여 해결방법을 작성합니다.

물론 CPU, 스토리지 등의 요구 사항을 충족하지 않은 경우도 있지만, 메인 보드의 펌웨어 fTPM가 활성화되어 있지 않을 가능성이 높기 때문입니다.

"이 PC에서 Windows 11를 실행할 수 없습니다"라고 표시된 경우

   *  **Intel**
      * UEFI (BIOS)에서 「Intel Platform Trust Technology」(Intel PTT)를 활성화 (Enabled) 함으로써 호환성을 확보 할 수 있습니다.
   *  **AMD**
      * UEFI (BIOS)에서 fTPM (Firmware TPM)을 활성화 (Enabled) 함으로써 호환성을 확보 할 수 있습니다.

## 비고

[Windows 11で必須になった「TPM 2.0」って何？TPMの役割や確認方法を紹介](https://pc.watch.impress.co.jp/docs/topic/feature/1334277.html)

[윈도우 11 무료 업그레이드하려면 TPM 2.0과 보안 부팅 기능 필수](https://www.boannews.com/media/view.asp?idx=98604)