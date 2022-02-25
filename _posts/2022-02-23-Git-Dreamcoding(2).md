---
layout: post
title: "Git(2) DreamCoding git 유투브 강의 공부"
tags: [Git, Github, GRJ]
comments: true
---

본 포스트는 DreamCoding의 깃,깃허브 제대로 배우기 강의를 수강한 후 쓴 글입니다.

---

> ✨ [DreamCoding의 git 유투브 강의 링크](https://www.youtube.com/watch?v=Z9dvM7qgN9s)

##### 목차

part2.Basic

1. git workflow
2. git add
3. git ignore
4. git status
5. git diff
6. git commit

---

## 1. git workflow

git에는 크게 총 3가지의 작업 환경이 나눠져 있다.

    - working directory : 프로젝트의 파일을 수정하는 곳
    - staging area : 버젼 히스토리에 저장 할 준비가 되어있는 파일들을 옮겨 놓는 곳
    - .git directoroy : commit명령어를 이용해 파일을 저장해두는 곳

.git directory에 저장된 버젼들은 `check out`이라는 명령어를 이용해서 언제든지 원하는 버전으로
다시 돌아갈 수 있다.
또한 보통 내 컴퓨터에만 저장되기때문에, `push`라는 명령어를 이용해 나의 git directory를 서버에 업로드해둔다. 서버에서 다시 내 컴퓨터에 다운로드할 때는 `pull`이라는 명령어를 이용해 다운받는다.

각각의 commit들은 snapshot된 정보들을 기반으로 고유한 해시 코드가 부가된다.이 코드를 이용해 버전 정보를 참조할 수 있다.그리고 이 commit에는 id뿐 아니라 버전에 관련된 메시지,저자,날짜와 시간 정보도 함께 포함되어 있다.

##### working directory

    - untracked와 tracked로 나눠진다.
    - git이 트랙킹하는 파일이면 tracked, 새로 만들어진 파일이나 기존에 존재하던 프로젝트에서 깃을 초기화하면 깃이 파일에 대한 정보가 없어 untracked된다.
    - 또한 tracked는 수정 여부에 따라 unmodified, modified로 나뉜다. 수정이 되지 않았다는 것은 이전 버젼에 비해 수정이 안되었다는 의미고, 수정이된 modified파일만 staging area로 갈 수 있다.

---

## 2. git add

예제)

```css
echo hello world! > b.txt
echo hello world! > c.txt
```

터미널에서는 위로 향하는 방향키를 누르면 이전 명령어를 재사용할 수 있다.
여기서 `ls`를 입력하면 현재 만들어진 txt파일들을 확인할 수 있고
`git status`를 입력하면 지금 현재 파일들의 상태를 확인할 수 있다.

![Gitadd image](https://media.vlpt.us/images/lisoh/post/2dcaae14-4df6-4207-8be1-34bd4c2fc556/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-23%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.15.49.png "Gitadd image"){: .center-image}

:어떤 브랜치에 있는지, 커밋 여부, 트랙킹 여부

깃이 tracking할 수 있도록 파일들을 staging area에 옮기려면
`git add`명령어를 터미널에 입력한다.
a.txt파일만 올리고 다시 `git status`를 입력하면

![Gitadd-staged image](https://media.vlpt.us/images/lisoh/post/a5e69c34-abfe-4b64-a82a-964c4b9e590e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-23%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.18.59.png "Gitadd-staged image"){: .center-image}

이렇게 커밋할 준비가 된 변경사항,a.txt파일을 볼 수 있다.

존재하는 모든 txt파일을 staging area에 옮기고 싶다면
`git add *.txt`명령어를 사용하면 된다. \* - 전체를 의미

모든 파일을 옮기고나서 a.txt파일만 수정하면

![Gitmodified image](https://media.vlpt.us/images/lisoh/post/ab68a5df-f2a0-4425-87f6-6c5065bfabd6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-23%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.22.26.png "Gitmodified image"){: .center-image}

다시 `git status`명령을 입력했을때 modified된 a.txt파일을 볼 수 있다.

`git rm --cached <file>...` 원하는 파일을 여기 넣어 명령어를 실행하면
그 파일을 다시 working directory - untracked 상태로 내려보낼 수 있다.

`git add *`명령어를 쓰면 git 에 있는 모든 파일을 git staging area로 보낼 수 있다. (삭제된 파일 빼고)
그런데 `git add .`명령어를 쓰면 삭제된 파일까지 모두 git staging area로 보낼 수 있다.

---

## 3. git ignore

tracking하고 싶지 않은 파일들, git에 포함하고 싶지않은 파일들은 git ignore파일에 넣는다.

만약 .log로 끝나는 파일들은 모두 git에 넣고싶지 않다면,
`echo *.log > .gitignore` 명령어를 실행하면 모든 log파일이 gitignore파일에 추가된다.

만약'폴더이름/'을 gitignore에 넣으면 그 폴더안에 있는 모든 파일을 gitignore안에 넣게된다.

---

## 4. git status

`git status -h`를 터미널에 입력하면 status에 관련된 모든 옵션을 볼 수 있다.
status에 옵션을 따로 적용하지 않으면 기본적으로 --long 옵션이 적용된다.(default)

-s 로 좀더 간결하게 나타내면

![Git-status image](https://media.vlpt.us/images/lisoh/post/3dabb8cc-d998-4af8-827d-43e64673d584/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-23%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.37.52.png "Git-status image"){: .center-image}

이런식으로 staging area는 A, modified는 M으로 나타내지는 걸 볼 수 있다.
하지만 초반에는 기본 옵션으로 길게 보는 것을 추천한다.

> tip)<br/>
> 터미널에<br/>
> 윈도우는 cntrl+ k<br/>
> 맥은 cmd + k<br/>
> 를 누르면 터미널 창이 깨끗하게 지워진다.

---

## 5. git diff

정확히 어떤 내용이 수정되었는지 보려면 이 명령어를 실행한다.
기본 옵션으로는 working directory의 파일의 변경사항만 보여준다.
staged된 파일들의 변경사항을 보고 싶다면 `git diff --staged`를 실행한다.
마찬가지로 `git diff -h`를 입력하면 diff에서 쓸 수 있는 옵션들을 볼 수 있다.
`git diff -cache`명령어는 `git diff --staged`와 같은 의미로 쓰인다.

텍스트 에디터에 연결하려면 `git config --global -e`을 실행하고
열린 에디터의 config파일에서 다음 이미지의 [diff]와 [difftool "vscode"]부분을 추가하고 저장한다.
그다음 터미널에서 `git difftool`을 입력하고 y(yes)를 입력하면 vscode가 연결된다.

---

## 6. git commit

버전을 만들 때 - `commit` 명령어 사용
title과 description을 작성한 후 commit하면 해시코드 id와 title이 보여진다.
git 히스토리를 보기위해서는 git log를 실행한다.

보통은

```css
git add .
git commit -m "커밋메시지"
```

를 입력해 간단하게 commit할 수 있다.

만약 staged area와 working directory에 있는 모~든 파일을 전부 한번에 commit하고 싶다면
`git commit am "커밋메시지"`를 실행하면 된다.

##### 권장되는 커밋 규모

어플리케이션을 세분화해서 기능별로, 작은 단위로 만드는 것이 중요하므로 적당히 작은 단위로 나누어 커밋하는게 좋다. 또한, 의미있는 단위로 나누고 이름을 지정해서 커밋하는게 좋다.
꼭! 커밋 메시지에 맞는 내용만 커밋하기!

보통 현재형,동사로 커밋메시지를 작성한다.
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
