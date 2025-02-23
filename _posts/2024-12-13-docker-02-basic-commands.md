---
title: "2. Docker 기본 사용 방법"
date: 2024-12-13 00:00:00 +/-TTTT
categories: [Main]
tags: [Docker]
toc: true
---

## 가이드

[0. Docker 시작하기](../docker-00)

---

## Docker Image

### 1) Docker Hub 에서 Docker Image 다운 받기

#### 명령어

```shell
docker pull <이미지 이름>
```

#### 사용 예시

```shell
docker pull python 

Using default tag: latest
latest: Pulling from library/python
4cf0e15c283e: Download complete 
133055fd9ad7: Download complete 
00fcba8cde0d: Download complete 
Digest: sha256:137ae4b9f85671bd912a82a19b6966e2655f73e13579b5d6ad4edbddaaf62a9c
Status: Downloaded newer image for python:latest
docker.io/library/python:latest
```

- tag 를 지정하지 않았기 때문에 `default tag: latest` 를 사용해서 이미지를 다운 받았습니다.
- tag 를 수동으로 지정 할 수도 있습니다. (예 : `docker pull python:3.13.1-alpine3.21`)

### 2) 다운 받은 Docker Image 리스트 확인 하기

#### 명령어

```shell
docker images
```

#### 사용 예시

```shell
docker images

REPOSITORY        TAG          IMAGE ID       CREATED       SIZE
python            latest       137ae4b9f856   2 weeks ago   1.47GB
...
```

### 3) Docker Image 삭제 하기

#### 명령어

```shell
docker rmi <이미지 이름>
```

- 해당 이미지로 실행중인 컨테이너가 있으면, 컨테이너 부터 삭제 후 이미지를 제거 해야 합니다.

---

## Docker Container

### 1) Docker Container 만들고 실행하기

#### 명령어

```shell
docker run [옵션] <이미지 이름 또는 ID> [커맨드]
```

#### 옵션

- `--name` : 실행될 컨테이너의 이름을 지정 합니다. (예 : `docker run --name py python`)
- `-i`, `-t` : 컨테이너가 실행 후 종료되지 않도록 유지 합니다.

#### 사용 예시

```shell
docker run --name py -it python 

Python 3.13.1 (main, Jan 24 2025, 20:47:48) [GCC 12.2.0] on linux

Type "help", "copyright", "credits" or "license" for more information.

>>>
```

- exit로 파이썬 종료 가능

### 2) 실행중인 Docker Container 에 명령어 실행

#### 명령어

```shell
docker exec [옵션] <컨테이너 이름 또는 ID> [커맨드]
```

#### 옵션

- `-i`, `t`: exec 명령어 실행 후 빠져나오지 않도록 유지 합니다.

#### 사용 예시

```shell
docker exec -it py sh
/ # ls
bin    dev    etc    home   lib    media  mnt    opt    proc   root   run    sbin   srv    sys    tmp    usr    var
```

- `-it` 옵션으로 컨테이너에 있는 쉘을 실행하면 컨테이너에 접속해서 컨트롤 할 수 있습니다.

### 3) Docker Container 리스트 확인 하기

#### 명령어

```shell
docker ps [옵션]
```

#### 옵션

- `-a` : 실행중이 아닌 컨테이너를 포함해서 리스트를 확인 합니다.

#### 사용 예시
```shell
docker ps -a

CONTAINER ID  IMAGE  COMMAND    ...   STATUS         PORTS     NAMES
088b5d666a08  python "python3"  ...   Up 9 seconds             py
...
```

- STATUS에 `Up`은 현재 컨테이너가 실행중이라는 뜻입니다. 실행중이 아닌 경우 `Exited`라고 출력 됩니다.

### 4) 실행중인 Docker Container 정지

#### 명령어

```shell
docker stop <컨테이너 이름 또는 ID>
```

### 5) 정지된 Docker Container를 다시 실행

#### 명령어

```shell
docker start <컨테이너 이름 또는 ID>
```

- 이미 만들어진 컨테이너를 다시 실행 할때는 `docker run`이 아닌 `docker start` 를 사용합니다.
- 이미지를 만들때 `docker run`에서 지정한 **옵션** 값과 **커맨드**가 `docker start`할 때 항상 자동으로 실행 됩니다.

### 6) 실행중인 Docker Container의 로그 보기

#### 명령어

```shell
docker logs [옵션] <컨테이너 이름 또는 ID>
```

#### 옵션

- `-f` : 해당 컨테이너에 붙어서 실시간으로 로그를 출력 합니다.

#### 사용 예시

```shell
docker logs -f py

Python 3.13.1 (main, Jan 24 2025, 20:47:48) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> exit
Python 3.13.1 (main, Jan 24 2025, 20:47:48) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
...
```

### 7) Docker Container 제거

#### 명령어

```shell
docker rm [옵션] <컨테이너 이름 또는 ID>
```

#### 옵션

- `-f` : 실행중인 컨테이너도 강제로 종료 후 삭제 합니다.

---

## 포트포워딩

- 현재 운영체제가 실행되고 있는 영역을 호스트(Host) 영역이라고 합니다.
- 호스트 영역과 컨테이너는 기본적으로 연결이 끊겨있습니다.
- 이미지에서 컨테이너를 만들때 호스트의 포트와 컨테이너의 포트를 연결해 줄 수 있고, 이를 포트포워딩이라고 합니다.

### 사용 예시

```shell
docker run -p <호스트의 포트 번호>:<컨테이너의 포트 번호> python
```

1. 컨테이너에서 파이썬으로 웹 서버를 하나 만들고 8000번 포트로 웹 서버를 실행 합니다.
2. `docker run -p 80:8000 python` 으로 컨테이너를 만들고 실행 합니다.
3. localhost:80/index.html 로 컨테이너에 있는 웹 서버로 접속이 가능 합니다.

---
