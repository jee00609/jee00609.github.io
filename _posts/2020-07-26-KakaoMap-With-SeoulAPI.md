---
title: "공공데이터 자료들을 카카오톡 맵 마커로 찍기"

categories:
  - Android
tags: 
  - Android
  - Error
  - API 
  - Thread
  - Kakao
 
last_modified_at: 2020-07-26
---
서울 공공데이터에서 무료 와이파이 장소를 가져와 카카오 맵에 마커를 찍는 기능을 만들고 있다.

마커가 대략 2300개 이상 찍히면 에러가 생기는 것 같아 고쳐야 할 부분이 있는 것 같다.

## 어플리케이션 기능 구조

말로 설명하면 쉽지만 직접 만들어 보니 어려웠다.

만들면서 어려웠던 부분에 대해 따로 작성해야겠다 느껴서 적는다.

   1. 카카오 맵 API 를 사용해서 현재 좌표값을 찾고 '사용자' 위치를 마킹한다.
   2. 현재 내 위치의 주소를 찾는 함수를 호출한다.
   3. 주소 값의 지역구만 분리하여 공공데이터 검색 함수에 대입한다.
   4. 검색을 통해 와이파이 이름, 위도, 경도를 얻는다.
   5. 얻은 값을 통해 맵포인트를 찍는다.

## 중요 코드 - 나의 현위치 좌표값을 찾기

   ```ruby
// 단말의 현위치 좌표값을 통보받을 수 있다.

@Override
public void onCurrentLocationUpdate(MapView mapView, MapPoint currentLocation, float accuracyInMeters) {

    //내 위치 찾기
    MapPoint.GeoCoordinate mapPointGeo = currentLocation.getMapPointGeoCoord();

    //내 위치 주소 찾기
    //kakaoKey는 Native APP KEY를 의미한다
    mReverseGeoCoder = new MapReverseGeoCoder(kakaoKey, mMapView.getMapCenterPoint(), MainActivity.this, MainActivity.this);

    //Reverse Geo-coding(Asynchronous) 서비스를 요청한다.
    // 주소 정보를 요청하는 함수다.
    mReverseGeoCoder.startFindingAddress();

}
   ```

## 중요 코드 - 내 위치 좌표값의 주소를 찾기

   ```ruby
// 주소를 찾은 경우 호출되는 함수

@Override
public void onReverseGeoCoderFoundAddress(MapReverseGeoCoder mapReverseGeoCoder, String s) {
    mapReverseGeoCoder.toString();

    String[] split = s.split(" ");
    final String myLocation = split[1]; // 내 위치 지역 (ex 강남구,고양시, 중구 같은 것)을 저장

    // 공공데이터 자료 검색 및 마커 찍을 함수에 현재 내 지역 s 를 인수로 보낸다.
    onFinishReverseGeoCoding(s);
}
   ```

## 중요 코드 - 주소 지역의 와이파이 자료들만 수집

   ```ruby
// onFinishReverseGeoCoding 내의 익명 스레드 에서 실행
// 주소 지역의 와이파이만 가져와서 반복 작업의 과부하 줄임

//검색 시작!
runOnUiThread(new Runnable() {

    @Override
    public void run() {

        final String save_data = data.toString();
        String[] split = split = save_data.split("\n");

        for(int i=0;i<split.length;i++){
            String[] splitresult = split[i].split("\\*");

            MapPOIItem wifiItem = new MapPOIItem();
            wifiItem.setTag(i);
            MapPoint mapPoint = MapPoint.mapPointWithGeoCoord(Float.parseFloat(splitresult[2]), Float.parseFloat(splitresult[1]));
            wifiItem.setItemName(splitresult[0]);
            wifiItem.setMapPoint(mapPoint);
            wifiItem.setMarkerType(MapPOIItem.MarkerType.BluePin);
            wifiItem.setSelectedMarkerType(MapPOIItem.MarkerType.RedPin);
            mMapView.addPOIItem(wifiItem);

        }

    }
});
   ```

## 이미지

<figure class="align-center">
  <img src="/assets/images/2020-07-26-success.jpg" witdth ="150" height = "100"/>
  <figcaption>성공!</figcaption>
</figure>


## 현재 문제점

<span style="color:gray"> 카카오 본사는 제주도에 있다고 한다. </span>

<span style="color:gray"> 그런데 대체 왜 카카오맵의 첫 시작이 중구인 것 일까? </span>

카카오맵을 시작하면 중구를 맨 처음 출력한 후 나의 위치를 찾는다.

그러다 보니 현재 나의 위치 주소값의 지역이 아닌 중구의 와이파이 자료들 또한 같이 검색 된다.

대략 2300개 이상의 마커를 찍히는데, 이는 맵에 과부하를 일으켜 프로젝트가 비정상 종료 한다.

현재 나의 위치와 맞지 않은 주소들의 마커를 지우려면 어떡해야 할까?

## 참고 사이트

[참고 사이트 - Kakao Maps API Docs](https://apis.map.kakao.com/android/documentation/)