---
title: "4. Docker Image 만들기"
date: 2025-01-05 00:00:00 +/-TTTT
categories: [Main]
tags: [Docker]
toc: true
---

## 가이드

[0. Docker 시작하기](../docker-00)

---

Docker를 사용하면 Docker Hub에서 이미지를 가져와 바로 사용할 수 있습니다. 하지만 때때로 자신만의 환경을 갖춘 이미지를 직접 만들어야 할 경우가 있습니다.

Docker 이미지를 만드는 방법은 크게 두 가지가 있습니다:

## 1. commit 방식으로 이미지 만들기

현재 실행 중인 컨테이너를 이미지로 저장할 수 있습니다.

```shell
# python-base 컨테이너를 만들고 실행 합니다.
docker run -it --name python-base python:alpine sh

# 컨테이너에 TestPython.py 파일을 생성 합니다.
/ # echo "print(\"Test\")" > TestPython.py

# 컨테이너에서 나갑니다.
/ # exit

# python-base 컨테이너를 기반으로 python-custom 이미지를 만듭니다.
docker commit python-base python-custom

# python-custom 이미지를 기반으로 python-coustom-container 컨테이너를 만듭니다.
docker run -it --name python-coustom-container python-custom sh

# TestPython.py가 추가된체 실행된 컨테이너를 확인할 수 있습니다.
/ # ls
TestPython.py  etc     media   proc    sbin    tmp    ...
```

1. python:alpine 기반 컨테이너를 실행한 후, 내부에서 `TestPython.py` 파일을 생성합니다.
2. 컨테이너를 commit 하면 새로운 이미지가 만들어 집니다.
3. 만들어진 이미지를 컨테이너로 실행하면 `TestPython.py` 파일이 시작부터 존재하는것을 확인할 수 있습니다.

## 2. Dockerfile 방식으로 이미지 만들기

Dockerfile을 작성하여 이미지를 빌드할 수 있습니다.

### 도커 파일 예시

```Dockerfile
# 도커 허브의 python:alpine 이미지를 기반으로 이미지를 생성 합니다.
FROM python:alpine

# pythonExample 디렉토리를 만들고 이동 합니다.
WORKDIR /pythonExample

# firstPython.py 파일을 만듭니다.
# 이미지가 만들어 질때 실행 됩니다.
RUN echo "print(\"Hello Python!\")" > firstPython.py

# 호스트에 있는 secondPython.py 파일을 이미지에 복사 합니다.
COPY ["secondPython.py", "."]

# 이미지가 컨테이너로 실행될 때 명령어가 실행 됩니다.
# docker run 에서 커멘드 옵션이 추가되면 아래 구문은 무시 됩니다.
CMD ["sh", "-c", "python3 firstPython.py && python3 secondPython.py"]
```

```shell
docker build -t test-python-image .
```

`docker build` 명렁어로 Dockerfile을 이미지로 빌드 합니다.

- `-t` 옵션은 이미지의 이름을 지정할 수 있습니다.
- `.` 은 Dockerfile의 경로 입니다.
- 더 자세한 Dockerfile의 사용방법은 [Dockerfile 공식 메뉴얼](https://docs.docker.com/reference/dockerfile/) 을 참고 하세요.

빌드에 성공하면 이미지를 컨테이너로 만들고 실행 합니다. 

```shell
docker run --name test-python-container test-python-image
```

### 실행 결과

```shell
(base) DockerTest % docker build -t test-python-image .

[+] Building 1.2s (9/9) FINISHED                                          
 => [internal] load build definition from Dockerfile                      
 => => transferring dockerfile: 328B                                      

...

 => CACHED [2/4] WORKDIR /pythonExample
 
 => [3/4] RUN echo "print("Hello Python!")" > firstPython.py
 
 => [4/4] COPY [secondPython.py, .]

...

(base) DockerTest % docker run --name test-python-container test-python-image

Hello Python!
Hello Python!!
```

- `test-python-image` 가 정상적으로 만들어 졌습니다.
- **Dockerfile** 에 명시한 내용이 순차적으로 실행되는것을 확인할 수 있습니다.
- `docker run` 으로 컨테이너를 만들고 실행하면 `firstPython.py`, `secondPython.py` 가 순차적으로 실행되는 것을 확인할 수 있습니다.
