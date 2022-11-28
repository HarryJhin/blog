---
title: Oh-My-Posh Set Up
description: >-
    WSL 환경에서 Oh My Posh를 설치하는 방법에 대해 소개합니다.
comments: true
---

# Oh My Posh

## 요구사항

- Windows 10/11
- Windows Terminal
- WSL2
- homebrew
- Nerd Font

### Windows Terminal 설치

!!! tip
    Windows 11은 Windows Terminal이 기본으로 설치되어 있으니 이 섹션은 건너뛰면 됩니다.

설치 방법:

1. Microsoft Store
2. Winget

저는 Winget(앱 설치 관리자)를 통한 설치 방법을 소개합니다.

1. PowerShell 실행
2. `winget install microsoft.windowsterminal` 명령 실행

    ```powershell
    winget install microsoft.windowsterminal # (1)!
    ```

    1. winget 명령은 microsoft에서 만든 앱 설치 관리자 cli입니다.

    ??? question "winget 용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다"

        ```powershell
        winget : 'winget' 용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다. 이름이 정확한지 확인하고 경로가 포함된 경우 경로가 올바른지 검증한 다음 다시 시도하십시오.
        위치 줄:1 문자:1
        + winget
        + ~~~~~~
            + CategoryInfo          : ObjectNotFound: (winget:String) [], CommandNotFoundException
            + FullyQualifiedErrorId : CommandNotFoundException
        ```

        위와 같은 에러 메시지를 겪는다면 Microsoft Store에서 업데이트가 필요합니다.

        [앱 설치 관리자 업데이트하러가기](https://apps.microsoft.com/store/detail/%EC%95%B1-%EC%84%A4%EC%B9%98-%EA%B4%80%EB%A6%AC%EC%9E%90/9NBLGGH4NNS1){ .md-button .md-button--primary }

### WSL2 설치

WSL2는 커널 버전을 의미하는 것으로 구버전 실행은 권장하지 않습니다.

소개해드리는 방법으로 설치하면 자동으로 WSL2 커널로 적용되기 때문에 신경쓰지 않아도 됩니다.

1. Windows Terminal(PowerShell 프로필) 관리자 권한으로 실행
2. `wsl --install` 명령 실행

    ```powershell
    wsl --install
    ```

3. 설치가 완료되면 시스템 재시작
4. username, password를 묻는 질문에 차레대로 응답

### Homebrew 설치

[공식문서 바로가기 :material-link:](https://brew.sh/index_ko){ .md-button .md-button--primary }

1. apt를 업그레이드 해줍니다.

    ```bash
    sudo apt update && sudo apt upgrade
    ```

2. homebrew 설치 명령 실행

    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

3. 