---
title: "Go 설치 및 Go 프로젝트 경로를 D 드라이브로 경로 바꾸기 - 윈도우"

categories:
  - QuickDraw
tags: 
  - Go
  - Window
last_modified_at: 2021-03-05
---

Go 언어를 공부하기 시작했는데 맨땅에 헤딩하듯이 시작하여 많은 시행착오를 겪었다.

언젠가 다시 깔 경우를 대비하여 기록을 남기고자 한다.

## Go 설치하기

가장 먼저해야 하는 것은 Go 공식 사이트에서 OS 에 맞는 버전을 다운 받는 것이다.

난 Window OS 로 다운 받았다.

[Go 다운로드 사이트](https://golang.org/dl/)

<figure>
	<a href="/assets/images/2021-03-05-GoInstall1.PNG"><img src="/assets/images/2021-03-05-GoInstall1.PNG"></a>
	<figcaption><a href="https://golang.org/dl/" title="Go 다운로드 사이트">Go 다운로드 사이트</a></figcaption>
</figure>

이미 깔려있다 보니 설치하지 못한다고 떠있다.

<figure>
	<a href="/assets/images/2021-03-05-GoInstall2.PNG"><img src="/assets/images/2021-03-05-GoInstall2.PNG"></a>
	<figcaption>이미 설치함</figcaption>
</figure>

그래서 다시 삭제하고 설치했다.

Destination Folder 를 D:\Program Files\Go 로 바꿔주도록 하자.

이후 CMD 창에서 Go 가 깔린 것을 볼 수 있다.

<figure>
	<a href="/assets/images/2021-03-05-GoInstall3.PNG"><img src="/assets/images/2021-03-05-GoInstall3.PNG"></a>
	<figcaption>기본 설치 경로를 D:\Program Files\Go 로 바꿔주자</figcaption>
</figure>

<figure>
	<a href="/assets/images/2021-03-05-GoInstall4.PNG"><img src="/assets/images/2021-03-05-GoInstall4.PNG"></a>
	<figcaption>go version 입력시 뜬다</figcaption>
</figure>

## GOROOT GOPATH 설정하기

제어판 - 시스템 및 보안 - 시스템 - 고급 시스템 설정 을 들어가자.

고급 - 환경변수 를 선택해 주면 창이 하나 뜬다.

시스템 변수의 GOROOT 의 경로가 설치한 경로가 맞는지 확인! 

아닐시 바꿔준다.

<figure>
	<a href="/assets/images/2021-03-05-GoInstall5.PNG"><img src="/assets/images/2021-03-05-GoInstall5.PNG"></a>
	<figcaption>환경변수 창에서 GOROOT 확인</figcaption>
</figure>

이후 환경 변수 창을 그대로 두고 Go 프로젝트가 생성될 워크스페이스를 만들어 주자.

이 때 가장 중요한 건 GOROOT 와 GOPATH 의 경로가 일치해선 안된다!

일치하게 될 경우 문제가 생기는데 이건 다음 포스팅에서 이야기하겠다.

<figure>
	<a href="/assets/images/2021-03-05-GoInstall6.PNG"><img src="/assets/images/2021-03-05-GoInstall6.PNG"></a>
	<figcaption>워크스페이스가 될 곳을 만들자</figcaption>
</figure>

이제 다시 환경 변수 창에서 GOPATH 를 입력해주면 된다.

사용자 변수의 것은 지워도 된다는데, 나는 사용자 변수와 시스템 변수 모든 곳에 같은 경로로 설정해주었다. 

<figure>
	<a href="/assets/images/2021-03-05-GoInstall7.PNG"><img src="/assets/images/2021-03-05-GoInstall7.PNG"></a>
	<figcaption>GOPATH 를 설정해주자</figcaption>
</figure>

## Path 경로 바꿔주기

사용자 변수와 시스템 변수 모두 Path 란 변수가 존재한다.

이곳에 D:\Program Files\Go\bin 를 추가해준다.

<figure>
	<a href="/assets/images/2021-03-05-GoInstall8.PNG"><img src="/assets/images/2021-03-05-GoInstall8.PNG"></a>
	<figcaption>PATH 를 설정해주자</figcaption>
</figure>

마지막으로 CMD 창에서 모든것이 세팅됬는지 확인하면 된다.

<figure>
	<a href="/assets/images/2021-03-05-GoInstall9.PNG"><img src="/assets/images/2021-03-05-GoInstall9.PNG"></a>
	<figcaption>세팅이 완료되었는지 확인하기</figcaption>
</figure>


Go IDE 는 Jetbrains GoLand와 Vistual Studio Code (vscode) 등이 있다.

GoLand 는 유료이지만 학생은 무료였기에 한번 GoLand 를 깔아서 Go 파일이 실행되는지 실험해보았다.

<figure>
	<a href="/assets/images/2021-03-05-GoInstall10.PNG"><img src="/assets/images/2021-03-05-GoInstall10.PNG"></a>
	<figcaption>성공!</figcaption>
</figure>


## 비고

[Go 프로그래밍 윈도우 기본 환경 설정](https://niceman.tistory.com/126)

[Go Module 알아보기](https://yoongrammer.tistory.com/33)

난 auto 로 해두었다.