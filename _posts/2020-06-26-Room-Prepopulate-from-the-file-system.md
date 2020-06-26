---
title: "안드로이드 Room 데이터베이스에 assets 폴더 속 db 파일 삽입하기"

categories:
  - Android
tags: 
  - Android
  - Room
  - Database
last_modified_at: 2020-06-26
---

서울 앱 공모전을 준비하면서 핸드폰 내장 데이터베이스를 이용해야 할 필요성을 느꼈다.

원래라면 가장 익숙하게 사용하던 PHP MySQL 을 이용할 것이었다.

그러나 매우 많은 숫자의 와이파이 주소지의 위,경도 값을 내가 움직이고 있는 위치와 계속해서 비교하며 값을 가져와야 하는 기능에서 PHP MySQL을 이용하기에는 무리가 있다고 생각했다.

따라서 핸드폰의 내장 데이터베이스 즉 SQLite 를 사용해보자고 결심했다.

그러다가 안드로이드 디벨로퍼에서 Room 지속성 라이브러리에 대해서 알게 되었다.

[참고하면 좋은 사이트 - Room 지속성 라이브러리](https://developer.android.com/topic/libraries/architecture/room?hl=ko)

> ###### 주의: 이러한 API는 강력하기는 하지만 상당히 낮은 수준이므로 다음과 같이 사용하는 데 상당한 시간과 노력이 필요합니다. 원시 SQL 쿼리에 관한 컴파일 타임 확인이 없습니다. 따라서 데이터 그래프가 변경됨에 따라 영향을 받는 SQL 쿼리를 수동으로 업데이트해야 합니다. 이 과정은 시간이 오래 걸리고 오류가 쉽게 발생할 수 있습니다. SQL 쿼리와 데이터 개체 간에 변환하려면 많은 상용구 코드를 사용해야 합니다. 이러한 이유로 앱의 SQLite 데이터베이스에 있는 정보에 액세스하기 위한 추상화 레이어로 Room 지속성 라이브러리를 사용하는 것이 좋습니다.
{: .small}

<cite>SQLite를 사용하여 데이터 저장</cite> --- 안드로이드 스튜디오 디벨로퍼
{: .small}

SQLite 를 검색하자마자 위의 주의사항이 뜬다. 한마디로 이제 Room 지속성 라이브러리가 안들이드 데이터베이스의 대세가 된단 것이다.

하지만 나온지 꽤 된 것 같은데도 'Prepopulate your Room database' 와 같은 기능은 (내 머리에) 이해하기 쉬운 문서를 찾지 못해서 드래곤볼 모으듯이 필요한 사이트를 찾기로 했다.

## Prepopulate from the file system

   ```ruby
   Room.databaseBuilder(appContext, AppDatabase.class, "Sample.db")
    .createFromFile(new File("mypath"))
    .build();
   ```

열심히 공부를 하지 않았던 과거의 업보로 문서를 제대로 이해하지 못해 직접 어디에 사용해야 하는지 알아보았다,

[참고하면 좋은 사이트 - Room database 사용해보기](https://velog.io/@ptm0304/Android-Room-database-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0)

여기서 보면 @Database 로 정의되는 클래스에 넣으면 되는 듯 하다.

따라서 

   ```ruby
   public static AppDatabase getInstance(Context context) {
        synchronized (sLock) {
            if(INSTANCE==null) {
                INSTANCE= Room.databaseBuilder(context.getApplicationContext(),
                        AppDatabase.class, "Wifi.db")
                        .createFromAsset("databases/SeoulWifiDB.db")
                        .build();
            }
            return INSTANCE;
        }
    }
   ```

이렇게 먼저 자체 제작을 했다.

빌드나 sync 에서 문제가 발생하지 않았기에 내일이나 일요일 안에는 제대로 들어갔는지 확인할 수 있도록 레이아웃을 설계할 생각이다.


 

