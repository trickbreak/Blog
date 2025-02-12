---
title: "4. Git CLI - 원격 저장소 관리"
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

## 1. 원격 저장소 연결

### 명령어

```shell
git remote add origin <원격 저장소 URL>
```

### 설명

- 로컬 저장소와 원격 저장소를 연결합니다.
- `origin`은 기본 원격 저장소의 이름으로, 필요에 따라 다른 이름을 사용할 수도 있습니다.
- 연결 후 `git remote -v` 명령어로 원격 저장소 URL을 확인할 수 있습니다.

---

## 2. 원격 저장소에서 복제 (Clone)

### 명령어

```shell
git clone <원격 저장소 URL>
```

### 설명

- 원격 저장소의 내용을 로컬 저장소로 복제합니다.

---

## 3. 원격 저장소에 업로드 (Push)

### 명령어

```shell
git push origin <브랜치 이름>
```

### 설명

- 로컬 브랜치의 변경 사항을 원격 저장소로 업로드합니다. (`origin`은 원격 저장소의 이름)
- 해당 브랜치를 처음으로 푸시할 때는 `-u` 옵션을 사용해 로컬 브랜치와 원격 브랜치를 연결해 주어야 합니다. (한 번 연결을 설정하면 이후에는 `-u` 옵션 없이도 푸시할 수 있습니다.)
	- 예: `git push -u origin develop`
- `-f` 옵션을 사용하면 로컬 저장소의 상태를 강제로 원격 저장소에 반영합니다. 이를 통해 로컬에서 `git reset`을 사용해 커밋 내역을 수정한 후, `git push -f origin master`와 같이 명령어를 실행하여 원격 저장소의 커밋 내역도 덮어쓸 수 있습니다. 단, 강제로 덮어쓰는 작업이므로 원격 저장소의 기존 커밋 기록이 손실될 수 있어 주의해야 합니다.

---

## 4. 원격 저장소 상태 새로고침 (Fetch)

### 명령어

```shell
git fetch
```

### 설명

- 원격 저장소의 변경 사항을 로컬로 다운로드하지만, 자동으로 병합하지는 않습니다.
- 다운로드 받은 변경 사항을 확인 후 필요 시 `git merge` 또는 `git rebase` 등을 통해 로컬 브랜치에 반영할 수 있습니다.

---

## 5. 원격 저장소에서 변경 사항 가져오기 (Pull)

### 명령어

```shell
git pull origin <브랜치 이름>
```

### 설명

- 원격 저장소의 최신 변경 사항을 가져와서 로컬 브랜치에 병합합니다.
- `git pull`은 내부적으로 `git fetch`와 `git merge`를 연달아 실행하는 것과 동일합니다.

---
