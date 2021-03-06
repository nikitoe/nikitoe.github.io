---
layout: post
title: Study-Git-post3
image: /assets/img/blog/study/background-git2.png
sitemap: false
hide_last_modified: false
categories:
  - study
  - git
---

# [Git]기본 정리

---
* toc
{:toc .large-only}

# Git 기본 정리

## SET UP

<aside>
💡 Terminal 추천

</aside>

> MAC 사용자는 [Iterm2](https://iterm2.com/)
>
> WINDOW 사용자는 [cmder](https://cmder.net/) (※ Git이 포함되서 설치됨)

<br>

- [깃 홈페이지](https://git-scm.com/downloads)에서 다운로드 받는다.

<br>

- ‘git --version’ 커멘드를 통해 git 버전을 확인할 수 있다.

```bash
C:\폴더경로>git --version
git version 2.33.1.windows.1
```

<br>

- ‘git config --list’ 명령어를 통해 현재 설정된 Git 설정을 확인할 수 있다.

```bash
C:\폴더경로>git --version
git version 2.33.1.windows.1
```

<br>

- ‘git config --global -e’ 명령어를 통해 파일을 읽고 쓸 수 있다.특정 사용자의 모든 저장소 설정에 적용된다.

```bash
C:\폴더경로>git config --global user.name "깃 이름"

C:\폴더경로>git config --global user.email "사용자 이메일"

```

git 환결설정에 사용자정보를 등록한다

<br>

- Git은 커밋할 때 자동으로 CRLF를 LF로 변환해주고 반대로 Checkout 할 때 LF를 CRLF로 변환해 주는 기능이 있다. `core.autocrlf` 설정으로 이 기능을 켤 수 있다. Windows에서 이 값을 true로 설정하면 Checkout 할 때 LF 문자가 CRLF 문자로 변환된다.

```bash
C:\폴더경로>git config --global core.autocrlf true
```

<br>

## Git 공부 포인트

<br>

- [깃 공식 홈페이지](https://git-scm.com/docs)에서 Git에서 사용하는 모든 멍령어를 찾아 볼 수있다.

![그림1](/assets/img/blog/study/git/study-git-point01.png)

<br>

- 그리고 해당 명령어를 클릭하면 여러 옵션들도 확인 할 수 있다.

![그림1](/assets/img/blog/study/git/study-git-point02.png)

<br>

## Git 초기화/ 삭제하기

<br>

- git관리 할 디렉토리에 들어가서 ‘git init’명령어를 사용하여 초기화한다.

```bash
C:\폴더경로>cd git

C:\폴더경로\git>git init

C:\폴더경로\git (master)> //master가 생성된 것을 확인 할 수 있다.
```

<br>

- ‘rm -rf .git ’명령어를 사용하여 삭제한다.

```bash
C:\폴더경로>rm -rf .git

C:\폴더경로\git> //master가 없어진 것을 확인 할 수 있다.
```

<br>

## Git 명령어 단축키

<br>

- “git config --global alias.’원하는 단축키’ ‘Git명령어’]”를 사용하여 자주 사용하는 Git명령어에 대해서 단축키 설정이 가능하다.

```bash
C:\폴더경로\git (master)>git config --global alias.st status

C:\폴더경로\git (master)>git st
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

<br>

<aside>
💡 git config —h:해당 명령어에 대한 속성값을 확인 할 수 있다.

</aside>

 <br>

## Git 중요 컨셉(workflow)

<br>

- working directory
    - untracked
    - tracked
        - unmodified
        - modified

- staging area
- .git directory
- remote

<br>

## Git add

<br>

- untracked 상태

```bash
C:\폴더경로\git (master)
λ git st
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.txt
        b.txt
        c.txt
nothing added to commit but untracked files present (use "git add" to track)
```

<br>

- staging area 상태

```bash
C:\폴더경로\git (master)
λ git add *.txt

C:\develp\git-study\git (master)
λ git st
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
        new file:   b.txt
        new file:   c.txt
```

‘git add’ 하여 tracked된 상태를 확인 할 수 있다.

<br>

- tracked이며 modified상태

```bash
C:\폴더경로\git (master)
λ echo ellie >>a.txt

C:\폴더경로\git (master)
λ git st
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
        new file:   b.txt
        new file:   c.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt
```

‘git add’한 a.txt파일을 수정하여 ‘git status’로 확인해보면, tracked이며 modified된 상태를 확인 할 수 있다.

<br>

- staging area 상태에서 untracked로 되돌리기

```bash
C:\폴더경로\git (master)
λ git rm --cached *
rm 'a.txt'
rm 'b.txt'
rm 'c.txt'

C:\폴더경로\git (master)
λ git st
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.txt
        b.txt
        c.txt

nothing added to commit but untracked files present (use "git add" to track)
```

‘git rm —cached 파일명’명령어로 staging area상태에 있는 파일을 다시 untracked로 되돌릴 수 있다.

<br>

## Git ignore

<br>

Git이나 Git hub에 추가하고 싶지 않은 파일들을 따로 설정할 수 있다.

<br>

- .gitignore 파일에 추가

```bash
C:\폴더경로\git (master)
λ git st
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   c.txt
        new file:   style.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        log.log

C:\폴더경로\git (master)
λ echo *.log > .gitignore

C:\폴더경로\git (master)
λ ls -al
total 12
drwxr-xr-x 1 sjy19 197609  0  1월 12 19:10 ./
drwxr-xr-x 1 sjy19 197609  0  1월 11 19:15 ../
drwxr-xr-x 1 sjy19 197609  0  1월 12 19:10 .git/
-rw-r--r-- 1 sjy19 197609  8  1월 12 19:10 .gitignore
-rw-r--r-- 1 sjy19 197609 15  1월 12 17:05 c.txt
-rw-r--r-- 1 sjy19 197609  6  1월 12 19:05 log.log
-rw-r--r-- 1 sjy19 197609 10  1월 12 19:05 style.css

C:\폴더경로\git (master)
λ git st
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   c.txt
        new file:   style.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
```

untracked된 Git과 Github에 올리고 싶지않은 log.log파일을 확인하고, .gitignore 파일에 *.log를 추가함으로써 log.log파일이 .gitignore로 대체된 것을 확인 할 수있다. 

<br>

## Git diff

<br>

- git diff

working directory에 있는 파일을 정확하게 비교해 볼 수있다. 

```bash
C:\폴더경로\git (master)
λ echo add >> c.txt

C:\폴더경로\git (master)
λ git st
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   c.txt
        new file:   style.css

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   c.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

C:\폴더경로\git (master)
λ git diff
diff --git a/c.txt b/c.txt
index 12a8798..311c32c 100644
--- a/c.txt
+++ b/c.txt
@@ -1 +1,2 @@
 hello world!
+add

```

staging area에 있는 c.txt파일을 수정한 후에, ‘git diff’명령어를 이용하여 파일을 비교해볼 수  있다.

<br>

- git diff --staged

staging area에 있는 파일을 비교해볼 수 있다.

```bash
C:\폴더경로\git (master)
λ git diff --staged
diff --git a/c.txt b/c.txt
new file mode 100644
index 0000000..12a8798
--- /dev/null
+++ b/c.txt
@@ -0,0 +1 @@
+hello world!
diff --git a/style.css b/style.css
new file mode 100644
index 0000000..65699e6
--- /dev/null
+++ b/style.css
@@ -0,0 +1 @@
+styling
```

<br>

<aside>
💡 git diff --cached : git diff --staged와 똑같은 내용을 출력

</aside>

<br>

👍!꿀팁

- terminal로 비교하는게 어렵다면, 우리가 원하는 UI로 연결하여 비교해 볼 수 있다.

<br>

’git config --global -e’명령어로 열고,**[diff]** 와 **[difftool “원하는 UI”]**를 추가한다.

```bash
[diff]
	tool = vscode
[difftool "vscode"]
	cmd = code --wait --diff $LOCAL $REMOTE
```

<br>

‘git difftool’명령어로 원하는 UI로 working directory에 있는 파일을 비교할 수 있다.

![그림3](/assets/img/blog/study/git/study-git-diff01.png)

<br>

‘git difftool --staged’명령어로 원하는 UI로 staging area에 있는 파일을 비교할 수 있다.

c.text파일

![그림4](/assets/img/blog/study/git/study-git-diff02.png)

style.css파일

![그림5](/assets/img/blog/study/git/study-git-diff03.png)
<br>

## Git commit

<br>

- ‘git commit’ 명령어로  commit을 한다

```bash
C:\폴더경로\git (master)
λ git commit
[master (root-commit) b87715f] Title
 2 files changed, 2 insertions(+)
 create mode 100644 c.txt
 create mode 100644 style.css
```

‘gt commit’할대 아무런 속성을 하지않으면 에디터를 열고 메시지를 작성하고 저장하고 닫는 번거러움이 발생한다.

그래서 속성값을 줘서 바로 메시지를 입력하고 commit을 할 수 있다.

```bash
C:\폴더경로\git (master)
λ git commit -am "third commit"
[master 0c36fbd] third commit
 1 file changed, 1 insertion(+)
```

-a : all의 의미로 모든것을 선택하겠다,

-m :message의 의미로 메시지를 값을 지정한다.

<br>

- ‘git log’명령어로 git의 모든 history정보를 확인할 수 있다.

```bash
C:\폴더경로\git (master)
λ git log
commit 0c36fbd1f7d43eac2a535c05466ea943acb24d97 (HEAD -> master)
Author: Jiyong Sim <sjy19910222@gmail.com>
Date:   Thu Jan 13 19:18:07 2022 +0900

    third commit

commit e233416842ba083fb68f2910018ba36ef38a0ff6
Author: Jiyong Sim <sjy19910222@gmail.com>
Date:   Thu Jan 13 19:17:09 2022 +0900

    second commit

commit b87715fb41bfa385be2782764b4a0a78e7ded25a
Author: Jiyong Sim <sjy19910222@gmail.com>
Date:   Thu Jan 13 19:14:23 2022 +0900

    Title

    Description
```

<br>

<aside>
💡 커밋 팁!!!

</aside>

- 기능별로 작은 단위로 나누어 만들어 나가는것이 중요!
- 무분별할 commit보다는 의미있는 commit을 해야한다.
- commit의 메세지는 보통 현재형과 동사형으로 만든다.(ex. Init, Add, Fix등)
- 고친내용을 commit할때는, 고친내용만 commit해야한다. (다른 기능을 고치거나 건드는 행위는 금지❌)
- 너무 크거나 너무 작은 commit은 금지 ❌