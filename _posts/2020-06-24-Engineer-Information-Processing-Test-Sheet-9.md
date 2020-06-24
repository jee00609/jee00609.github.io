---
title: "2020년 정보처리기사 필기 문제 풀이 9번"
categories:
  - Engineer Information Processing
tags: 
  - Engineer Information Processing
last_modified_at: 2020-06-24
---

이번 문제는 운으로 맞췄던 것 같아 좀 더 상세히 작성해야 할 것 같다.

<span style="color:lightsteelblue"> 삼성과 한화 야구를 보다가 늦게 포스팅 한다. </span>

<span style="color:lightsteelblue"> 한화 이자식들은 야구를 하는건지 안하는 건지 9회말 투아웃 투스트라이크에 져버리는 대단한 놈들이다. </span>

<span style="color:lightsteelblue"> 가슴이 웅장해진다. </span>

## <span style="color:red"> 9. 트랜잭션이 올바르게 처리되고 있는지 데이터를 감시하고 제어하는 미들웨어는? </span>

① RPC

② ORB

③ TP monitor

④ HUB

정답 : ③ TP monitor

> ###### 제 1과목 - 인터페이스 설계 - 미들웨어 솔루션 명세
{: .small}

<cite>시나공</cite> --- 정보처리기사 필기,2020 시나공 기본서
{: .small}

## 미들웨어 (Middleware)

미들웨어는 미들 (Middle)과 소프트웨어 (Software)의 합성어로, 운영체제와 해당 운영체제에서 실행되는 응용 프로그램 사이에서 운영체제가 제공하는 서비스 이외에 추가적인 서비스를 제공하는 소프트웨어이다.

표준화된 인터페이스를 제공함으로써 시스템 간의 데이터 교환에 일관성을 보장한다.

## 미들웨어의 종류

미들웨어는 통신 제공 방법이나 기능에 따라 구분된다.

  * DB (DataBase)
  * RPC (Remote Procedure Call)
  * MOM (Message Oriented Middleware)
  * TP monitor (Transaction Processing Monitor)
  * ORB (Object Request Broker)
  * WAS (Web Application Server)

## 미들웨어의 종류 상세 설명

| 미들웨어             | 기능                                                             | 예시 |
| ------------         | ------------------------------------------------------------------------------------- | ----------------- |
| DB    | 데이터베이스 벤더에서 제공하는 클라이언트에서 원격의 데이터베이스와 연결하기 위해 제작 | ODBC, IDAPI, Glue         |
| RPC    | 응용 프로그램의 프로시저를 사용하여 원격 프로시저를 로컬 프로시저처럼 호출하는 방식 | Entra, ONC/RPC          |
| MOM    | 메시지 기반의 비동기형 메시지를 전달하는 방식의 미들웨어 | MQ, Message Q, JMS         |
| TP monitor    | 항공기나 철도 예약 업무 등과 같이 온라인 트랜잭션 업무에서 트랜잭션을 처리 및 감시하는 역할 | tuxedo, tmax      |
| ORB    | 객체 지향 미들웨어, 코바 표준 스펙을 구현 | Orbix, CORBA     |
| WAS    | 정적 콘텐츠를 다루는 웹서버와 달리 사용자의 요구에 따른 동적인 콘텐츠 처리를 위해 사용하는 미들웨어 | WebLogic, WebSphere       |


[참고하면 좋은 사이트 - TP-Monitor](https://technet.tmaxsoft.com/upload/download/online/tmax/pver-20140117-000058/getting-started/ch01.html)





 

