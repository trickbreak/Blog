---
title: "3. Chirpy 테마 적용 및 배포"
date: 2024-11-29 00:00:00 +/-TTTT
categories: [Main]
tags: [Blog, GitHub]
toc: true
---

## 가이드

[0. GitHub Pages 를 이용해 블로그 운영하기](../github-pages-blog-00)

---

## 1. Jekyll 테마

Jekyll의 기본 테마는 기능이 제한적이기 때문에, 블로그 운영을 위해 **Chirpy 테마**를 적용하는 방법을 알아보겠습니다.

Chirpy 테마는 **포스트 단위 관리, 카테고리 정리, 태그 기능** 등 다양한 기능을 제공하며, 이를 적용하는 과정을 익히면 **다른 Jekyll 테마도 손쉽게 사용할 수 있습니다**.  
(단, 테마마다 적용 방법이 다를 수 있으므로, 해당 테마의 공식 가이드를 참고해야 합니다.)

---

## 2. Jekyll 테마 찾기

Jekyll 테마는 다양한 플랫폼에서 배포되고 있습니다.

- 🔗 [Jamstack Themes](https://jamstackthemes.dev/ssg/jekyll/)
- 🔗 [Jekyll Themes (jekyllthemes.io)](https://jekyllthemes.io/)
- 🔗 [Jekyll Themes (jekyll-themes.com)](https://jekyll-themes.com/)

### 1 Chirpy 테마 적용

🔗 [Chirpy 테마 공식 가이드](https://chirpy.cotes.page/posts/getting-started/)

Chirpy 테마는 **두 가지 방식**으로 사용할 수 있습니다.

1. **[chirpy-starter](https://github.com/cotes2020/chirpy-starter)**
    
    - 간편한 세팅 가능
    - 테마 기능을 직접 수정하기는 어려움
    
2. **[jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)**
    
    - 테마를 직접 수정 가능
    - 초기 세팅이 다소 복잡함

이번에는 **스타터 버전(chirpy-starter)** 을 사용하여 적용해보겠습니다.

---

## 3. Chirpy 스타터 프로젝트 가져오기

1. 저장소를 포크하거나 다운로드하여 로컬 환경에 복사합니다.
2. Visual Studio Code에서 프로젝트를 엽니다.
3. `.devcontainer/devcontainer.json` 파일을 열고 `"postStartCommand": "bundle exec jekyll serve",` 를 추가합니다

```json
{
	"name": "Jekyll",
	"image": "mcr.microsoft.com/devcontainers/jekyll:2-bullseye",
	"onCreateCommand": "git config --global --add safe.directory ${containerWorkspaceFolder}",
	"postCreateCommand": "bash .devcontainer/post-create.sh",
	// 추가한 내용
	"postStartCommand": "bundle exec jekyll serve",
	"customizations": {
		"vscode": {
			"settings": {
				"terminal.integrated.defaultProfile.linux": "zsh"
			},
			"extensions": [
				"killalau.vscode-liquid-snippets",
				"Shopify.theme-check-vscode",
				"timonwong.shellcheck",
				"mkhl.shfmt",
				"EditorConfig.EditorConfig",
				"esbenp.prettier-vscode",
				"stylelint.vscode-stylelint",
				"yzhang.markdown-all-in-one",
				"mhutchie.git-graph"
			]
		}
	}
}
```

>💡 컨테이너가 실행될 때마다 `bundle exec jekyll serve` 명령어가 자동 실행됩니다.

4. 컨테이너 다시 빌드
	
	- 컨테이너를 다시 빌드한 후, 브라우저에서 `localhost:4000`에 접속하여 Chirpy 테마가 적용된 사이트를 확인합니다.

---

## 4. GitHub Pages 배포 전 필수 설정

GitHub Pages에서 정상적으로 동작하려면 `_config.yml` 파일에서 **URL 및 경로 설정**이 필요합니다.

```yml
url: "https://깃허브아이디.github.io" # 저장소 이름 포함 X, 마지막 "/" 제거 
baseurl: "/저장소이름" # 저장소 이름 입력, 첫글자로 "/" 추가
```

- `url` 값에는 **저장소 이름을 포함하지 않아야 합니다.**
- `url` 값의 마지막에 `/`가 붙으면 안 됩니다.

---

## 5. GitHub Pages에 Chirpy 테마 배포

Chirpy 테마는 GitHub Pages는 **GitHub Actions**을 이용하여 배포합니다.

### 1 GitHub Pages 설정

1. **GitHub 저장소(Settings) → Pages로 이동**
2. **Source 변경**
    
    - 기본적으로 `Deploy from a branch` 옵션이 선택되어 있습니다.
    - 이를 `GitHub Actions`로 변경합니다.

### 2 GitHub Actions를 통한 자동 배포

Chirpy 프로젝트에는 **GitHub Actions 배포 설정 파일(`.github/workflows/pages-deploy.yml`)** 이 포함되어 있습니다.  
따라서, **GitHub에 푸시하는 것만으로 자동으로 사이트가 배포됩니다.**

### 3 배포 과정 확인

3. **GitHub 저장소 → Actions 탭 이동**
4. 자동으로 실행된 **빌드 작업이 진행 중인지 확인**
5. 빌드가 완료되면 아래 주소에서 사이트가 배포됩니다.

```
https://깃허브아이디.github.io/저장소이름/
```
