---
title: "카카오 지도 API 에러 해결"
categories:
  - Android
tags:
  - Android
last_modified_at: 2020-05-21
---

카카오 지도 API 사용해서 지도에 자신의 위치를 나타내는 기능을 구현하고 있다.
그런데 분명히 상속되야할 클래스들이 상속되지 않는 문제가 생겼다.

대체 왜 이럴까 싶어서 찾아봤다. 그리고 카카오 가이드만을 따라하면 안된다는 것을 깨달았다.

참고 - https://m.blog.naver.com/jogilsang/221393218449
참고 사이트에 의하면 gradle 파일에 dependency 에 문구를 추가해줘야한다고 한다.

compile files('libs/libDaumMapAndroid.jar')
사이트에서는 위의 것으로 써있지만 
 
implementation files('libs\\libDaumMapAndroid.jar')
버전 및 경로 문제로 인해 나에게 맞게 고쳐서 바꿨다.


