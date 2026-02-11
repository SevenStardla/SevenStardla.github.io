---
title: "[VSCode 세팅] VS Code + raylib + C++ (MinGW-w64) 환경 세팅 & 해결 가이드"
date: 2026-01-30 22:00:00 +09:00
categories: [VSCode, C++, raylib]
tags: [VSCode, C++, raylib, MinGw-w64]
math: false
toc: true
pin: false
image:
  path: /assets/postImage/VSCode.png
  alt: VSCode
---

## 이 글을 보기에 앞서..
저는 게임 개발 공부를 위해 C++과 raylib를 선택했습니다.
이 방법을 선택한 이유는 최대한 언리얼 엔진과 유니티 같은 툴에 의존하지 않고
게임이 동작하는 원리를 알고 싶어서 최소한의 라이브러리를 사용해 게임 개발을 진행하려고 했으나,
실제 개발을 시작하기도 전에, 환경 세팅에서 훨씬 더 많은 시간을 쓰게 됐습니다.

이 글은 저처럼 Windows에서 VS Code + raylib + MinGW-w64 환경을 구성하다가
실제로 겪은 문제와 해결 과정을 정리한 기록을 담았습니다.

---

## 1. 목표 환경

최종적으로 구성한 환경은 다음과 같습니다.

OS: Windows
IDE: VSCode
Compiler: MinGW-w64 (mingw64)
Library: raylib
빌드: Debug / Release 분리
디버그: F5로 실행

---

## 2. 가장 큰 문제: VS Code 터미널 꼬임

### 처음 겪은 문제들
- `exit code 1`, `exit code 127` 반복
- exe 파일이 생성되지 않음
- mingw64 터미널에서는 빌드 성공
- VS Code에서만 빌드 실패
- g++가 있는데 없다고 나오는 상황

### 3. 원인 및 해결방법
첫번째로 VS Code에서 기본 터미널이 MSYS / bash로 열리고 있었다는 걸 알았습니다.

---

```text
seven@XXXX MSYS /c/Users/...
$ g++ main.cpp
bash: g++: command not found
```

---
해결방법
 VS Code 검색창에 >Terminal → Select Default Profile 를 선택한 후 Command Prompt(Cmd) 나 PowerShell 둘 중 하나를 선택해야 합니다.
이후 VS Code를 재부팅한 후 Terminal을 실행시킬때 마다 기본으로 PowerShell이나 Command Prompt(Cmd)가 터미널로 실행됩니다.
---
두번째로 gcc / g++ 인식 문제로 환경 변수(PATH)에 MinGW 경로가 등록되지 않았기 때문에 다음과 같은 오류 메시지가 발생했습니다.

```text
'g++' is not recognized as an internal or external command
```

---
해결방법
내 PC → 속성 → 고급 시스템 설정 → 환경 변수(N) → 시스템 변수에서 변수 PATH를 더블 클릭한 후 새로 만들기를 누른 후 MinGw의 bin폴더 경로를 추가합니다.
환경 변수가 제대로 등록 되었는지 Command prompt창을 킨 후 명령어 g++ --version 로 버전이 뜨는지를 확인했으면 MinGw 경로가 제대로 등록이 된 것입니다.
---

---
<!-- ![내PC속성창](repo/images/VSCodeSettings/MyPC_Attribute.png) -->
<img src="./repo/images/VSCodeSettings/MyPC_Attribute.png", height="100x", width="100px">
---
