---
title: "안드로이드 카카오톡 지도에서 공공데이터 검색 에러  StringIndexOutOfBoundsException: String index out of range"

categories:
  - Android
tags: 
  - Android
  - Error
  - API 
  - Thread
last_modified_at: 2020-07-13
---

카카오톡과 서울 와이파이 API 를 병합하는 과정에 발생한 오류다.

에러의 원인이 웃기면서 슬프다.

## 에러가 발생한 스레드

해당 프로젝트가 실행되고 나서 몇분 후면 강제로 종료된다.

   ```ruby
// 쓰레드를 생성하여 돌리는 구간
new Thread(new Runnable() {

    @Override
    public void run() {

        //
        String key = "key값";
        String data;
        XmlPullParser xpp;

        //
        String num; // 그 지역에 와이파이가 몇개 있는지 가져오는 변수
        //2020-06-30
        int location_num;   //검색해야할 총 개수 1000개가 넘으면 api 한번 가져오는 양을 넘어서 뻑간다.
        final int api_limit = 1000;

        //2020-07-13
        //이제부터 사용자가 입력한 글자가 아닌 자동적으로 지역 이름을 가져가야 한다.

        num = getXmlData_num(myLocation); // 검색한 지역에 와이파이의 총 개수를 가져오는 함수

        System.out.println("num:"+num);

        //2020-06-30
        //오늘에서야 api 1000건을 넘기면 가져 오지 않는 걸 알게 된 민지는 슬픈 것이어요...
        //해결해보자

        //ParsesInt 만 해선 쓰레드에서 에러난다.
        // 문자열 뒤에 \n 같이 온전한 정수형이 들어가지 않기 때문이다.
        //해결법 substring으로 나눠서 \n 을 뺀다.
        //https://m.blog.naver.com/PostView.nhn?blogId=sseyoung513&logNo=221079088209&proxyReferer=https:%2F%2Fwww.google.com%2F

        location_num = Integer.parseInt(num.substring(0, num.length()-1));
        System.out.println("num.length : "+ num.length());
        System.out.println("location_num : "+location_num);

        if(location_num < api_limit){ //1000개 이하일 때
            System.out.println("while no");
            String start_num_String = "1";
            data= getXmlData(start_num_String,num,myLocation); // 하단의 getData 메소드를 통해 데이터를 파싱

            //검색 시작!
            runOnUiThread(new Runnable() {

                @Override
                public void run() {
                    //text.setText(data);
                }
            });

        }
        else{ //1000개 이상일 때
            int index_num= 1000;
            int start_num = 1;  //url에서 api 검색 시작 주소를 나타낸다.
            String start_num_string;
            int last_num = 1000;   //url에서 api 마지막 검색 주소를 나타낼 수 도 있다...?
            String last_num_String;  //url에서 api 검색 시작 주소를 나타낸다.

            final StringBuffer input_data = new StringBuffer();

            do{
                start_num_string = String.valueOf(start_num);
                last_num_String = String.valueOf(last_num);

                data = getXmlData(start_num_string,last_num_String,myLocation);
                input_data.append(data);
                System.out.println("while data + "+data);


                start_num+=1000;
                last_num+=1000;
                index_num+=1000;

            }while(index_num<location_num);

            //검색 시작!
            runOnUiThread(new Runnable() {

                @Override
                public void run() {
                    //text.setText(input_data);
                }
            });

        }

        //data= getXmlData(num); // 하단의 getData 메소드를 통해 데이터를 파싱


        System.out.println("data"+data);

    }

}).start();
   ```

익명 클래스를 이용한 스레드 부분이다.

현재 자신이 있는 위치에 대한 값 myLocation 의 지역에 대한 와이파이 개수 location_num 을 얻는다.

location_num의 개수는 API 의 검색 한번 당 최대로 가져올 수 있는 와이파이 개수 (1000개) 와 비교한다.

if문을 통해 1000개를 넘느냐, 넘지 않느냐에 따라 검색 횟수가 달라지도록 만들었다.

병합 전의 해당 기능에 대한 프로젝트에서 잘 실행됨을 해결했기에 에러가 왜 일어나는지 이해가 가지 않았다.


## 에러 메시지

   ```ruby
2020-07-13 17:32:18.802 5917-6262/? E/NetdEventListenerService: handleMessage: { when=-1ms what=10001 obj=com.android.server.connectivity.NetdEventListenerService$DnsResultParams@25d8f30 target=com.android.server.connectivity.NetdEventListenerService$DnsEventHandler }
2020-07-13 17:32:18.863 26757-26914/? E/AndroidRuntime: FATAL EXCEPTION: Thread-12
    Process: com.example.kakao_map, PID: 26757
    java.lang.StringIndexOutOfBoundsException: String index out of range: -1
        at java.lang.String.substring(String.java:2064)
        at com.example.kakao_map.MainActivity$1.run(MainActivity.java:381)
        at java.lang.Thread.run(Thread.java:919)
   ```

## 원인 추정

   ```ruby
java.lang.StringIndexOutOfBoundsException: String index out of range: -1
   ```

   ```ruby
location_num = Integer.parseInt(num.substring(0, num.length()-1)); 
   ```

에러 메시지 중요 파트와 에러가 발생한 지점이다.

<span style="color:red"> String index out of range: -1 은 문자열이 비어있는데 substring 하는 경우, 또는 AABBCC이렇게들어있는데 substring(5,7) 하는 경우 발생한다. </span>

위에서 설명했듯이 location_num 은 자신이 현재 위치한 지역구의 와이파이 총 개수를 저장하는 변수다.

kakao Map API 는 기본 위치 시작을 중구로 시작하기에 스레드가 한번은 실행 한다.

그러나 나는 서울에 살지 않는 10분 거리에 논밭이 펼쳐지는 촌구석 사람이다.

<span style="color:red"> 즉 스레드가 다시 실행될 타이밍에 들어있는 location_num 은 0개가 됨으로써 오류가 발생하고, 프로젝트 또한 강제 종료된다. </span>

만약 내가 서울에서 살았으면 이 문제를 아예 몰랐을 것이고, 고치지도 못했을 거란 생각에 안도감과 미묘한 슬픔을 느꼈다.   

## 어떻게 에러를 해결할 것인가?

서울 지역 이외에서 앱을 켰을 경우 와이파이를 검색하는 스레드를 실행하지 않도록 변경하고자 노력 중이다.

## 깨달은 점

   * 갑자기 에러 메시지가 길어지는 부분이 존재한다. 그 부분을 중점으로 검색해보자

## 참고

[참고하면 좋은 사이트 - StringIndexOutOfBoundsException](https://sweetpinklady.tistory.com/66)