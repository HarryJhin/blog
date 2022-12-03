---
comments: true
---

# Git - init

깃을 본격적으로 사용하려면 깃 저장소가 필요합니다. 버전 관리를 사용하려면 전제 조건이 깃 저장소여야하기 때문입니다.

깃(git) 저장소(repository)를 생성하는 방법은 크게 두 가지 입니다:

1. 로컬(local) 저장소 만들기
2. 원격(remote) 저장소 만들기

## 로컬 저장소 생성

원하는 디렉토리로 이동한 후 `git init` 명령어를 사용하면 해당 디렉토리는 깃 저장소가 됩니다.

```bash
mkdir repository # repository 이름을 가진 디렉토리 생성
cd repository # repository 디렉토리로 이동
git init # repository 디렉토리를 깃 저장소로 초기화
```

위 과정을 거치면 `repository`라는 이름을 가진 깃 저장소를 생성한 것입니다.

무엇이 달라졌는지 알기 위해 터미널에서 다음 명령어를 입력합니다.

```bash
la -al
drwxr-xr-x jjh staff  96 B Sat Dec  3 23:08:24 2022  .
drwxr-xr-x jjh staff 352 B Sat Dec  3 23:08:18 2022  ..
drwxr-xr-x jjh staff 288 B Sat Dec  3 23:08:24 2022  .git
```

위와 같이 `.git` 디렉토리가 보이게 되는데 여기에 버전 정보 및 설정이 있습니다.

이제 이 디렉토리에서 일어나는 파일을 생성, 수정, 삭제하는 내용을 모두 추적될 수 있는 준비 상태가 되었습니다.

## 원격 저장소 생성

원격 저장소는 보통 서버에 저장되어 있는 저장소를 이야기 합니다.

저장소 서버를 직접 구축해도 되지만 이미 폭넓게 사용되는 SaaS[^1]가 많습니다.

대표적인 SaaS로 Github(Microsoft), BitBucket(Atlassian) 등이 있습니다.

- '**Github**'은 다양한 오픈소스들이 모여있습니다. 세계 최대의 Git 서버라고 생각하시면 됩니다. 기본적으로 대부분의 기능을 무료로 사용할 수 있다보니 접근성이 제일 좋습니다.
- '**BitBucket**'은 Atlassian 회사의 솔루션 중 하나로 Jira, Wiki 등의 서비스와 함께 제공됩니다. 이 솔루션의 장점은 기업의 거대한 프로젝트의 히스토리, 요건 사항, 개발 사항을 공유하는 것에 최적화되어 있다는 것입니다. 국내에도 많은 대기업들이 내부적으로 사용 중입니다.

[^1]:
    SaaS(software as a service)란 서비스형 소프트웨어라고 이야기하며, 인터넷 브라우저를 통해 사용자에게 서비스 애플리케이션을 제공하는 클라우드 기반 소프트웨어입니다. 다른 대표적인 서비스로 Notion, Google Docs, Office 365 등이 있습니다.
