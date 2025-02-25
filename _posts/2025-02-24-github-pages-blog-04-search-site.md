---
title: "4. 검색 사이트에 블로그 등록하기"
date: 2025-02-24 00:00:00 +/-TTTT
categories: [Main, Blog]
tags: [Blog, GitHub]
toc: true
---

## 가이드

[0. GitHub Pages 를 이용해 블로그 운영하기](../github-pages-blog-00)

---

## 네이버 등록 하기

[네이버 서치 어드바이저](https://searchadvisor.naver.com/)에서 사이트를 등록할 수 있습니다.

1. `웹마스터 도구 사용하기`를 클릭 합니다.
2. 블로그의 메인 주소를 등록 합니다.
3. `HTML 파일 업로드` 또는 `HTML 태그` 방식으로 소유 확인을 진행할 수 있습니다. 여기서는 `HTML 태그` 방식을 사용합니다.
	
   ```html
   <meta name="naver-site-verification" content="인증키" />
   ```
	
4. 위의 메타 태그를 블로그의 헤더에 추가합니다.
5. 네이버 서치 어드바이저 페이지로 돌아가 `소유 확인`을 클릭합니다.
6. 인증이 완료되면, 좌측 메뉴에서 `요청` → `사이트맵 제출`로 이동합니다.
7. Chirpy 테마를 사용하는 경우, 자동으로 생성된 `블로그주소/sitemap.xml`을 입력하여 등록합니다.

### 문제1: 메인 주소가 네이버 서치 어드바이저에 등록되지 않는 문제

GitHub Pages를 이용하면 기본 도메인이 `{깃허브 아이디}.github.io/{저장소 이름}` 형식으로 제공됩니다. 그러나 네이버 서치 어드바이저에서는 `/{저장소 이름}`이 포함된 URL을 등록할 수 없습니다.

#### 해결 방법

GitHub Pages의 기본 저장소 이름을 `{깃허브 아이디}.github.io`로 변경하면 `{깃허브 아이디}.github.io` 주소를 사용할 수 있습니다. 

> 참고 : Chirpy 테마 사용시 \_config.yml에 baseurl 값을 "" 이렇게 바꿔줘야 합니다.
{: .prompt-info }

### 문제2: Chirpy Starter 테마에서 헤더 수정이 어려운 문제

Chirpy 테마에서는 `_includes/head.html` 파일을 수정해야 하지만, Chirpy Starter 테마에는 `_includes` 폴더가 없습니다.

#### 해결 방법

1. [Chirpy 테마 GitHub 저장소](https://github.com/cotes2020/jekyll-theme-chirpy)에서 `_includes/head.html` 파일을 다운로드합니다.
2. 블로그 프로젝트 내에 `_includes` 폴더를 생성하고, 해당 폴더에 `head.html` 파일을 추가합니다.
3. `head.html` 파일을 열어 다음 메타 태그를 추가합니다.
	
   ```html
   <meta name="naver-site-verification" content="인증키" />
   ```

---

## 다음(Daum) 등록 하기

[다음 검색 등록](https://register.search.daum.net/index.daum)에서 사이트를 등록할 수 있습니다.

1. 등록 탭에서 `블로그 등록`을 선택 합니다.
2. 블로그 URL을 입력하고 `확인`을 클릭합니다.
3. 이용 약관을 확인한 수 `확인`을 클릭합니다.
4. 이메일을 입력 하고 `확인`을 클릭합니다.

---

## 구글 등록 하기

[구글 서치 콘솔](https://search.google.com/search-console?hl=ko)에서 사이트를 등록할 수 있습니다.

1. 우측 메뉴에서 `속성 추가`를 선택합니다.
2. 속성 유형 선택 팝업에서 `URL 접두어`에 블로그 URL을 입력합니다.
3. 소유권 확인 팝업에서 `HTML 태그` 방식을 선택합니다.
    
    ```html
    <meta name="google-site-verification" content="인증키" />
    ```
    
4. `인증키`를 복사합니다.
5. 블로그 프로젝트의 `_config.yml` 파일을 열고 다음과 같이 입력합니다.
    
    ```yml
    webmaster_verifications:
      google: "인증키"
    ```
    
    (이렇게 설정하면 `head` 태그에 자동으로 추가됩니다.)
    
6. 변경 사항을 배포한 후, 구글 서치 콘솔에서 `확인` 버튼을 클릭합니다.
7. 등록이 완료되면 좌측 메뉴에서 `Sitemaps`를 선택합니다.
8. `블로그주소/sitemap.xml`을 등록합니다. (등록 후 `가져올 수 없음` 상태일 수 있지만, 저는 다음날 `성공`으로 변경 되었습니다.)

---

## 빙 등록 하기

[빙 웹마스터 도구](https://www.bing.com/webmasters/about?mkt=ko-kr)에서 사이트를 등록할 수 있습니다.

1. `시작하기` 버튼을 클릭합니다.
2. `사이트 수동 추가`에 블로그 URL을 입력합니다.
3. 사이트 추가 및 인증 단계에서 `HTML 메타 태그` 방식을 선택합니다.
4. 블로그 프로젝트의 `_config.yml` 파일을 열고 다음과 같이 입력합니다.
    
    ```yml
    webmaster_verifications:
      bing: "인증키"
    ```
    
    (이렇게 설정하면 `head` 태그에 자동으로 추가됩니다.)
    
5. 변경 사항을 배포한 후, 빙 웹마스터 도구에서 `확인` 버튼을 클릭합니다.
6. 등록이 완료되면 좌측 메뉴에서 `사이트맵`을 선택합니다.
7. `사이트맵 제출` 버튼을 클릭합니다.
8. `블로그주소/sitemap.xml`을 등록합니다. (등록 후 `처리중` 상태일 수 있지만, 저는 다음날 `성공`으로 변경 되었습니다.)

