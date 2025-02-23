---
title: "2. Git CLI - rebase"
date: 2024-02-15 00:00:00 +/-TTTT
categories: [Main]
tags: [Git]
toc: true
---

## 가이드

[0. Git CLI 시작하기](../git-cli-00)

---

`git rebase` 명령어는 커밋 히스토리를 재구성할 때 사용하는 강력한 도구입니다. 주로 커밋을 정리하거나 병합할 때 사용되며, 브랜치의 기반을 다른 커밋으로 변경할 수 있습니다. 기본적인 사용법을 아래와 같이 설명할 수 있습니다.

## 1. 기본 사용법

```shell
git rebase <base-branch>
```

이 명령어는 현재 브랜치의 변경 사항을 `<base-branch>` 위로 재적용하는 방식으로 작동합니다. 예를 들어, `develop`라는 브랜치에서 작업하고 있을 때, `main` 브랜치에 있던 최신 커밋들을 기반으로 `develop` 브랜치를 업데이트하려면 다음과 같이 입력합니다:

```shell
git log --oneline --graph --branches

* 9d12689 (**main**) Main2 Add
* c2b1bde Main1 Add
| * 49ebaac (HEAD -> develop) Develop2 Add
| * 82c6e32 Develop1 Add
|/  
* 7b6956f Test2 Add
* 924fde2 Test1 Add

git rebase main

Successfully rebased and updated refs/heads/develop.

git log --oneline --graph --branches

* 2ea0d6a (HEAD -> develop) Develop2 Add
* a7e2976 Develop1 Add
* 9d12689 (main) Main2 Add
* c2b1bde Main1 Add
* 7b6956f Test2 Add
* 924fde2 Test1 Add
```

## 2. `interactive`옵션 사용법
    
특정 커밋을 수정하거나 삭제하는 등의 작업을 할 때 `-i` 옵션을 사용하여 **인터랙티브 모드**로 진행할 수 있습니다. 이 방법은 커밋 히스토리를 깔끔하게 정리할 때 유용합니다.
    
```shell
git log --oneline --graph --branches

* 9d12689 (**main**) Main2 Add
* c2b1bde Main1 Add
| * 49ebaac (HEAD -> develop) Develop2 Add
| * 82c6e32 Develop1 Add
|/  
* 7b6956f Test2 Add
* 924fde2 Test1 Add 

git rebase -i main
```

`-i`옵션을 사용하면 아래와 같이 텍스트 편집기 화면이 출력 됩니다.

```shell
pick 82c6e32 Develop1 Add
pick 49ebaac Develop2 Add
  
# Rebase 9d12689..49ebaac onto 9d12689 (2 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

커밋 내역 앞에 붙어있는 명령어를 수정하여 다양한 작업을 수행할 수 있습니다.

예를 들어 `squash`옵션을 사용하면 이전 commit에 병합할 수 있습니다.

```shell
git log --oneline --graph --branches

* 651cbd5 (HEAD -> develop) Develop2 Add
* 38ae394 Develop1 Add
* 9d12689 (main) Main2 Add
* c2b1bde Main1 Add
* 7b6956f Test2 Add
* 924fde2 Test1 Add
```

현재 상태에서 다음 명령어를 실행 합니다. 
(`HADE`에서 4개의 커밋 내역을 인터렉티브 모드로 리베이스)

```shell
git rebase -i HEAD~4
```

텍스트 편집기 화면이 열리고 4개의 커밋 리스트가 표시됩니다.

```shell
pick c2b1bde Main1 Add
pick 9d12689 Main2 Add
pick 38ae394 Develop1 Add
pick 651cbd5 Develop2 Add

# 아래 주석은 무시
```

2~4번째 커밋의 `pick`을 `s`(squash) 로 수정합니다.

```shell
pick c2b1bde Main1 Add
s 9d12689 Main2 Add
s 38ae394 Develop1 Add
s 651cbd5 Develop2 Add
```

편집된 내용을 저장하고 편집기를 종료하면, 다음과 같이 새로운 커밋 메시지를 작성하는 편집기가 열립니다.

```shell
# This is a combination of 4 commits.
# This is the 1st commit message:
  
Main1 Add
  
# This is the commit message #2:
  
Main2 Add
  
# This is the commit message #3:
  
Develop1 Add
  
# This is the commit message #4:
  
Develop2 Add
  
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Sun Feb 2 16:33:33 2025 +0900
#
# interactive rebase in progress; onto 7b6956f
# Last commands done (4 commands done):
#    squash 38ae394 Develop1 Add
#    squash 651cbd5 Develop2 Add
# No commands remaining.
# You are currently rebasing branch 'develop' on '7b6956f'.
#
# Changes to be committed:
#       new file:   Develop1.txt
#       new file:   Develop2.txt
#       new file:   Main1.txt
#       new file:   Main2.txt
#
```

편집기를 종료하면, 아래와 같이 4개의 커밋이 하나의 커밋(`bb56519`)으로 합쳐진 것을 확인할 수 있습니다.

```shell
git log --oneline --graph           

* bb56519 (HEAD -> develop) Main1 Add
* 7b6956f Test2 Add
* 924fde2 Test1 Add
```
