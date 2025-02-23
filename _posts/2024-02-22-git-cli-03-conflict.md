---
title: "3. Git CLI - 충돌"
date: 2024-02-22 00:00:00 +/-TTTT
categories: [Main]
tags: [Git]
toc: true
---

## 가이드

[0. Git CLI 시작하기](../git-cli-00)

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
