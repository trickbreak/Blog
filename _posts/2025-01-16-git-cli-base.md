---
title: "1. Git CLI - 기본 명령어"
date: 2025-01-16 17:00:00 +/-TTTT
categories: [Main]
tags: [Git]
toc: true
---

## 목차

Git CLI 명령어 시리즈 입니다.

[1. Git CLI - 기본 명령어](../git-cli-base)  
[2. Git CLI - rebase](../git-cli-rebase)  
[3. Git CLI - 충돌](../git-cli-conflict)  
[4. Git CLI - 원격 저장소 관리](../git-cli-remote-repository)  

---

## 1. Git 저장소 초기화

### 명령어

```shell
git init .
```

### 설명

- 현재 디렉터리에서 Git 버전 관리를 시작합니다.
- `.git` 폴더가 생성되며, 이 폴더에 Git 관련 데이터가 저장됩니다.

---

## 2. 저장소 상태 확인

### 명령어

```shell
git status
```

### 출력 예시

```shell
git status

On branch develop

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   Test.cs
	renamed:    OldManager.cs -> NewManager.cs

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   TagList.txt
	modified:   Tag.cs

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	Temp.cs
```

### 설명

- **Changes to be committed**: 스테이지에 올려진 변경 사항입니다.
- **Changes not staged for commit**: 수정했지만 아직 스테이지에 추가되지 않은 변경 사항입니다.
- **Untracked files**: Git에서 추적하지 않는 새 파일입니다.

---

## 3. 변경 사항 스테이징

### 명령어

```shell
git add <file>
```

### 설명

- 수정한 파일을 스테이지에 추가하여 커밋할 준비를 합니다.
- 추적되지 않는 파일도 `git add`로 추가할 수 있습니다.
- 이미 스테이지에 올린 파일을 다시 수정한 경우, 변경 사항을 반영하려면 다시 `git add`를 실행해야 합니다.

---

## 4. 스테이지에서 변경 사항 제거

### 명령어

```shell
git restore --staged <file>
```

### 설명

- 스테이지에 올라간 특정 파일을 제거하여 다시 수정된(unstaged) 상태로 되돌립니다.

---

## 5. 로컬 저장소에 추가

### 명령어

```shell
git commit -am "커밋 메시지"
```

### 설명

- `a` 옵션은 워킹 디렉토리에서 발생한 변경사항 중 스테이지에 올라가지 않은 변경 사항을 `add`해서 스테이지에 자동으로 올리는 옵션입니다. (단, 추적되지 않은 파일은 포함되지 않습니다.)
- `m` 옵션은 커밋 메시지를 입력하는 옵션입니다. `m` 옵션 없이 실행하면 기본 편집기에서 커밋 메시지를 입력해야 합니다.

---

## 6. 로그 확인

### 명령어

```shell
git log --oneline --graph --branches
```

### 출력 예시

```shell
git log --oneline --graph --branches

*   f00f4eec7e Merge branch
|\  
| * 97035b61fc 커밋2-2
* | 2c23137092 커밋2-1
|/  
* e13210532b 커밋1
```

### 설명

- 저장소에 커밋된 내역을 확인합니다.
- `--oneline` 옵션은 저장소의 커밋 ID와 타이틀만 보여줍니다.
- `--graph` 옵션은 브랜치 구조를 그래프로 표시합니다.
- `--branches` 옵션은 존재하는 모든 브랜치의 커밋을 표시합니다.

---

## 7. 브랜치 생성

### 명령어

```shell
git branch <브랜치 이름>
```

### 설명

- 현재 HEAD가 가리키고 있는 위치에서 새로운 브랜치를 생성합니다.
- `git branch` 명령어로 브랜치 목록을 확인할 수 있습니다.

---

## 8. 브랜치 변경 (체크아웃)

### 명령어

```shell
git checkout <'브랜치 이름' 또는 '커밋ID'>
```

### 설명

- 해당 브랜치로 이동하여 작업할 수 있습니다.
- 커밋ID를 사용하면 해당 커밋까지 이동하여 작업할 수 있습니다.
- Git 버전 2.23 이후에는 `git switch <브랜치 이름>`을 사용할 수도 있습니다.

---

## 9. 브랜치 병합

### 명령어

```shell
git merge <병합할 브랜치 이름>
```

### 설명

- 현재 HEAD가 가리키는 브랜치에 지정한 브랜치를 병합합니다.

---

## 10. 로컬 저장소의 커밋 내역 취소하기

### 명령어

```shell
git reset <'커밋ID' 또는 'HEAD~숫자'>
```

### 설명

- `커밋ID`를 입력하면 해당 커밋 이후의 모든 변경 사항을 되돌립니다.
- `HEAD~숫자`를 입력하면 현재 HEAD에서 입력된 숫자만큼 커밋을 되돌립니다.
- `--hard` 옵션: 변경 사항을 완전히 삭제합니다.
- `--mixed` 옵션: 변경 사항을 스테이징에서만 제거하고, 작업 디렉토리에 남깁니다.
- `--soft` 옵션: 변경 사항을 스테이징에 그대로 유지합니다.

---

## 11. 커밋 취소 (Revert)

### 명령어

```shell
git revert <커밋 ID>
```

### 설명

- 특정 커밋을 되돌리는 새로운 커밋을 생성합니다.
- reset과 달리 기존 기록을 유지하면서 변경 사항을 취소 할 수 있습니다.

---

## 12. 특정 커밋 적용 (Cherry-Pick)

### 명령어

```shell
git cherry-pick <커밋ID>
```

### 설명

- 특정 커밋을 현재 브랜치에 적용합니다.

---
