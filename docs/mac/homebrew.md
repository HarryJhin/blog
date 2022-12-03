---
comments: true
---

# Mac - Homebrew

## 설치

터미널을 실행하고 다음 명령을 실행합니다.

```zsh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 최초 설정

설치가 완료되었으면 실행하기 위한 최초 설정을 설정해야 합니다.

```zsh
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
source ~/.zprofile
```

마지막으로, 정상 사용이 가능한지 확인해봅니다.

```zsh
brew doctor
```

다음과 같이 출력된다면 정상적으로 설치가 완료되었습니다.

```zsh
Your system is ready to brew.
```

## 사용법

`brew` 명령어를 사용하여 손쉽게 패키지를 검색, 설치, 업그레이드, 삭제할 수 있습니다.

### 검색

다음은 git이라는 패키지가 있는지 확인하는 예제입니다.

```zsh
brew search git
```

검색하려는 패키지명은 풀네임이 아니라 일부여도 됩니다.

### 설치

다음은 git을 설치하는 예제입니다.

```zsh
brew install git
```

### 업그레이드

다음은 git의 버전을 업데이트하는 예제입니다.

```zsh
brew upgrade git
```

### 삭제

다음은 git을 삭제하는 예제입니다.

```zsh
brew uninstall git
```

!!! warning "brew로 설치한 패키지만 삭제할 수 있습니다"

    `brew`로 설치되지 않은 패키지(응용 프로그램 등)는 삭제할 수 없으니 주의하세요.
