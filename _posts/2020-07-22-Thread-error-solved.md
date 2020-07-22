---
title: "안드로이드 카카오톡 지도에서 공공데이터 검색 에러 해결"

categories:
  - Android
tags: 
  - Android
  - Error
  - API 
  - Thread
last_modified_at: 2020-07-22
---

카카오톡과 서울 와이파이 API 를 병합하는 과정에 발생한 오류를 고쳤다.

[서울이 아닌 지역에서 검색 시 오류 발생](https://jee00609.github.io/android/Thread-error-not-solved/)

## 해결법

   ```ruby
// String getXmlData_num() 라는 검색한 지역의 
// 와이파이 총 개수를 구하는 함수에 코드를 삽입했다. 

if(buffer_num.length() == 0){
    buffer_num.delete(0,buffer_num.length());
    buffer_num.append("0");
    buffer_num.append("\n");
}
   ```

여기서 buffr_num 은 공공데이터를 파싱하면서 얻은 개수를 의미한다.

원래는 buffer_num 에 대해 NULL값인지 확인해서 NULL 값이면 0을 보내도록 만들고자 했다.

그러나 리턴값은 NULL 값이 아니었고, 그렇다고 출력했을 때 나오는 값이 없었다.

따라서 buffer_num 의 길이를 파악하는 length 를 사용했다.

buffer_num.length 가 0인 경우, 직접 문자열 0의 값을 리턴하는 방향으로 고쳤다. 

## 코드 보완

   ```ruby
// public void mOnClick 의 스레드 생성 후 
// run() 내부에서 검색결과 0일때 종료하도록 보완

if(location_num == 0){
    return;
}
   ```

이 파트는 이전 프로젝트의 출력물과 차이점이 크진 않다.

카카오 맵 API 와 연결했을 시, runOnUIThread 를 돌리는 불필요한 상황을 방지하기 위해 추가로 보완했다.

## 비고

[프로젝트 전문](https://github.com/jee00609/Seoul_Wifi_Search)