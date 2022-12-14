---
title: 깃으로 커밋하기
description: >-
    깃을 사용하여 커밋하는 방법은 `git commit` 명령어를 사용하는 것입니다. 작업 영역에 있는 것 말고 스테이지 영역에 있는 것만 커밋을 하게 되면 하나의 버전이 추가됩니다.
comments: true
---

# Git - Commit

커밋(commit)이란 버전을 생성하는 것을 의미합니다.

## 1. 상태

깃 저장소에는 용이한 버전 관리를 위해 세 가지 상태(status)를 두고 있습니다:

1. 작업 트리(**working tree**)
2. 스테이지(**stage**)
3. 저장소(**repository**)

### 1.1. 작업 트리

작업 트리(working tree)는 우리가 실제로 작업하는 로컬의 디렉토리를 의미합니다.

`repository`라는 깃 저장소를 만들었다면 작업 트리라고도 말할 수 있습니다.

이 곳에서 우리는 파일을 생성하거나 수정하거나 삭제할 수 있습니다.

당연하죠? 원래 일반적인 사용 방법이 그러하니까요.
### 1.2. 스테이지

스테이지(stage)는 작업 트리에서 변경된 내용을 버전으로 만들기 위해 대기하는 영역입니다.

우리가 작업한 모든 내용을 버전에 추가하고 싶지 않을 수 있기 때문에 선택적으로 변경 내용을 버전으로 추가할 수 있도록 하는 기능입니다.

실제로 스테이지 내용을 확인하고 싶다면 `.git/index` 파일을 확인해보시면 됩니다.

### 1.3. 저장소

저장소(repository)는 스테이지에 있던 변경 사항을 커밋하여 새롭게 추가된 버전을 저장하는 영역입니다.

실제 버전을 저장하고 작업 트리와 비교하는 기준점이 됩니다.

즉, 저장소는 버전이라고 보셔도 무방합니다.

실제 저장소 내용을 확인하고 싶다면 `.git/HEAD` 파일을 확인해보시면 됩니다.

### 1.4. 상태 확인하기

현재 작업한 내용이 어느 단계인지 확인하는 방법은 `git status` 명령어입니다.

```bash
git status
```

- `untaracked files`: 버전(`commit`)에 포함되지 않고, 무시(`ignore`[^1])되지 않고, 추적(`add`)되지 않는 파일 변경 사항
- `changes to be commnited`: 추적 중인 파일의 변경 사항

## 2. 스테이지 추가

변경 사항을 스테이지에 추가하는 것은 버전에 추가하기 위한 대기열에 합류시킨 것입니다.

스테이지에 추가하는 방법은 `git add <파일 이름>` 명령어입니다.

```bash
git add test.txt # test.txt 파일의 변경 사항이 있어야만 합니다.
```

`git status` 명령어를 실행하면 tracked files에 추가되어 있는 것을 확인할 수 있습니다.

### 2.1. 경로에 있는 변경 사항 추가

```bash
git add test/*
```

### 2.2. 모든 변경 사항 추가

```bash
git add -A # 또는 --all
```

## 3. 커밋하기

```bash
git commit -m "테스트 커밋"
```

### 3.1. 모든 변경 사항을 커밋하기

`git add -A` 명령을 사전에 입력하지 않아도 커밋할 때 똑같은 옵션을 선언할 수 있습니다.

```bash
git commit -am "모든 변경 사항 커밋"
```

## 4. 커밋 관리

버전을 관리할 수 있도록 다양한 방법을 지원합니다.

- `log`: 커밋 기록 확인
- `diff`: 변경 사항 확인

### 4.1. 커밋 기록 확인

현재까지 기록된 버전 기록을 확인할 수 있도록 `log` 명령을 지원합니다.

```bash
git log
```

버전에 포함된 변경 사항 파일 명을 보고 싶다면 `--stat` 옵션을 사용하면 됩니다.

```bash
git log --stat
```

### 4.2. 변경 사항 확인

변경 사항은 저장소에 저장된 버전 정보를 기준으로 판단합니다.

변경 사항을 판단하는 기준은 글자 단위가 아닌 줄 단위입니다.

"가나다라마바사"라는 글자를 "가나다라마바사아자차카타파하"로 수정했다면 깃은 변경 사항을 다음과 같이 판단합니다.

- "가나다라마바사" 줄은 삭제(**---**)
- "가나다라마바사아자차카타파하" 줄을 추가(**+++**)

확인 하는 방법은 `diif` 명령어입니다.

```bash
git diff
```

[^1]:
    git 설정에는 특정 파일의 변경 사항을 매번 추적하는 것을 막기 위한 `.gitignore` 파일 옵션을 제공합니다. 이 파일에 명세된 폴더 또는 파일은 더이상 추적하지 않습니다.
