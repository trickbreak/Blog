---
title: "부록2. docker-compose 사용 방법"
date: 2025-01-28 00:00:00 +/-TTTT
categories: [Main]
tags: [Docker]
toc: true
---

## 가이드

[0. Docker 시작하기](../docker-00)

---

## Docker Compose란?

Docker를 사용하면서 하나의 서비스를 제공하기 위해 여러 컨테이너(예: 웹 서버, DB 서버 등)를 실행하고, 이들 간의 네트워크 연결이나 볼륨 공유 같은 추가 설정을 해야 할 때가 있습니다. 이럴 때 Docker Compose를 사용하면, 복잡한 설정을 하나의 YAML 파일(`docker-compose.yml`)에 정의하고 간편하게 관리할 수 있습니다.

---

## docker-compose.yml 파일

Docker Compose를 사용하려면 먼저 `docker-compose.yml` 파일을 작성해야 합니다. 이 파일에 각 서비스(컨테이너)에 대한 설정을 정의할 수 있습니다. 아래는 예시 파일입니다.

```yaml
version: '3.8'  # Docker Compose 파일 버전

services:

  web:
    build: .               # 현재 디렉토리의 Dockerfile을 사용해 이미지 빌드
    ports:
      - "5000:5000"        # 호스트의 5000번 포트를 컨테이너의 5000번 포트에 매핑
    depends_on:
      - redis              # web 서비스는 redis 서비스가 먼저 실행되어야 함

  redis:
    image: redis:alpine    # Redis 이미지를 사용
```

- **version**: Compose 파일의 버전을 명시합니다.
- **services**: 실행할 개별 컨테이너(서비스)를 정의합니다.
    - **web**:
        - `build`: 현재 디렉토리의 Dockerfile을 기반으로 이미지를 빌드합니다.
        - `ports`: 호스트와 컨테이너 간 포트 매핑을 설정합니다.
        - `depends_on`: 특정 서비스(redis)가 먼저 실행되어야 함을 지정합니다.
    - **redis**:
        - `image`: 미리 빌드된 Redis 이미지를 사용합니다.

---

## Docker Compose 명령어

### 1. 서비스 실행

```shell
docker compose up [옵션]
```

- **기본 동작**: `docker-compose.yml` 파일에 정의된 모든 서비스를 실행합니다.
- **옵션 설명**:
    - `-d`: 컨테이너를 백그라운드에서 실행합니다.
	- `--build`: 코드 수정 후 이미지 재빌드가 필요할 때 사용합니다.

### 2. 서비스 중지 및 정리

```shell
docker compose down
```

- **동작**: 실행 중인 모든 컨테이너를 중지하고, 네트워크 등 관련 자원을 정리합니다.

---

Docker Compose를 사용하면 여러 컨테이너를 하나의 YAML 파일로 정의하고, 네트워크 설정이나 의존성 관리, 볼륨 공유 등을 손쉽게 처리할 수 있습니다. 복잡한 멀티 컨테이너 환경을 간편하게 관리할 수 있어 서비스 개발 및 배포에 매우 유용합니다.
