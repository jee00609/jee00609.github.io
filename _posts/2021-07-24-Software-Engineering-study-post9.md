---
title: "소프트웨어 공학 - Chpater 18. 서비스 지향 소프트웨어 공학"

categories:
  - Software Engineering
tags: 
  - Software Engineering
last_modified_at: 2021-07-24
---

서비스 지향 아키텍처(SOA)는 네트워크에서 공통의 통신 언어를 사용하는 서비스 인터페이스를 활용하여 소프트웨어 구성 요소를 다시 사용할 수 있게 만드는 소프트웨어 설계 유형이다.

이번 장에선 서비스 지향 소프트웨어란 무엇이고 각각의 예시를 살펴보고자 한다.

## 서비스 지향 소프트웨어 공학 목차
* 서비스 지향 아키텍처  
* RESTful 서비스

## Web Services [550p]

* 웹 서비스
   * 다른 프로그램이 사용 가능하게 한 계산 및 정보자원을 위한 표준
   * 서비스는 서비스를 사용하는 애플리케이션과 독립적
   * 서비스 제공자는 조직 외부의 사용자에게 서비스를 제공

* A Web Service is
   * A loosely coupled, reusable software component that encapsulates discrete functionality, which may be distributed and programmatically accessed. <br/>A web service is a service that is accessed using standard Internet and XML-based protocols
   * 서비스가 독립적이고 느슨하게 연결
   * 외부 컴포넌트에 의존하지 않음, 서비스 기능과 매개변수
   * HTTP,SOAP 등 인터넷과 틔 기반 프로토콜을 이용하여 접근
   * 플랫폼 및 구현 언어에 독립적

## Web Services [551p]

* 서비스 지향 접근법의 장점
   * 조직 내부나 외부의 서비스 제공자에 의해 제공
   * 서비스에 대한 정보가 공개되어 있으며 권한이 있으면 누구나 사용
   * 배치 (Deploy) 또는 실행 시 까지 서비스 바인딩 연기 가능
   * 기존 서비스들을 이용하여 새로운 서비스 구축 가능
   * 서비스 사용에 따른 비용 지불 가능
   * 외부 서비스를 이용하여 애플리케이션 경량화 가능


## Service-oriented Architectures [554p]

<figure class="align-center">
  <a href="/assets/images/2021-07-24-SOA.PNG"><img src="/assets/images/2021-07-24-SOA.PNG"></a>
  <figcaption>TPM 의 활용</figcaption>
</figure>

* 분산 환경에서 독립적으로 수행되는 서비스들을 이용
* 서비스는 서비스 제공자의 컴퓨터에서 수행됨
* 서비스 통신과 정보 교환을 위한 표준 프로토콜이 개발됨
   * XML Web Service : 복잡, 실행 오버헤드가 상당함 
   * RESTful : 간단, 복잡한 기능을 제공하는 서비스에는 부적절

* SOA 장점
   * 외부 제공자에게 서비스를 아웃소싱 가능
   * 서비스는 언어 독립적
   * 단순화된 정보 교환을 통해 조직 간의 컴퓨팅이 가능

## Service-oriented Architectures [554p]

* 서비스 지향 아키텍처 구조
   * 서비스 제공자
      * 서비스를 설계하고 구현
      * 서비스에 대한 인터페이스 명세를 생성
      * 서비스에 대한 정보를 레지스트리에 등록
   * 서비스 요청자
      * 서비스 명세를 검색하여 서비스 제공자를 찾음
      * 표준 서비스 프로토콜을 이용
      * 애플리케이션을 서비스와 연결
   * 서비스 레지스트리

## Key Standares [555p]

* 서비스 지향 아키텍처의 핵심적인 표준
   * SOAP (Simple Object Access Protocol)
      * 서비스 메시지 교환 표준

   * WSDL (Web Service Description Language)
      * 서비스 인터페이스 정의 표준
      * 서비스 오퍼레이션
         * 이름, 매개변수, 타입
      * 서비스 바인딩

   * WS-BPEL
      * 워크플로우 언어 표준

   * UDDI
      * 서비스 명세, 서비스 검색

Tip)

1. SOAP : 서비스 사이의 통신을 지원하는 메시지 교환 표준이다. 이것은 서비스 간에 전달되는 메시지의 필수적인 컴포넌트와 선택적인 텀포넌트를 정의한다. <br/>서비스 지향 아키텍처에서의 서비스는 종종 SOAP 기반 서비스라고 불린다.
2. WSDL : 웹 서비스 정의 언어는 서비스 인터페이스 정의를 위한 표준이다. <br/>이것은 서비스 오퍼레이션과 서비스 바인딩이 정의되는 방식을 결정한다.

## Web service description Language [556p]

* 인터페이스 (What)
   * 서비스가 지원하는 오퍼레이션, 송수신 하는 메시지 형식
* 바인딩 (How)
   * 추상 인터페이스를 구체적인 프로토콜 집합으로 변환
* 구현 위치 (Where)
   * 웹 서비스의 엔드 포인트

## RESTful Services [559p]

* SOAP / WSDL을 이용한 XML 웹서비스 표준의 문제점
   * 무거움 (Heavyweight)
   * 필요 이상으로 일반적 (Over-general)
   * 비효율적 (Inefficient)

* 웹서비스의 대안
   * REST (REpresentational State Transfer) 는 서버에서 클라이언트로 자원을 전송하는 방식
   * RESTful 은 overhead 가 적은 서비스

* 자원 (Resources)
   * RESTful 이 기본 요소는 자원
   * 자원은 식별자를 가짐
   * 기본적으로 자원은 카탈로그 및 의료 기록 혹은 이 책의 장과 같은 문서에 해당하는 데이터 요소이다.

## RESTful Services [560p]

* 지원 오퍼레이션
   * Create : 자원을 생성 (존재해야 함) -> POST
   * Read : 자원값을 읽음 (표현을 반환) -> GET
   * Update : 자원의 값을 변경함 -> PUT
   * Delete : 자원을 접근 불가능하게 함 -> DELETE

## RESTful Services [561~562p]

* JSON (JavaScript Object Notation) 의 사용
   * 웹서비스는 XML을 사용하여 오버헤드가 큼

* RESTful 의 문제점
   * 서비스가 복잡하고 자원이 단순하지 않을 때 서비스 설계가 어려움
   * 공식적인 RESTful 서비스 표준이 없음
   * 서비스 품질 (QoS) 이나 신뢰성을 위한 구조를 직접 구현해야 함

* RESTful 과 SOAP API 동시 제공