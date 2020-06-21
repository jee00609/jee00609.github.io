---
title: "2020년 정보처리기사 필기 문제 풀이 6번"
header:
  teaser: "/assets/images/ISO-IEC-9126.png"
categories:
  - Engineer Information Processing
tags: 
  - Engineer Information Processing
last_modified_at: 2020-06-21
---

이번 문제는 운으로 맞췄던 것 같다.

## <span style="color:red"> 6. UML 확장 모델에서 스테레오 타입 객체를 표현할 때 사용하는 기호로 맞는 것은? </span>

① << >>

② (( ))

③ {{ }}

④ [[ ]]

정답 : ① << >>

> ###### 제 1과목 - 요구사항 확인 - 요구사항 확인 - UML
{: .small}

<cite>정보처리기사 출제기준</cite> --- 한국산업인력공단
{: .small}

## ISO/IEC 9126

UML 모델에서 스테레오타입은 다른 모델 요소의 용도를 식별하는 모델 요소이다.

UML 모델 요소에 스테레오 타입을 적용하면 아래 이미지처럼 만들어진다.

<figure style="width: 150px" class="align-center">
  <a href="https://www.ibm.com/support/knowledgecenter/ko/SS4JE2_7.5.5/com.ibm.xtools.modeler.doc/images/tasnstyp.gif"><img src="https://www.ibm.com/support/knowledgecenter/ko/SS4JE2_7.5.5/com.ibm.xtools.modeler.doc/images/tasnstyp.gif"></a>
</figure>

## 표준 UML 2.1 모델 요소 스테레오타입

<table cellpadding="4" cellspacing="0" summary="" border="1" class="simpletable"><tr class="sthead"><th valign="bottom" align="left" id="d20856e48" class="stentry">스테레오타입</th>
<th valign="bottom" align="left" id="d20856e50" class="stentry">모델 요소</th>
<th valign="bottom" align="left" id="d20856e52" class="stentry">설명</th>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«auxiliary»</td>
<td valign="top" headers="d20856e50" class="stentry">클래스</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 일반적으로 제어 메커니즘을 제공해서 다른 클래스를
지원하는 클래스에 적용됩니다. 지원되는 클래스는
초점 클래스입니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«buildComponent»</td>
<td valign="top" headers="d20856e50" class="stentry">컴포넌트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 조직 또는 시스템 레벨 개발을 위한 컴포넌트 세트를 지정하는
컴포넌트에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«create»</td>
<td valign="top" headers="d20856e50" class="stentry">오퍼레이션</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 예를 들어, 오퍼레이션이 생성자인 경우 클래스류의
인스턴스를 작성하는 오퍼레이션에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«destroy»</td>
<td valign="top" headers="d20856e50" class="stentry">오퍼레이션</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 클래스류의 인스턴스를 제거하는
오퍼레이션에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«document»</td>
<td valign="top" headers="d20856e50" class="stentry">아티팩트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 문서를 나타내는 아티팩트에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«entity»</td>
<td valign="top" headers="d20856e50" class="stentry">컴포넌트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 비즈니스 개념을 표시하는 컴포넌트에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«executable»</td>
<td valign="top" headers="d20856e50" class="stentry">아티팩트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 노드에서 실행할 수 있는 아티팩트에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«file»</td>
<td valign="top" headers="d20856e50" class="stentry">아티팩트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 소스 코드나 데이터를 포함하는
아티팩트에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«focus»</td>
<td valign="top" headers="d20856e50" class="stentry">클래스</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 하위 메커니즘을 제공하는 보조 클래스가 있는
코어 논리 또는 제어를 지정하는 클래스에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«framework»</td>
<td valign="top" headers="d20856e50" class="stentry">패키지</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 클래스, 패턴 및 템플리트와 같이 재사용 가능한
요소를 포함한 패키지에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«implement»</td>
<td valign="top" headers="d20856e50" class="stentry">컴포넌트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 종속성이 있는 스펙의 구현이며 스펙이 없는
컴포넌트에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«implementationClass»</td>
<td valign="top" headers="d20856e50" class="stentry">클래스</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 클래스 인스턴스에 둘 이상의 클래스가 있을 수 없는
클래스 구현에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«library»</td>
<td valign="top" headers="d20856e50" class="stentry">아티팩트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 정적 또는 동적 라이브러리 파일인
아티팩트에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«metaclass»</td>
<td valign="top" headers="d20856e50" class="stentry">클래스</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 인스턴스가 메타클래스에 맞는 기타 클래스인
클래스에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«metamodel»</td>
<td valign="top" headers="d20856e50" class="stentry">모델</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 다른 모델의 추상인 모델을 포함한
패키지에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«modelLibrary»</td>
<td valign="top" headers="d20856e50" class="stentry">패키지</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 재사용할 모델 요소를 포함한 패키지에
적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«perspective»</td>
<td valign="top" headers="d20856e50" class="stentry">패키지</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 다이어그램 또는 하위 패키지만 포함한
패키지에 적용됩니다. 추출기는 이 스테레오타입이 적용된 패키지를 무시합니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«process»</td>
<td valign="top" headers="d20856e50" class="stentry">컴포넌트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 트랜잭션 기반의 컴포넌트에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«realization»</td>
<td valign="top" headers="d20856e50" class="stentry">클래스류</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 오브젝트 도메인 및 구현을 지정하는 클래스류에
적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«responsibility»</td>
<td valign="top" headers="d20856e50" class="stentry">노트, 텍스트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 모델 요소의 다른 모델 요소에 대한 의무를
설명하는 노트에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«script»</td>
<td valign="top" headers="d20856e50" class="stentry">아티팩트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 컴퓨터 시스템으로 해석할 수 있는 파일에
적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«service»</td>
<td valign="top" headers="d20856e50" class="stentry">컴포넌트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 값을 계산하는 컴포넌트에
적용됩니다. 이 컴포넌트는 상태가 없습니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«source»</td>
<td valign="top" headers="d20856e50" class="stentry">아티팩트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 실행 파일의 소스 파일에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«specification»</td>
<td valign="top" headers="d20856e50" class="stentry">클래스류</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 구현이 아닌 오브젝트 도메인을 지정하는
클래스류에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«subsystem»</td>
<td valign="top" headers="d20856e50" class="stentry">컴포넌트</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 큰 시스템의 파트인 컴포넌트에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«systemModel»</td>
<td valign="top" headers="d20856e50" class="stentry">모델</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 시스템의 다른 Perspective를 설명하는
모델을 포함한 패키지나 모델에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«type»</td>
<td valign="top" headers="d20856e50" class="stentry">클래스</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 오브젝트 도메인 및 오퍼레이션을 설명하지만,
오브젝트의 구현을 정의하지 않는 클래스에 적용됩니다. </td>
</tr>
<tr class="strow"><td valign="top" headers="d20856e48" class="stentry">«utility»</td>
<td valign="top" headers="d20856e50" class="stentry">클래스</td>
<td valign="top" headers="d20856e52" class="stentry">이 스테레오타입은 인스턴스가 없지만 속성 및 오퍼레이션에
클래스 범위가 있는 클래스에 적용됩니다. </td>
</tr>
</table>

[참고하면 좋은 사이트 - UML 스테레오타입](https://www.ibm.com/support/knowledgecenter/ko/SS4JE2_7.5.5/com.ibm.xtools.modeler.doc/topics/cstereotyp.html)





 

