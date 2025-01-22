---
title: "마크다운 확장 문법"
date: 2025-01-20 17:00:00 +/-TTTT
categories: [Main]
tags: [Markdown, Bloging]
toc: true
---

# Markdown 확장 문법

   - 모든 마크다운 애플리케이션에서 확장 구문을 지원하는 것은 아닙니다. 자신이 사용하는 환경에서 테스트가 필요 합니다.


## 테이블

- `|`와 `-`를 사용하여 표를 작성합니다.

- 사용법
  ```markdown
  | 헤더1 | 헤더2 |
  | ----- | ----- |
  | 셀1   | 셀2   |
  ```

- 출력

  | 헤더1 | 헤더2 |
  | ----- | ----- |
  | 셀1   | 셀2   |


## 코드 블록

- \`\`\`(언어정보) 의 형태로 사용합니다.

- 사용법
  ````markdown  
  ```python
  print("Hello, World!")  
  ```
  ````

- 출력
  ```python
  print("Hello, World!")
  ```


## 각주

- 사용법
  ```markdown
  1번 테스트 텍스트 [^1]  
  2번 테스트 텍스트 [^2]  
  테스트 텍스트 [^none]

  [^1]: 1번 테스트 텍스트의 각주 입니다.  
  [^2]: 2번 테스트 텍스트의 각주 입니다.  
  [^none]: 테스트 텍스트의 각주 입니다.
  ```

- 출력  
  1번 테스트 텍스트 [^1]  
  2번 테스트 텍스트 [^2]  
  테스트 텍스트 [^none]

  [^1]: 1번 테스트 텍스트의 각주 입니다.  
  [^2]: 2번 테스트 텍스트의 각주 입니다.  
  [^none]: 테스트 텍스트의 각주 입니다.


## 제목에 커스텀 ID 부여

- 제목에 사용자 지정 ID를 부여할 수 있습니다. 이를 이용해 사용자 지정 ID를 부여 받은 제목의 CSS를 수정할 수 있습니다.

- 사용법
  ```markdown
  ### 커스텀 아이디 제목 {#custom-id}
  ```

- 출력  
### 커스텀 아이디 제목 {#custom-id}

- 다음과 같이 html 구문으로 번역 됩니다.
  ```html
  <h3 id="custom-id">커스텀 아이디 제목\</h3>
  ```


## Definition List
- html에 <dl>, <dt>, <dd> 구문을 표현할때 사용합니다.
- 사용법
  ```markdown
  Name
  : value1
  : value2
  ```

- 출력
  Name
  : value1
  : value2

- 다음과 같이 html 구문으로 번역 됩니다.
  ```html
  <dl>
    <dt>Name</dt>
    <dd>value1</dd>
    <dd>value2</dd>
  </dl>
  ```


## 취소선
- 사용법
  ```markdown
  ~~취소선 테스트~~
  ```

- 출력  
  ~~취소선 테스트~~


## 작업 목록

- 목록으로 구현된 리스트에 체크박스를 추가할 수 있습니다.

- 사용법
  
  ```markdown
  - [x] 방청소 하기
  - [ ] 공과금 내기
  - [ ] 책 읽기
  ```

- 출력
  - [x] 방청소 하기
  - [ ] 공과금 내기
  - [ ] 책 읽기


<!-- ## 이모지

- :이모지 이름: 으로 사용할 수 있습니다.

- [이모지 이름 목록](https://gist.github.com/rxaviers/7360908) 에서 이모지 이름을 찾아 사용할 수 있지만, 이모지 이름은 애플리케이션 마다 다를 수 있습니다.

- 만약 github page에서 이모지를 사용할 수 없는경우

    - Gemfile 에 다음을 추가 합니다.

        ```Gemfile
        group :jekyll_plugins do
	        gem "jemoji", "~> 0.11" # 버전은 상황에 따라 달라질 수 있습니다.
        ```

    - _config.yml 에 다음을 추가 합니다.

        ```yml
        plugins:
            - jemoji
        ```

- 사용법

    ```markdown
    Gone camping! :tent: Be back soon.
    That is so funny! :joy:
    ```

- 출력  
    Gone camping! :tent: Be back soon.  
    That is so funny! :joy: -->


---

※ 더 자세한 마크다운 문법을 확인 하려면 공식 마크다운 가이드를 확인 하세요. [Markdown Guide](https://www.markdownguide.org/extended-syntax/) 
