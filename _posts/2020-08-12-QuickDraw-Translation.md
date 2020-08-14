---
title: "QuickDraw로 플레이 : 실시간 애플리케이션 - 번역"

categories:
  - QuickDraw
tags: 
  - QuickDraw
  - Error
  - Hanium
last_modified_at: 2020-08-12
---

퀵드로우란 구글이 개발한 온라인 게임의 하나로서, 플레이어가 사물이나 개념에 대한 그림을 그리면 인공신경망 인공지능을 사용하여 해당 낙서가 표현한 바를 추측하게 된다.

한이음에서 퀵드로우를 이용한 교육용 게임 컨텐츠 기능을 제작 중인데 한글로 바로 볼 수 있는 자료들이 많지 않아 제작하는데 어려움을 겪었다.

내가 도움을 받은 외국 자료는 1년 전 포스팅이라 현재로선 모듈 버전 오류도 있고, 

프로젝트 코드에도 주석이 달려있지 않아 이걸 기반으로 코드를 바꾼다는게 쉬운게 아니었다.

따라서 구글신의 도움을 받아 대충이나마 자료를 번역하고자 한다.

또한 다음 포스팅에서 참고한 프로젝트에서 어떤 부분을 고쳐야 하는지 설명하겠다.

## QuickDraw 문서

   * Step 1. [QuickDraw로 플레이 : 실시간 애플리케이션 - 번역](https://jee00609.github.io/quickdraw/QuickDraw-Translation/)
   * Step 2. [QuickDraw로 플레이 : 실시간 애플리케이션 - 코드 설명](https://jee00609.github.io/quickdraw/QuickDraw-import-error/)

## QuickDraw 란 무엇입니까?

Pictionary는 한 사람이 공중에있는 물체의 모양이나 그림을 그리고 다른 사람이 그것을 추측해야하는 게임입니다. Pictionary와 마찬가지로 Quickdraw는 카메라 앞에 패턴을 그리고 컴퓨터가 당신이 그린 것을 추측하게하는 게임입니다.

## QuickDraw 데이터베이스 정보

이 아이디어의 기원은 Google Research의 Magenta 팀에서 개발했습니다. 사실 "Quick, Draw!" 처음에는 2016 년 Google I / O에서 소개되었으며, 나중에 팀은 그리기 패턴을 예측하기 위해 CNN (Convolutional Neural Network) 기반 모델을 교육했습니다. 그들은이 게임을 온라인으로 만들었습니다. 모델 학습을위한 데이터 세트는 345 개 범주에 걸쳐 5 천만 개의 도면으로 구성됩니다. 이 5 천만 패턴은 그림 1과 같습니다. 이미지는 [여기](https://github.com/googlecreativelab/quickdraw-dataset) 에서 가져온 것 입니다.

<figure class="align-center">
  <img src="/assets/images/2020-08-12-QD.jpeg">
  <figcaption>그림 1 : 데이터베이스 이미지 샘플</figcaption>
</figure>

연구팀은 연구자들이 자체 CNN 모델을 훈련 할 수 있도록 데이터베이스를 공개적으로 사용할 수 있도록했습니다. 전체 데이터 세트는 4 가지 유형의 카테고리로 구분됩니다.

1. [원시 파일](https://console.cloud.google.com/storage/quickdraw_dataset/full/raw)

2. [단순화 된 도면 파일](https://console.cloud.google.com/storage/quickdraw_dataset/full/simplified)

3. [바이너리 파일](https://console.cloud.google.com/storage/quickdraw_dataset/full/binary)

4. [Numpy 비트 맵 파일](https://console.cloud.google.com/storage/quickdraw_dataset/full/numpy_bitmap)

일부 연구자들은이 데이터 세트를 사용하여 드로잉 패턴을 예측하기 위해 훈련 된 CNN 모델을 성공적으로 개발했습니다. [여기](https://github.com/googlecreativelab/quickdraw-dataset#get-the-data)에서 이러한 실험 및 자습서를 찾을 수 있습니다 . 그들은 또한 다른 연구자들을 돕기 위해 소스 코드를 온라인으로 만들었습니다.

## CNN을 사용한 실시간 QuickDraw 애플리케이션 개발

여기서는 전체 데이터베이스 이미지를 사용하는 대신 15 개의 주제를 사용하여 tensorflow 기반 QuickDraw 애플리케이션을 개발했습니다. [여기](https://console.cloud.google.com/storage/browser/quickdraw_dataset/full/numpy_bitmap) 에서 .npy 형식의 15 개 클래스 이미지를 다운로드 했습니다 . 이 15 개 클래스에는 Apple, Candle, Bowtie, Door, Envelope, Guitar, Ice Cream, Fish, Mountain, Moon, Toothbrush, Star, Tent, Wristwatch가 포함됩니다.

다운로드 한 데이터 세트는 'data'라는 폴더에 보관됩니다. CNN 모델은 이러한 이미지 샘플로 학습됩니다. 작은 데이터 세트의 경우 3 개의 컨볼 루션 레이어와 최대 풀링 및 드롭 아웃으로 CNN 모델을 학습했습니다. 네트워크를 평탄화 한 후 두 개의 조밀 한 레이어가 사용됩니다. 훈련 가능한 매개 변수의 수는 그림 2에 나와 있습니다.

<figure class="align-center">
  <img src="/assets/images/2020-08-12-QD2.png">
  <figcaption>그림 2 : QuickDraw 데이터 세트로 훈련하는 데 사용되는 CNN 모델 요약</figcaption>
</figure>

OpenCV 라이브러리에 지정된 기본 학습률로 훈련 네트워크 중에 Adam 최적화를 사용했습니다. 그러나 SGD (Stochastic Gradient Descent)도 사용했지만이 경우 기본 학습률 SGD에서는 낮은 학습 및 검증 정확도를 제공하므로 이러한 매개 변수를 수동으로 설정해야합니다. 우리는 50 epochs로 훈련했습니다. 6GB RAM CPU에서 CNN 모델을 학습하는 데 약 2 시간이 걸렸습니다. 모델의 정확도는 약 94 %였습니다. 실시간 테스트 결과는 아래 비디오에 나와 있습니다. Bandicam 소프트웨어는 데스크탑 활동을 기록하는 데 사용됩니다.

<iframe width="560" height="315" src="https://www.youtube.com/embed/CFTesizZZgo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

응용 프로그램은 파란색 포인터를 찾아 그 주위에 원을 만든 다음 원의 중심을 찾아 선이나 곡선을 그리고 손을 움직입니다. 파란색 포인터를 다른 색상으로도 바꿀 수 있습니다. 이를 위해 코드에 적절한 RGB 색상 조합을 제공해야합니다. 드로잉 패턴에 따라 모델은 예측 된 이모티콘을 추측하여 출력으로 표시합니다. 그러나 때로는 개체를 올바르게 분류하지 못했습니다. 분명한 이유는 실시간 애플리케이션이 비디오 스트림 수집에 사용되는 센서의 노이즈, 배경색 및 품질에 민감하기 때문입니다. 그러나 파란색 포인터를 웹캠에 충분히 가깝게 유지하면서 더 많은 Epoch로 훈련함으로써 시스템의 정확도를 향상시킬 수 있습니다.

이 애플리케이션의 소스 코드는 [GitHub 저장소](https://github.com/gautamkumarjaiswal/QucikDraw) 에서 사용할 수 있습니다 . 이를 다운로드하여 사용하여 자신의 CNN 모델을 학습시킬 수 있습니다. 필수 패키지의 설치 프로세스는 [GitHub 페이지](https://github.com/gautamkumarjaiswal/QucikDraw) 에서도 언급됩니다 .

이 프로젝트를 개발하는 데 도움을 준 Jayeeta Chakraborty에게 감사드립니다. 또한 훌륭한 튜토리얼과 코드 에 대해 [Akshay Bahadur](https://github.com/akshaybahadur21/QuickDraw) 에게 감사드립니다 . 그러나 시스템 성능을 향상시키기 위해 추가 컨볼 루션 및 드롭 아웃 레이어를 추가하여 CNN 아키텍처를 약간 개선했습니다. 이 기사와 코드가 다른 유사한 실시간 애플리케이션을 개발하는 데 도움이되기를 바랍니다.

## 원본 기사

[Play with QuickDraw: A Real-time Application](https://towardsdatascience.com/play-with-quickdraw-a-real-time-application-137e66ea9b60)
