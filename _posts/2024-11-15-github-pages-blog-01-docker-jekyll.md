---
title: "1. Docker로 Jekyll 로컬 서버 구축하기"
date: 2024-11-15 00:00:00 +/-TTTT
categories: [Main, Blog]
tags: [Blog, GitHub]
toc: true
---

## 가이드

[0. GitHub Pages 를 이용해 블로그 운영하기](../github-pages-blog-00)

---

## Jekyll이란?

Jekyll은 **정적 사이트 생성기(Static Site Generator, SSG)** 로, 마크다운(Markdown) 파일을 HTML로 변환하여 정적 웹사이트(블로그, 문서 사이트 등)를 쉽게 만들 수 있도록 도와주는 도구입니다.

GitHub Pages는 Jekyll을 기본적으로 지원하기 때문에, 마크다운 파일을 푸시하는 것만으로 HTML 기반의 웹 페이지를 생성할 수 있습니다. 하지만 배포 전에 **로컬 환경에서 미리 확인하고 싶다면** Jekyll을 직접 실행해보는 것이 좋습니다. 이번 글에서는 **Docker를 이용해 로컬 Jekyll 환경을 구축하는 방법**을 알아보겠습니다.

---

## 1. GitHub Pages에서 지원하는 Jekyll 버전 확인

GitHub Pages에서 사용하는 Jekyll의 버전은 공식 문서를 통해 확인할 수 있습니다.

🔗 [GitHub Pages - Dependency versions](https://pages.github.com/versions/)

📌 2025년 2월 12일 기준 지원 버전:

- **Ruby**: 3.3.4 (Jekyll은 Ruby 기반이므로 설치 필요)
- **Jekyll**: 3.10.0

이제 이 버전에 맞춰 Docker 환경을 세팅해보겠습니다.

---

## 2. Docker 이미지 만들기

Docker Hub에는 **Jekyll이 포함된 공식 이미지**가 없기 때문에, **Ruby 공식 이미지**를 기반으로 직접 Dockerfile을 작성해야 합니다.

### 2.1 Ruby 공식 이미지 확인

🔗 [Ruby 공식 이미지 (Docker Hub)](https://hub.docker.com/_/ruby/tags)  
이곳에서 최신 Ruby 3.3.4 버전을 선택합니다.

### 2.2 Dockerfile 작성

```Dockerfile
FROM ruby:3.3.4 

# RubyGems 버전 업데이트 
RUN gem update --system 3.6.2 

# Jekyll 3.10.0 버전 설치 
RUN gem install jekyll -v 3.10.0 

# Jekyll 프로젝트를 저장할 디렉토리 생성 
RUN mkdir my_jekyll_page
```

- `gem update --system 3.6.2` → 루비의 패키지 관리도구인 Gem을 업데이트
- `gem install jekyll -v 3.10.0` → GitHub Pages에서 지원하는 jekyll 설치
- `mkdir my_jekyll_page` → 마크다운 파일을 저장할 디렉토리 생성

### 2.3 Docker 이미지 빌드

이제 Docker 이미지를 생성합니다.

```shell
docker build -t jekyll-image .;
```

- `-t jekyll-image` → 생성할 이미지 이름을 `jekyll-image`로 지정

---

## 3. Docker 컨테이너 실행

Docker 컨테이너를 실행하여 Jekyll 서버를 띄웁니다.

```shell
docker run --name jekyll-server -it -p 4000:4000 -v $(pwd)/docs:/my_jekyll_page jekyll-image /bin/bash -c "[ ! \"\$(ls -A /my_jekyll_page)\" ] && jekyll new my_jekyll_page; cd my_jekyll_page; bundle install; bundle exec jekyll serve --host 0.0.0.0";
```

### 3.1 옵션 설명

- `--name jekyll-server` → 컨테이너 이름을 `jekyll-server`로 설정
- `-it` → 인터랙티브 모드로 실행하여 서버가 계속 동작하도록 설정
- `-p 4000:4000` → 컨테이너의 4000번 포트를 호스트의 4000번 포트와 연결
- `-v $(pwd)/docs:/my_jekyll_page` → 호스트의 `docs` 폴더를 컨테이너 내부 `/my_jekyll_page` 폴더와 마운트

### 3.2 실행되는 명령어

컨테이너 내에서 실행되는 명령어를 풀어보면 다음과 같습니다.

```shell
# Jekyll 프로젝트 생성 (폴더가 비어있는 경우)
[ ! "$(ls -A /my_jekyll_page)" ] && 
jekyll new my_jekyll_page; # 새 프로젝트(사이트) 생성
cd my_jekyll_page; 
bundle install; # 프로젝트에서 필요한 번들 설치
bundle exec jekyll serve --host 0.0.0.0 # jekyll 실행
```

- jekyll 프로젝트 폴더에는 Gemfile이 있습니다. Gemfile에 명시된 패키지를 `bundle install;`을 이용해 설치 합니다.
- 도커 환경에서는 `--host 0.0.0.0` 옵션을 추가하지 않으면 **호스트에서 localhost:4000으로 접속할 수 없습니다.**

---

## 4. 테스트 페이지 작성

이제 **마크다운 파일을 작성하고, 웹에서 확인**해봅니다.

1. **호스트의 `docs` 폴더에 마크다운 파일 작성**

```shell
echo "# Hello Jekyll" > docs/index.md
```

2. **웹 브라우저에서 확인**

- `http://localhost:4000/` → 기본 페이지 (`index.md`가 자동 적용됨)
- `http://localhost:4000/파일명` → 특정 마크다운 페이지 확인 (확장자 제외)

---

이제 로컬 환경에서 **Jekyll을 이용한 GitHub Pages 블로그 운영**을 시작할 준비가 완료되었습니다.

다음 편에서는 **GitHub Pages에 배포하는 과정**을 알아보겠습니다.
