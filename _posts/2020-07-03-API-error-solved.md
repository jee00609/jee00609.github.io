---
title: "안드로이드 공공데이터 API 검색 불가 에러 해결"

categories:
  - Android
tags: 
  - Android
  - Error
  - API 
last_modified_at: 2020-07-03
---

코드 짜면서 멍청해진다고 느낄 때가 있는데 저번 이틀이 그랬던 것 같다.

현재 카카오 맵과 서울 와이파이 검색 프로젝트를 병합하기 위해 노력하고 있다.

그러던 와중에 늘 테스트로 검색하던 강남구가 아닌 중구를 검색했던 것이 이번 일의 시작이었다.

정상적으로 검색이 되던 어플리케이션에서 에러를 발견한 것이다.

<figure class="align-center">
  <img src="/assets/images/2020-07-03-view.jpg">
  <figcaption>출력이 잘 나오는 강남구 와 출력이 되지 않는 중구</figcaption>
</figure>


대체 왜 이런 일이 발생했는지 알아보았다.

## 에러가 발생한 프로젝트의 알고리즘

<span style="color:blue"> 사용자 : 파랑 </span>

<span style="color:green"> 어플리케이션 : 초록 </span>

   1. <span style="color:blue"> 원하는 지역을 검색한다. </span>
   2. <span style="color:green"> 입력받은 지역에 와이파이가 존재하는 지 검색 </span>
      1. <span style="color:green"> 존재하면 3으로 넘어간다. </span>
      2. <span style="color:green"> 존재하지 않으면 빈 텍스트뷰를 출력한다. </span>
   3. <span style="color:green"> 입력받은 지역의 와이파이 총 개수를 검색한다. </span>
   4. <span style="color:green"> 입력받은 지역의 와이파이 개수를 END_INDEX로 지정한 URL 로 검색을 한다.  </span>
   5. <span style="color:green"> URL 을 통해 받아온 값들을 텍스트 뷰에 출력한다. </span>

## 서울시 공공와이파이 위치정보 샘플 URL

| 샘플 URL                             | 설명                                                           |
| ----------------------------------- | ------------------------------------------------------- |
| 서울시 공공WiFi 위치정보 조회 | http://openAPI.seoul.go.kr:8088/(인증키)/xml/PublicWiFiPlaceInfo/1/5/  |
| 종로구 공공WiFi 위치정보 조회 | http://openAPI.seoul.go.kr:8088/(인증키)/xml/PublicWiFiPlaceInfo/1/5/종로구  |

지역에 있는 와이파이를 알고자 한다면 위 샘플 URL 에서 보이듯 3가지를 알고 있어야 한다.

   * START_INDEX (데이터 행 시작번호)
   * END_INDEX 정수 입력 (데이터 행 끝번호)
   * GU_NM (구명 문자열)

검색 URL 이 잘못된 것일까하고 로그를 찍게 했다.

## 정상작동 하는 강남구 요청 URL

   ```ruby
http://openapi.seoul.go.kr:8088/key값/xml/PublicWiFiPlaceInfo/1/1/강남
http://openapi.seoul.go.kr:8088/key값/xml/PublicWiFiPlaceInfo/1/895/강남
   ```

## 에러가 발생한 중구 요청 URL

   ```ruby
http://openapi.seoul.go.kr:8088/key값/xml/PublicWiFiPlaceInfo/1/1/중구
http://openapi.seoul.go.kr:8088/key값/xml/PublicWiFiPlaceInfo/1/1248/중구
   ```

처음 봤을 땐 아무런 문제가 없다고 생각했다.

그래서 직접 인터넷을 통해 URL 을 입력해보았다.

<figure class="align-center">
  <img src="/assets/images/2020-07-03-api-error.PNG">
  <figcaption>데이터요청은 한번에 최대 1000건을 넘을 수 없습니다.</figcaption>
</figure>

<figure class="align-center">
  <img src="/assets/images/2020-07-03-api-explain.PNG">
  <figcaption>ERROR-336 을 자세히 보자.</figcaption>
</figure>

설계된 알고리즘 자체가 잘못됬음을 느꼈다.

애초에 Open API 설명만 잘 읽었어도 설계 상에서 고칠 수 있던 문제였던 것이다.

서울의 한 지역에 와이파이 개수가 1000개가 넘어갈 것이라고 생각하지도 않았던 지방 촌뜨기의 실수였다.

## 에러가 발생한 프로젝트의 알고리즘

<span style="color:blue"> 사용자 : 파랑 </span>

<span style="color:green"> 어플리케이션 : 초록 </span>

<span style="color:red"> 수정 : 빨강 </span>

   1. <span style="color:blue"> 원하는 지역을 검색한다. </span>
   2. <span style="color:green"> 입력받은 지역에 와이파이가 존재하는 지 검색 </span>
      1. <span style="color:green"> 존재하면 3으로 넘어간다. </span>
      2. <span style="color:green"> 존재하지 않으면 빈 텍스트뷰를 출력한다. </span>
   3. <span style="color:green"> 입력받은 지역의 와이파이 총 개수를 검색한다. </span>
      1. <span style="color:red">총 개수가 1000개를 넘어가지 않으면 총 개수를 END_INDEX로 지정한 URL 로 검색을 한다. </span>
      2. <span style="color:red"> 총 개수가 1000개를 넘어가면 limit 이란 변수가 총 개수보다 커질 때까지 1000개씩 검색을 돌린다. </span>
   5. <span style="color:green"> URL 을 통해 받아온 값들을 텍스트 뷰에 출력한다. </span>

## 에러 해결

<figure style="width: 300px" class="align-center">
  <img src="/assets/images/2020-07-03-success.PNG">
  <figcaption>잘 나오는 것을 확인 가능</figcaption>
</figure>

## 깨달은 점

   * 개발 전에 사용할 기능의 문서를 꼭! 확인하자
   * 어떤 부분이 잘못되었는지 확인을 위해 로그를 수시로 찍자

프로젝트 전문은 아래 사이트로 볼 수 있다.

[사용했던 서울시 공공 와이파이 위치정보](http://data.seoul.go.kr/dataList/OA-1218/S/1/datasetView.do)

[업데이트 한 프로젝트](https://github.com/jee00609/Seoul_Wifi_Search)