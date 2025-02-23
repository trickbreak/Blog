---
title: "유니티 커스텀 패키지 제작 및 배포"
date: 2024-01-16 00:00:00 +/-TTTT
categories: [Main, Unity]
tags: [Unity]
toc: true
---

> Unity6 LTS 버전 기준 입니다.
{: .prompt-info }

유니티 프로젝트를 진행하다 보면 공통 기능을 모듈화하여 관리하는 경우가 많습니다. 이러한 기능을 **Assets 폴더** 내부에서 개별 폴더로 관리할 수도 있지만, **유니티 패키지**로 만들어 관리하면 더욱 효율적입니다.

유니티 패키지를 활용하면 다음과 같은 장점이 있습니다:

- **재사용성**: 여러 프로젝트에서 동일한 패키지를 활용할 수 있습니다.
- **협업 용이**: 팀원 간 패키지를 쉽게 공유하고 일관된 개발 환경 유지할 수 있습니다.
- **버전 관리**: 패키지별로 버전을 체계적으로 관리하여 업데이트 및 롤백이 용이 합니다.
- **의존성 관리**: 특정 패키지가 다른 패키지에 의존하는 경우, **유니티 패키지 매니저(Package Manager)** 가 이를 자동으로 처리 합니다.

유니티 패키지를 적극 활용하면 프로젝트 구조를 깔끔하게 유지하고, 유지보수 및 확장성을 높일 수 있습니다.

## 1. 커스텀 패키지 폴더 구조

```plaintext
<package-root>
  ├── package.json
  ├── README.md
  ├── CHANGELOG.md
  ├── LICENSE.md
  ├── Third Party Notices.md
  ├── Editor
  │   ├── <company-name>.<package-name>.Editor.asmdef
  │   └── EditorExample.cs
  ├── Runtime
  │   ├── <company-name>.<package-name>.asmdef
  │   └── RuntimeExample.cs
  ├── Tests
  │   ├── Editor
  │   │   ├── <company-name>.<package-name>.Editor.Tests.asmdef
  │   │   └── EditorExampleTest.cs
  │   └── Runtime
  │        ├── <company-name>.<package-name>.Tests.asmdef
  │        └── RuntimeExampleTest.cs
  ├── Samples~
  │        ├── SampleFolder1
  │        ├── SampleFolder2
  │        └── ...
  └── Documentation~
       └── <package-name>.md
```

- `package.json`: 패키지의 메타데이터를 포함하는 파일
- `README.md`: 패키지 사용법을 설명하는 파일
- `CHANGELOG.md`: 패키지의 변경 사항을 기록하는 파일
- `LICENSE.md`: 패키지의 라이선스 정보를 포함하는 파일
- `Third Party Notices.md`: 패키지가 포함하는 서드파티 라이브러리 목록
- `Editor/`: 유니티 에디터 전용 스크립트를 포함하는 폴더
- `Runtime/`: 실행 중 필요한 스크립트 및 에셋을 포함하는 폴더
- `Tests/`: 단위 테스트를 포함하는 폴더
- `Samples~/`: 샘플 예제를 포함하는 폴더
- `Documentation~/`: 추가적인 문서를 포함하는 폴더

---

## 2. package.json 설정

```json
{
  "name": "com.mycompany.mypackage",
  "version": "1.0.0",
  "displayName": "My Custom Package",
  "description": "This is my custom Unity package.",
  "unity": "2021.3",
  "author": {
    "name": "My Company",
    "email": "support@mycompany.com",
    "url": "https://mycompany.com"
  },
  "dependencies": {
    "com.unity.textmeshpro": "3.0.6"
  }
}
```

- `name`: 패키지의 고유한 이름 (역방향 도메인 형식 권장)
- `version`: 패키지의 버전 정보 (SemVer 사용)
- `displayName`: 패키지의 표시 이름
- `description`: 패키지 설명
- `unity`: 패키지가 지원하는 최소 유니티 버전
- `author`: 제작자 정보
- `dependencies`: 패키지가 의존하는 다른 패키지 목록

---

## 3. 패키지 설치

### 1) 디스크에서 패키지 설치

1. 유니티 프로젝트에서 유니티 패키지 매니저를 실행합니다.
2. 패키지 매니저 좌측 상단에서 `+`을 눌러 `디스크에서 패키지 설치`를 선택합니다.
3. 커스텀 패키지의 경로를 설정하면 프로젝트에 패키지가 추가됩니다.

### 2) Git저장소에서 패키지 설치

1. 유니티 프로젝트에서 유니티 패키지 매니저를 실행합니다.
2. 패키지 매니저 좌측 상단에서 `+`을 눌러 `Git URL에서 패키지 설치`를 선택합니다.
3. Git 저장소 URL을 입력합니다. 저장소에 여러 개의 패키지가 포함되어 있는 경우, GitHub 기준 `https://github.com/{아이디}/{저장소이름}.git?path={package.json 파일이 있는 경로}`와 같은 형식으로 지정할 수 있습니다.

---

## 4. 추가 기능 및 최적화

- **샘플 코드 제공**: `Samples~/` 폴더를 활용하여 사용자가 쉽게 예제 코드를 추가할 수 있도록 합니다.
- **테스트 코드 작성**: `Tests/` 폴더 내에 `Runtime` 및 `Editor` 테스트를 추가하여 품질을 보장합니다.
- **유니티 에디터 확장**: `Editor/` 폴더에 `EditorWindow`, `Custom Inspector` 등을 작성하여 패키지 사용성을 향상시킵니다.
- **문서화**: `README.md`에 패키지 설치 방법, 사용법, 예제 등을 명확하게 정리합니다. 추가적인 문서는 `Documentation~/` 폴더에 포함할 수 있습니다.

---

※ 더 자세한 내용은 유니티 공식 매뉴얼을 확인 하세요. [Unity Documentation](https://docs.unity3d.com/6000.0/Documentation/Manual/CustomPackages.html)

