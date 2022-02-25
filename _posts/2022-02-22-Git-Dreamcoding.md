---
layout: post
title: "Git(1) DreamCoding git 유투브 강의 공부"
tags: [Git, Github, GRJ]
comments: true
---

본 포스트는 DreamCoding의 깃,깃허브 제대로 배우기 강의를 수강한 후 쓴 글입니다.

---

> ✨ [DreamCoding의 git 유투브 강의 링크](https://www.youtube.com/watch?v=Z9dvM7qgN9s)

##### 목차

1. git 소개
2. git 설정
3. git 명령어 단축키
4. git 초기화/삭제

---

## 1. git 소개

> 💡 깃: 버전을 편리하게 관리할 수 있도록 도와주는 도구

우리가 작업하고 있는 파일들을 원하는 순간으로 다시 돌아갈 수 있게 만들어주는 도구

### git 설치

<mark>깃은 명령어를 기본으로 한 명령어 프로그램</mark> -> 터미널에서 커맨드로 배워야 깃을 정확히 사용하는 방법을 익힐 수 있다. 깃을 처음 배울 때는 터미널을 이용해서 명령어로 하나씩 공부해나가는 걸 추천한다.

물론 ui도 많이 있어서 [git 공식 사이트](https://git-scm.com/downloads/guis)에서 사용가능한 ui 어플리케이션에 대해 알아볼 수 있다. 깃을 잘 이해하고 기능을 잘 이용한다면 ui 사용도 추천한다.

- 깃허브 데스크탑 - 기능이 제한되어 비추
- 아틀라시안 Sourcetree(소스트리) - ui가 조금 클래식하지만 다양한 기능 포함해서 추천
- GitKraken(깃크라켄) - 화려한 ui 좋아하면 추천

##### 깃 설치 전 터미널이 필요 - 맥북이라면 iTerm2 프로그램 이용해보자

맥이나 윈도에 기본적으로 내장되어 있는 터미널을 써도되지만 조금 더 편리한 툴을 이용하고 싶다면
맥에서는 iTerm2, 윈도우라면 cmder을 추천(윈도우에서 cmder를 설치하면 git이 포함되어 설치됨)

##### 깃 설치 후 설치 여부 확인

터미널에 아래 명령어 입력하면 설치된 깃의 버전을 확인할 수 있다.

```css
git --version
```

##### 만약 깃이 설치가 안되어 있다면

[깃 공식 사이트의 다운로드 페이지](https://git-scm.com/downloads/guis)에서 자신의 운영체제에 맞게 다운로드 할 수 있다.

##### Sourcetree를 설치하려면

[Sourcetree(소스트리) 공식 사이트](https://www.sourcetreeapp.com/)에 가서 자신의 운영체제에 맞게 다운로드 할 수 있다.

---

## 2. git 설치 후 설정

터미널에서 아래 명령어를 작성하면 모든 설정을 확인할 수 있고

```css
git config --list
```

다시 q를 누르면 터미널로 돌아올 수 있다.
만약 파일로 열어 보고 싶으면 글로벌로 설정된 edit(편집)모드를 열게되면

```css
git config --global -e
```

터미널에서 모든 설정을 확인할 수 있다.

터미널이 아니라 텍스트 에디터에서 열어보고 싶다면 각자 원하는 텍스트 에디터를 연결할 수 있는데
강의에서는 visual studio code를 연결해보도록 한다.

##### visual studio code 연결

각 텍스트 에디터마다 연결방법이 다른데, 보통 커맨드 팔레트 툴에서 'code'를 검색하면 연결할 수 있는 shell command에 설정할 수 있는 명령어가 나온다.
visual studio code는 연결 설정 후 터미널에

```css
code .
```

를 입력하면 연동이 된다. 또한

```css
git config --global -core.editor "code --wait"
```

로 글로벌적으로 설정하고 -core.editor "code --wait"는 방금 쓴 코드를 작성하는 명령어고
그냥 "code"를 쓰면 그 다음 다른 명령어를 바로 칠 수 있다. code --wait를 작성하면 텍스트 에디터에서 열린 파일이 저장되기 전까지는 다른 명령어를 쓸 수 없게 코드가 '기다린다'.

##### 사용자 정보 설정

동일하게 깃 글로벌 명령어를 작성한 다음에 유저의 정보를 설정해보자.

```css
git config --global user.name"lisoh"
git config --global user.email"lisoh@mail.com" //본인의 정보로 작성해야함
```

이렇게 설정하고

```css
git config user.name
```

명령어를 작성하면 내가 저장한 나의 이름이 출력되는 걸 볼 수 있다.

##### 운영체제간 줄바꿈 코드 자동변경 설정

```css
git config --global core.autocrlf true //윈도우 사용자라면
git config --global core.autocrlf input //맥 사용자라면
```

를 작성하면 에디터에서 새로운 줄바꿈을 할 때 들어가는 문자열이 달라진다.
기본적으로 윈도우는 /r/n , 맥은 /n을 작성해주는데, 위의 명령어를 쓰면
운영체제를 오갈 때 알아서 /r을 붙이거나 삭제해준다.

---

## 3.git 명령어

'git + 명령어' 형태로 명령어가 이루어진다.
[깃 공식 사이트의 documentation - reference 페이지](https://git-scm.com/docs)를 가면 git의 모든 명령어를 볼 수 있다.

##### 터미널 명령어

```css
mkdir [폴더이름] //폴더 만들기
cd [폴더이름] //폴더로 이동하기
ls -al //폴더(디렉토리)내용 나열하기
```

##### 자주쓰이는 명령어

```css
git init //git 초기화 -> 자동으로 master 브랜치가 생성된다.
rm -rf git //git을 삭제
git status //git의 상태를 볼 수 있음
git config --global alias //터미널안에서 명령어를 단축해서 쓸 수 있게 하는 명령어
git config --global alias.st status // status를 st로 단축해서 설정해달라
git config --h //git 명령어와 명령어의 속성값을 보고싶으면 명령어 뒤에 --h를 입력하면 된다.
```

폴더 앞에 '.'이 붙으면 숨겨진 폴더라는 뜻.
그냥 ls를 치면 나오지 않는다.
master branch : 기본적으로 commit에서 버전을 관리하는 브랜치

---

## 4.git 초기화/삭제

##### 터미널에서 git 초기화 및 삭제하는 방법

```css
git init //git 초기화 -> 자동으로 master 브랜치가 생성된다.
rm -rf git //git을 삭제
```

##### ui로 git을 초기화하고 관리하는 방법 (Sourcetree)

이미 기존에 만든 git이 있다면 Sourcetree를 열고 그안에 git폴더를 드래그함으로써 git을 추가할 수 있다.
새로운 git은 new 버튼을 눌러서 만들 수 있다.
create local repository를 누르면 원하는 경로에 깃 레포지터리를 만들 수 있다.
