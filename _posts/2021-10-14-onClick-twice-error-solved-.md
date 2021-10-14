---
title: "[JAVA SCRIPT] On Cllick 내부 On Click 구조 속 동작 에러 해결"

categories:
  - Java Script
tags: 
  - Java
  - Error

last_modified_at: 2021-10-14
---

졸업 작품의 완성이 눈에 보이기 시작해서 드디어 오류와 해결 과정을 포스팅 해보려 한다.

## 서문

졸업 작품은 백 엔드 뿐만 아니라 프론트 엔드까지 혼자서 구현해야 하다보니 참 힘들었다.

아무리 내부 기능을 다 만들어도 화면에서 그것을 요청하지 못하면 없는 것과 다름없으니 말이다.

이번에 작성하고자 하는 것은 즉 화면의 동작 상태에서 발생했던 오류와 이를 해결한 방법이다.

## 구조

<figure class="align-center">
  <a href="/assets/images/2021-10-14-page1.jpg"><img src="/assets/images/2021-10-14-page1.jpg"></a>
  <figcaption>메인 페이지</figcaption>
</figure>

이미지를 선택해서 AWS S3 에 업로드 시 사진 속의 Object 를 추출하여 동적으로 카드를 출력한다.

## 카드에 버튼 호버 시

<figure class="align-center">
  <a href="/assets/images/2021-10-14-card.PNG"><img src="/assets/images/2021-10-14-card.PNG"></a>
  <figcaption>Object Card Mouse Hover</figcaption>
</figure>

카드를 선택하고자 마우스를 호버하면 카드가 변화함과 동시에 More 또한 하나의 Input 버튼으로써 동작한다.

이제 More 버튼을 누르면서 문제가 생겼다.

## 오류의 서막 - More 버튼 호버 시

<figure class="align-center">
  <a href="/assets/images/2021-10-14-lastCard .PNG"><img src="/assets/images/2021-10-14-lastCard .PNG"></a>
  <figcaption>상세 카드</figcaption>
</figure>

More 버튼을 클릭하면 상세 카드가 아래에 출력되도록 구현했다.

상세 카드는 선택한 Object 를 발음하라는 내용과 함께 해당 단어에 대한 발음을 평가할 수 있는 페이지로 넘어갈 수 있도록 Rating 버튼이 존재했다.

처음에는 미리 제작해두었던 Rating 버튼 태그에 On Click 기능을 넣고자 했다.

* 기본 코드

```javascript
//미리 만들었던 코드

$targetObject.innerHTML = `
	<h2>${thisObj}</h2>
	<p>Please Speak ${thisObj} loudly</p>
	<img src='https://assets.codepen.io/2301174/icon-supervisor.svg' alt=''>
	<button type='button'> Rating </button>						
	`;

```

* 오류 코드

```javascript
//이제 여기다가 특정 함수로 인자를 보낼 수 있도록 구현하고자 했다.
$targetObject.innerHTML = `
	<h2>${thisObj}</h2>
	<p>Please Speak ${thisObj} loudly</p>
	<img src='https://assets.codepen.io/2301174/icon-supervisor.svg' alt=''>
	<button type='button' onClick='button1_click(${thisObj});'> Rating </button>						
	`;

```

이제 여기서 부터 문제가 발생했다.

```ruby
Uncaught ReferenceError: is not defined at HTMLButtonElement.onclick
```
버튼 onClick 속의 인자인 thisObj 를 인식하지 못하는 오류였다.

이를 해결하기 위해 arrow Function 을 이용해 보기로 했다.


```javascript
//이제 여기다가 특정 함수로 인자를 보낼 수 있도록 구현하고자 했다.
$targetObject.innerHTML = `
	<h2>${thisObj}</h2>
	<p>Please Speak ${thisObj} loudly</p>
	<img src='https://assets.codepen.io/2301174/icon-supervisor.svg' alt=''>
	<button type='button' onClick={()=>button1_clcick(${thisObj})}> Rating </button>						
	`;
```


## 오류의 절정 - 외부 onClick 버튼 동작 무시

<figure class="align-center">
  <a href="/assets/images/2021-10-14-card.PNG"><img src="/assets/images/2021-10-14-card.PNG"></a>
  <figcaption>More 에서 바로 다음 페이지로 넘어간다</figcaption>
</figure>

More 버튼을 클릭 할 시 바로 다음 페이지로 이동했다.

밑에 상세 카드가 출력되지 못한 채로 바로 다음 페이지로만 넘어가는 문제였다.

## 최종 해결

```javascript
// document.createElement 기능을 사용

$targetObject.innerHTML = `
	<h2>${thisObj}</h2>
	<p>Please Speak ${thisObj} loudly</p>
	<img src='https://assets.codepen.io/2301174/icon-supervisor.svg' alt=''>						
	`;
let inputAudio = "audioName.wav"
	
let ratingBtn = document.createElement('input');
ratingBtn.setAttribute("type", "button");
ratingBtn.setAttribute("id", "apiBtn");
ratingBtn.setAttribute("value", "Rating");
ratingBtn.onclick = ()=> button1_click(inputAudio,thisObj);

$targetObject.appendChild(ratingBtn);
```

ratingBtn 이라는 변수에 input 태그의 속성을 세팅해준 다음 $targetObject 의 뒤에 붙여주는 것이었다.

그러면 다음과 같은 논리 구조가 된다.

   * Main Page 에서 More 버튼을 클릭한다.
   * $targetObject 에서 innerHTML 을 통해 상세 카드가 생성된다.
   * 생성이 종료된 이후 ratingBtn 이 생성되며, 이후에 $targetObject 에 붙여진다.

이런 논리구조에선 처음 생성 될때 자동적으로 onClick 이 실행되는 것을 막을 수 있었다.

## 최종 구조

* 첫 화면

<figure class="align-center">
  <a href="/assets/images/2021-10-14-page1.jpg"><img src="/assets/images/2021-10-14-page1.jpg"></a>
  <figcaption>메인 페이지</figcaption>
</figure>

* More 버튼 클릭 시

<figure class="align-center">
  <a href="/assets/images/2021-10-14-lastCard .PNG"><img src="/assets/images/2021-10-14-lastCard .PNG"></a>
  <figcaption>상세 카드 출력</figcaption>
</figure>

* Rating 버튼 클릭 시

<figure class="align-center">
  <a href="/assets/images/2021-10-14-nextPage.PNG"><img src="/assets/images/2021-10-14-nextPage.PNG"></a>
  <figcaption>다음 페이지로 제대로 넘어간다.</figcaption>
</figure>

## 느낀점

아무리 생각해도 화면에서 나타나는 오류는 에러 내용이 자세하지 못해서 왜 오류가 났는지 찾는 것도 힘들다고 느꼈다.

그래도 논리구조적인 부분에서 오류가 있었고 이를 해결할 수 있었다는 점에서 기뻤다!

## 참고 자료

[Binding vs Arrow-function (in JavaScript, or for react onClick)](https://stackoverflow.com/questions/50375440/binding-vs-arrow-function-in-javascript-or-for-react-onclick)