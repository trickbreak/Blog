---
title: "3. Git CLI - 충돌"
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

## 1. 충돌 시 작업 취소하기

### 옵션
```shell
--abort
```

### 사용 예시

```shell
git cherry-pick --abort  # 체리픽을 시작하기 전 상태로 되돌립니다. 
git merge --abort        # 머지를 시작하기 전 상태로 되돌립니다. 
git rebase --abort       # 리베이스를 시작하기 전 상태로 되돌립니다.
```

## 2. 충돌 해결 후 작업 계속 진행하기

### 옵션

```shell
--continue
```

### 사용 예시

```shell
git cherry-pick --continue  # 충돌을 해결한 후 체리픽을 계속 진행합니다. 
git merge --continue        # 충돌을 해결한 후 머지를 계속 진행합니다. 
git rebase --continue       # 충돌을 해결한 후 리베이스를 계속 진행합니다.
```
