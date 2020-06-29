---
title: "안드로이드 Room 실습 1단계 error: Entities and POJOs must have a usable public constructor. "

categories:
  - Android
tags: 
  - Android
  - Room
  - Database
  - Error
last_modified_at: 2020-06-29
---

26일부터 Room 지속성 DB 를 이용하기 위해 온갖 자료를 섭렵했다.

그러나 asset 폴더 databases 안의 db 파일을 아직도 읽지 못하는 문제에 직면했다.

db 파일을 읽을 때 인코딩오류로 인해 읽지 못하는 것인지, MainActivity 의 논리적 오류인지 확인해보기 위해 간단한 모듈 프로젝트를 만들어 보기로 했다.

분명히 간단하게 만들어 보기 위해 노력했는데 간단히 끝나지 않았다...

유튜브 Room 강의 중 오준석 선생님의 강의가 있는데 java, kotlin 모두 있고, 댓글로 질문을 달았는데 매우 친절히 답변해주셔서 정말 감사했다.

[참고하면 좋은 사이트 - Room 데이터베이스 예제-글](https://youngest-programming.tistory.com/113)

[참고하면 좋은 사이트 - Room 데이터베이스 예제-유튜브](https://www.youtube.com/watch?v=pG6OkJ3rSjg)

대부분의 코드는 위의 막내 프로그래밍 막내와 비슷하다.

많은 자료들에서 Entity 의 Primary 키를 @PrimaryKey(autoGenerate = true) 하는 경우가 많다.

이번 프로젝트에선 향후에 넣을 WifiDB의 PrimaryKey 에 적용하기 쉽도록 ContentID 라는 변수를 만들어 구현하였다.

## Error 발생 Entity.java

   ```ruby
@Entity
public class Wifi {

    @NonNull
    @PrimaryKey
    private String ContentID;

    private float Xcors;
    private float Ycors;

    public Wifi(@NonNull String ContentID, float xcors, float ycors) {
        this.ContentID = ContentID;
        this.Xcors = xcors;
        this.Ycors = ycors;
    }

    @NonNull
    public String getContentID() {
        return ContentID;
    }

    public void setContentID(@NonNull String contentID) {
        this.ContentID = contentID;
    }

    public float getXcors() {
        return Xcors;
    }

    public void setXcors(float xcors) {
        this.Xcors = xcors;
    }

    public float getYcors() {
        return Ycors;
    }

    public void setYcors(float ycors) {
        this.Ycors = ycors;
    }

    @Override
    public String toString() {
        return "Wifi{" +
                "ContentID='" + this.ContentID + '\'' +
                ", Xcors=" + this.Xcors +
                ", Ycors=" + this.Ycors +
                '}';
    }
}
   ```

이 코드는 AndroidStudio 의 Generate 기능을 이용해서 만든 코드로 빨간 줄도 쳐지지 않는 문제 없는 코드로 보일 것이다.

그러나 이 코드는 Build 에서부터 막히는 에러를 발생시킨다.

<figure class="align-center">
  <img src="/assets/images/2020-06-29-error.PNG">
  <figcaption>error: Entities and POJOs must have a usable public constructor.</figcaption>
</figure>

너무 길어서 제대로 보이지 않기에 원문을 올린다.

## Error

   ```ruby
D:\workspace\Andriod_Workspace\roomtest2\app\src\main\java\com\example\roomtest2\Wifi.java:8: error: Entities and POJOs must have a usable public constructor. You can have an empty constructor or a constructor whose parameters match the fields (by name and type).
public class Wifi {
       ^
  Tried the following constructors but they failed to match:
   ```

분명 Getter, Setter 그리고 Constructor 까지 안드로이드에서 자동으로 만들어 주는 기능을 사용했는데 빌드도 못하는 상황이 발생한다.

나와 비슷한 문제를 겪은 이름도 모를 친구에게서 해결법을 유추해 낼 수 있었다.

[참고하면 좋은 사이트 - Room Persistence](https://stackoverflow.com/questions/53874559/room-persistence-entities-and-pojos-must-have-a-usable-public-constructor)

## Correct Entity.java

   ```ruby
@Entity
public class Wifi {

    @NonNull
    @PrimaryKey
    private String ContentID;

    private float Xcors;
    private float Ycors;

    public Wifi(@NonNull String ContentID, float Xcors, float Ycors) {
        this.ContentID = ContentID;
        this.Xcors = Xcors;
        this.Ycors = Ycors;
    }

    @NonNull
    public String getContentID() {
        return ContentID;
    }

    public void setContentID(@NonNull String ContentID) {
        this.ContentID = ContentID;
    }

    public float getXcors() {
        return Xcors;
    }

    public void setXcors(float Xcors) {
        this.Xcors = Xcors;
    }

    public float getYcors() {
        return Ycors;
    }

    public void setYcors(float Ycors) {
        this.Ycors = Ycors;
    }

    @Override
    public String toString() {
        return "Wifi{" +
                "ContentID='" + this.ContentID + '\'' +
                ", Xcors=" + this.Xcors +
                ", Ycors=" + this.Ycors +
                '}';
    }
}
   ```

어디서 틀렸는지 눈치 챘는가?

<span style="color:red"> Entity 에서 사용하는 변수의 이름과 매개변수가 동일하지 않기에 발생한 오류다. </span>

아주 쉽게 바꿀 수 있는 문제지만 눈치채기 매우 어려운 문제였다. 

Android Studio 의 Generate 기능으로 자동적으로 구현해주는 함수에서 오류가 날 것이라고 생각하지도 못했다.

프로젝트 전문은 아래 사이트로 볼 수 있다.

[참고하면 좋은 사이트 - Fix Error Room DB](https://github.com/jee00609/Room_DB_Example)