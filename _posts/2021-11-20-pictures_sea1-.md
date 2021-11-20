---
title: "졸업 작품 - Pictures, Sea"

categories:
  - Java
tags: 
  - Java
  - AWS
  - API
  - ETRI
last_modified_at: 2021-11-20
---

저번 주에 졸업 작품을 제출했고, 이번 주 수요일에 최종적으로 통과 연락을 받았다!

이전 작품의 단점을 고쳐서 꼭 다시 만들어 보고 싶었는데, 결국엔 원했던 기능을 만들어 볼 수 있어서 기뻤다.

이번 포스팅에선 프로젝트의 소개를 하고 나중에 프로젝트 구현에서 어려웠던 점을 작성하고자 한다.

## 목차

* [이전 작품의 문제점](#이전-작품의-문제점)
* [프로젝트 개요](#프로젝트-개요)
* [상세 기능 구현 사항](#상세-기능-구현-사항)
* [UML](#UML)
* [개발 기록](#개발-기록)
* [동영상](#동영상)
* [비고](#비고)

## 이전 작품의 문제점

Python TK GUI 인터페이스로, ETRI API 만을 이용하여 완성했었던 과거의 프로젝트에는 문제가 존재했었다.

   * 고정적인 인터페이스 크기
   * 생각보다 적은 이미지 인식 지원 객체 카테고리
   * 해당 객체가 지칭하는 것이 알 수 없는 한국어 정의 미지원

여기서 제일 문제가 됬던 점은 지원하는 객체 카테고리가 총 80개였단 점이었다.

<figure style="width: 300px" class="align-center">
  <a href="/assets/jjal/jokeBear_computer.jpg"><img src="/assets/jjal/jokeBear_computer.jpg"></a>
  <figcaption>더 좋은 방법이 없을까 고민했다.</figcaption>
</figure>

그러다가 AWS Rekognition 을 사용해서 이미지를 분석해보자는 아이디어가 떠올랐다.

<figure class="align-center">
  <a href="/assets/images/2021-11-20-rekognition.PNG"><img src="/assets/images/2021-11-20-rekognition.PNG"></a>
  <figcaption>수천개의 레이블을 지원하는 AWS Rekogntion으로 기능을 업그레이드해보자고 생각했다.</figcaption>
</figure>

또한 Python 이 아닌 Java Spring Framework 환경에서 구현하였다.

덕분에 웹사이트 형식을 통한 Dynamic 한 사이즈를 지원하는 UI 와 더 다양하게 객체를 탐지할 수 있는 기능 등 다양한 업데이트를 진행할 수 있었다.

이제 이 아래로 프로젝트에 대한 간단한 설명을 할 것이다.

## 프로젝트 개요

![Main Page](https://user-images.githubusercontent.com/31675804/141615048-78f8ccf2-0bf2-4a57-88b4-f089a161c526.PNG)

AWS Rekognition 과 ETRI Open API 를 통해 사용자의 이미지를 분석하여 추출한 오브젝트 단어에 대하여, **단어에 대한 정의와 사용자의 발음을 평가** 해주는 프로그램


## 상세 기능 구현 사항

* 선택한 이미지 S3 에 업로드 후 Rekognition Object 추출
* 추출한 Object 에 대해 화면에 동적으로 카드 출력
* 출력된 카드들 중에 원하는 카드 클릭 시 상세 카드(Rating) 가 아래에 출력
* 녹음 및 녹음 저장
* 녹음한 Audio 파일 업로드
* 상세카드의 Rating 버튼 클릭 시 업로드한 Audio 파일과 Object 카드를 비교하여 발음 평가
* Object 와 Object 에 대한 한국어 정의, 발음 평가 점수 등을 새 탭에서 열리는 페이지에서 출력
* 프로젝트를 소개하는 Introduce 페이지


## UML

(클릭 시 원본 그림 보기 가능)

* Class Diagram

<figure class="align-center">
  <a href="https://raw.githubusercontent.com/jee00609/Pictures_Sea/master/src/main/resources/static/uml/Class%20Diagram.png"><img src="https://raw.githubusercontent.com/jee00609/Pictures_Sea/master/src/main/resources/static/uml/Class%20Diagram.png"></a>
  <figcaption>Class Diagram</figcaption>
</figure>

* Floaw Chart

<figure style="width: 500px" class="align-centert">
  <a href="https://raw.githubusercontent.com/jee00609/Pictures_Sea/master/src/main/resources/static/uml/Flow%20Chart.png"><img src="https://raw.githubusercontent.com/jee00609/Pictures_Sea/master/src/main/resources/static/uml/Flow%20Chart.png"></a>
  <figcaption>간단한 Flow Chart</figcaption>
</figure>



## 개발 기록

* [Spring Framework 환경 에서의 AWS-S3 업로드 테스팅 프로젝트](https://github.com/jee00609/aws-s3Uplaod-Upgrade-Demo)
* [Spring Framework 환경 에서의 AWS-Rekognition 테스팅 프로젝트](https://github.com/jee00609/aws-rekognition-Demo)

## 동영상

짧은 설명

<iframe width="560" height="315" src="https://www.youtube.com/embed/8zzVUW735Cs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

상세 설명

<iframe width="560" height="315" src="https://www.youtube.com/embed/zSkj0KpMWxw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 비고

[프로젝트 전문](https://github.com/jee00609/Pictures_Sea)