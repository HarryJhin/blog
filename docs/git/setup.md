---
title: Git - Setup
comments: true
---

# Git - Setup

## Git 설치

### 윈도우

윈도우 10/11 사용자는 [winget] 명령어를 사용하여 설치할 수 있습니다.

[winget]: ../windows/winget/installation.md

```powershell
winget install git.git
```

!!! tip "WSL 사용자이신가요?"

    WSL을 사용하신다면 설치된 Ubuntu에 기본적으로 Git이 포함되어 있으니, 또 설치하실 필요가 없습니다.

### 맥

맥(mac) 사용자는 [brew] 또는 [port] 명령어를 사용하여 설치할 수 있습니다.

[brew]: ../mac/hombrew.md
[port]: ../mac/port.md

```zsh
brew install git
```

```zsh
sudo port install git
```

### 우분투

우분투는 `apt`를 사용하여 설치할 수 있습니다.

```bash
sudo apt install git
```

## 최초 설정

Git을 본격적으로 사용하기 전에 해두어야 할 최초 설정이 있습니다.

1. git 사용자 이름

    ```bash
    git config --global user.name 사용자이름
    ```

    Ex: `git config --global user.email HarryJhin`

2. git 사용자 이메일


    ```bash
    git config --global user.email 사용자이메일
    ```

    Ex: `git config --global user.email joojinhyun00@gmail.com`

## 기본 편집기 설정

깃에 대해 설정 및 커밋 등의 활동에서 다룰 편집기를 설정할 수 있습니다.

```bash
git config --global core.editor vim # vim
git config --global core.editor notepad # notepad (메모장)
git config --global core.editor code # Visual Studio Code
```
