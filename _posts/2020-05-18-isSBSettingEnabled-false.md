---
title: "공공 API 이용한 검색 기능과 파싱 문제 해결 (HTTPLog)-Static: isSBSettingEnabled false"
categories:
  - Android
tags:
  - Android
  - HTTP
last_modified_at: 2020-05-18
---

서울에 있는 무료 와이파이 좌표 API를 이용해 자신의 지역을 검색하면 값을 파싱해오는 기능을 구현해보았다.
분명 갤럭시 나의 S7에서 잘 작동하던 것이 다른 사람의 S10 에서 작동하지 않아 고민했다.

깃허브에 올려놓은 코드를 다시 천천히 읽었더니 메인 액티비티내의 함수 하나가 아예 빠져 있었다는 것을 깨달았다.
그래서 메인 액티비티에 빠져있던 함수를 다시 넣고 돌렸더니 위의 2가지 에러로그를 띄울 수 있었다.

   ```ruby
no network security config specified using platform default android

(HTTPLog)-Static: isSBSettingEnabled false
   ```

지역마다 다른 와이파이의 개수를 동적으로 갖고 오기 위해 만들었던 두가지의 함수들 중 첫번째 함수에서 오류가 났다는 것을 알게되었다. 


검색해보니 [변방의 프로그래머](https://developside.tistory.com/85)님 의 글을 통해 해결할 수 있었다.

나는 AndroidManifest.xml 파일에 

   ```ruby
android:usesCleartextTraffic="true" 
   ```

를 삽입했더니 기능이 제대로 실행됬다.

코드를 제대로 올리지 못했던 문제점과 코드 한줄로 며칠 고민했다는것이 민망해진다.



