---
title: "[JAVA] WAV 파일을 RAW Data 로 변환하기 (Wav to Raw) - Step 1"

categories:
  - Java
tags: 
  - Java
  - Audio
  - Error
last_modified_at: 2021-08-20
---

어쩌다 보니 Java 에서 Wav 파일을 Raw 데이터로 변환해야하는 기능을 만들어야 했다.

그러나 그 국내 및 외국 자료에도 참고할 자료가 없어서 직접 만들어야 겠다고 결심했다.

현재 리팩토링을 전혀 거치지 않은 날것의 코드를 만들었는데 아직 고쳐야 할 점이 있어 따로 문제점만 메모하고자 포스팅 한다.

현재 만든 Raw 파일은 이전 Python 에서 Raw Data 를 만지면서 고생했던 샘플링 주파수와 관련이 있는 것 같아 테스팅 했다.


## 샘플링 주파수 44100

<iframe width="560" height="315" src="https://www.youtube.com/embed/V1Oh2Sm4U18" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 샘플링 주파수 80000

<iframe width="560" height="315" src="https://www.youtube.com/embed/i8S83ewdPzI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

차이점이 확연히 보인다.

현재 Java 에서 이 Raw Data 를 읽으려고 하는 경우 샘플링 주파수 44100 을 기준으로 읽는 것 같아 제대로 사람의 목소리를 인지하지 못하는 것 같다.

이를 고치기 위해 어떻게 해야 할지 고민해 봐야 겠다.