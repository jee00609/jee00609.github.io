---
title: "Git을 이용한 버전 관리 - Git 이란?"

categories:
  - GIT
tags: 
  - GIT
  - Hanium
  - Elice
last_modified_at: 2020-09-28
---

Git 기초를 elice 에서 수업 듣고 메모한 것들을 작성한다.

하계 학술대회에 논문을 제출했다.

좋은 성적있길 기대하고 있다.


## Git 을 이용한 버전 관리 목차
* Step 1. [Git을 이용한 버전 관리 - Git 이란?](https://jee00609.github.io/git/Hanium-Pratice-Git-Version1/)

## Git 기초

### Git 이란?

여러명이 효율적으로 협업하기 위한 툴

   * 오픈 소스 이므로 누구나 사용 가능
   * 옛 버전의 파일을 지우지 않는다.
   * 여러 버전을 동시에 관리할 수 있어 데이터의 안전성을 보장한다.

## Git 특징
   1. 가지 치기와 병합
   2. 가볍고 빠름 
      * 로컬에서 작업-공유시에만 네트워크 사용
      * Git 은 SVN 과 달리 각 개발자가 중앙 집중된 서버 저장소와 독립된 상태로 작업 가능
   3. 분산 작업에 효율적
   4. 데이터 보장
   5. 준비 영역(Staging area) 존재
      * Staging area 는 Git 영역 중 검토 단계로 보면 된다.
      * Working Directory →  git add→ Staging Area →  git commit→ Repository
   6. 오픈 소스 (누구나 프로젝트에 기여 가능)

### Git 호스팅 서비스
   * GitHub
   * Bitbucket
   * GitLab

## Git 설치와 초기 설정

   1. Git 설치
   2. Git 설치 확인
      * git --version
   3. Git 초기 설정
      * git config --global user.name “대충 이름”
      * git config --global user.email “대충 메일”
   4. 설정 정보 확인
      * git config --list
      * 프로젝트 마다 다른 사용자 정보를 지정하고 싶으면 저장소 생성 후 --global 옵션 빼고 실행하기

## Git 저장소 생성

기존 디렉토리를 이용해 사용하려면 Git 을 사용할 프로젝트 폴더로 이동 후 git init 명령어 실행

   * git init : 기존의 디렉토리를 git repository로 설정
   * ls -al 로 .git 파일 생성 확인 가능

## Git 명령어

| 명령어            | 설명                                                           |
| ------------         | ------------------------------------------------------------------ |
| git version    | git의 버전 확인  |
| git init    | git저장소 생성  |
| git config --global user.name "<이름>" | git관련 작업 기록에 남는 이름 수정 |
| git config --global user.email "<이름>" | git관련 작업 기록에 남는 이름 수정 |
|git config --list | git 설정 확인|

