---
title: "리눅스 터미널 치트 시트"
date: 2024-05-05 00:00:00 +/-TTTT
categories: [Main, Linux]
tags: [Linux]
toc: true
---

## 1. 터미널 기본 개념

리눅스 터미널(Terminal)은 명령어 기반으로 시스템을 조작하는 인터페이스입니다. 명령어를 입력하여 파일을 조작하고, 프로세스를 관리하며, 네트워크 설정을 변경하는 등의 작업을 수행할 수 있습니다.

## 2. 기본 명령어

### 파일 및 디렉토리 조작

- `ls` : 현재 디렉토리의 파일 목록 보기 (`ls -l`, `ls -a` 등 옵션 가능)
- `cd [디렉토리]` : 디렉토리 이동 (`cd ..` : 상위 디렉토리 이동)
- `pwd` : 현재 위치 확인
- `mkdir [디렉토리명]` : 새 디렉토리 생성
- `rm [파일/디렉토리]` : 파일 삭제 (`rm -r [디렉토리]` : 디렉토리 삭제)
- `cp [원본] [대상]` : 파일 복사 (`cp -r [디렉토리] [대상]` : 디렉토리 복사)
- `mv [원본] [대상]` : 파일 또는 디렉토리 이동/이름 변경

### 파일 내용 확인 및 편집

- `cat [파일]` : 파일 내용 출력
- `less [파일]` : 페이지 단위로 파일 보기 (`q` 키로 종료)
- `nano [파일]` : 간단한 텍스트 편집기 실행
- `vim [파일]` : 강력한 텍스트 편집기 실행 (`i`: 입력 모드, `Esc` + `:wq` : 저장 후 종료)

### 파일 권한 및 소유권 변경

- `chmod [모드] [파일]` : 파일 권한 변경 (`chmod 755 script.sh`)
- `chown [사용자:그룹] [파일]` : 파일 소유자 변경 (`chown user:user file.txt`)
- `chgrp [그룹] [파일]` : 파일 그룹 변경 (`chgrp developers file.txt`)

## 3. 프로세스 및 시스템 관리

### 프로세스 관리

- `ps aux` : 현재 실행 중인 프로세스 목록 확인
- `top` : 실시간 프로세스 모니터링 (`htop`은 더 편리한 대체 명령어)
- `kill [PID]` : 특정 프로세스 종료
- `killall [프로세스이름]` : 해당 이름의 모든 프로세스 종료
- `pkill [이름]` : 프로세스 이름으로 종료

### 시스템 상태 확인

- `df -h` : 디스크 사용량 확인
- `du -sh [디렉토리]` : 특정 디렉토리의 용량 확인
- `free -m` : 메모리 사용량 확인
- `uptime` : 시스템 가동 시간 확인
- `who` : 현재 로그인한 사용자 목록
- `uname -a` : 시스템 정보 확인

## 4. 네트워크 명령어

- `ping [주소]` : 네트워크 연결 확인 (`ping google.com`)
- `curl -I [URL]` : HTTP 헤더 정보 가져오기
- `wget [URL]` : 파일 다운로드
- `ifconfig` 또는 `ip a` : 네트워크 인터페이스 정보 확인
- `netstat -tulnp` 또는 `ss -tulnp` : 열려 있는 포트 확인
- `traceroute [주소]` : 경로 추적
- `nslookup [도메인]` : DNS 정보 확인

## 5. 사용자 및 그룹 관리

- `whoami` : 현재 사용자 확인
- `id` : 현재 사용자 및 그룹 ID 확인
- `sudo [명령어]` : 관리자 권한으로 명령 실행
- `adduser [사용자]` : 새 사용자 추가
- `passwd [사용자]` : 비밀번호 변경
- `usermod -aG [그룹] [사용자]` : 사용자를 그룹에 추가
- `deluser [사용자]` : 사용자 삭제

## 6. Bash Shell 스크립트 기본

### 변수 및 기본 구문

```bash
#!/bin/bash

# 변수 설정
name="Linux"
echo "Hello, $name!"

# 조건문
if [ -f "/etc/passwd" ]; then
    echo "File exists."
fi

# 반복문
for i in {1..5}; do
    echo "Iteration $i"
done

# 함수 정의
function greet {
    echo "Welcome, $1!"
}
greet "User"
```

### 실행 방법

```bash
chmod +x script.sh
./script.sh
```

## 7. 패키지 관리

### Debian 기반 (Ubuntu, Debian 등)

- `apt update` : 패키지 목록 갱신
- `apt upgrade` : 패키지 업데이트
- `apt install [패키지명]` : 패키지 설치
- `apt remove [패키지명]` : 패키지 삭제

### RHEL 기반 (CentOS, Fedora 등)

- `yum update` 또는 `dnf update` : 패키지 업데이트
- `yum install [패키지명]` : 패키지 설치
- `yum remove [패키지명]` : 패키지 삭제

## 8. 로그 및 시스템 모니터링

- `journalctl -xe` : 시스템 로그 확인
- `tail -f /var/log/syslog` : 실시간 로그 모니터링
- `dmesg` : 시스템 부팅 메시지 확인
- `history` : 실행한 명령어 기록 확인

## 9. 터미널 단축키

- `Ctrl + C` : 실행 중인 프로세스 중지
- `Ctrl + Z` : 프로세스 일시 중지
- `Ctrl + D` : 현재 터미널 세션 종료
- `Ctrl + L` : 터미널 화면 정리
- `!!` : 마지막 명령어 실행
- `!n` : n번째 명령어 실행 (예: `!42` → 42번째 실행)
- `Ctrl + R` : 명령어 검색 (이전 명령어 빠르게 실행)

## 10. 터미널 환경 설정

- `.bashrc` : 사용자별 Bash 설정 파일 (`~/.bashrc` 수정)
- `.bash_profile` : 로그인 시 실행되는 설정 파일 (`~/.bash_profile` 수정)
- `alias ll='ls -l'` : 명령어 단축 설정
- `export PATH=$PATH:/usr/local/bin` : 환경 변수 설정
