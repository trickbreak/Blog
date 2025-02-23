---
title: "2. GitHub Pages에 배포"
date: 2024-11-22 00:00:00 +/-TTTT
categories: [Main]
tags: [Blog, GitHub]
toc: true
---

## 가이드

[0. GitHub Pages 를 이용해 블로그 운영하기](../github-pages-blog-00)

---

이제 로컬에서 만든 Jekyll 사이트를 GitHub Pages에 배포해보겠습니다.

## 1. GitHub에 프로젝트 업로드

먼저, Jekyll 프로젝트를 GitHub 저장소에 업로드해야 합니다.

### 1.1 GitHub 저장소 생성

1. GitHub에 로그인한 후, **새 저장소(New repository)** 를 생성합니다.
2. **저장소를 Public(공개)로 설정**합니다.
    
    > (Private 저장소를 GitHub Pages로 게시하려면 GitHub Enterprise 를 사용해야 합니다.)
    

### 1.2 프로젝트를 GitHub에 업로드

이전에 **Docker를 이용해 만든 Jekyll 프로젝트**를 GitHub에 올립니다. 로컬에서 만든 docs 폴더가 반드시 포함 되어야 합니다.

## 2. GitHub Pages 설정

이제 GitHub Pages를 활성화하여 사이트를 배포해보겠습니다.

### 2.1 GitHub Pages 활성화

1. GitHub 저장소 페이지로 이동합니다.
2. **Settings** 탭을 클릭합니다.
3. 왼쪽 메뉴에서 **Pages**를 선택합니다.
4. **Branch 설정**:
    - 기본적으로 `None`으로 되어 있는 브랜치를, **Jekyll 프로젝트가 업로드된 브랜치**로 변경합니다.
    - 보통 `main` 브랜치를 선택합니다.

### 2.2 사이트 루트 폴더 설정

- 만약 **저장소의 루트 디렉터리에 Jekyll 프로젝트가 있다면** 기본 경로를 사용합니다.
- 만약 **`docs/` 폴더가 프로젝트를 업로드했다면**, **배포 경로를 `/docs`로 설정**해야 합니다.
- `docs/` 폴더가 아닌 docs/ 있는 파일을 저장소에 업로드 했다면 `/root`로 설정하면 됩니다.

### 2.3 배포 완료

1. 설정이 완료되었으면 **Save** 버튼을 클릭합니다.
2. GitHub Pages가 자동으로 빌드되고, 잠시 후 사이트가 배포됩니다.
3. 아래 주소로 접속하여 사이트가 정상적으로 표시되는지 확인합니다.

```
https://깃허브아이디.github.io/저장소이름/
```
