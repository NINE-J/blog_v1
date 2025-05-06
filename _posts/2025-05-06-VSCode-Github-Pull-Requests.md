---
title: VSCode에서 PR 보기
description: feat.GitHub Pull Requests
author: Nine
Created: 2025-05-06
categories:
  [IDE,
  VSCode]
tags:
  [devlog,
  VSCode,
  Github,
  PR,
  PullRequest,
  Extensoins]
image:
  path: /assets/img/posts/20250506/thumbnail-2025-05-06-VSCode-Github-Pull-Requests.png
  lqip: data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAoAAAAGCAYAAAD68A/GAAAAAklEQVR4AewaftIAAABISURBVI3BsQnDMBAAwNPzKoyTCQLefygP4SpNMJ8YREqju1Y/JoRJadiP01m8PyxJYe3N9gyXNCzZXNaOotDDXxpej3AnTPoCWwAOWlTGmvAAAAAASUVORK5CYII=
  alt: VSCode에서 PR 보기 feat.GitHub Pull Requests
---
## 📌개요

VSCode에서 PR 보려는데 복잡시럽다 복잡시러.
IntelliJ Ultimate/Community에선 GitHub 플러그인으로 손쉽게 확인이 가능하다.

## 📌내용

### IDE에서 PR을 확인하면 좋은 점

코드 리뷰에 대한 코멘트를 **바로 파일의 라인에서 확인**할 수 있다.
의견이 있어서 Reply를 남기거나 수정 완료를 곧바로 처리할 수 있다.

![IDE에서 PR을 확인하면 좋은 점](/assets/img/posts/20250506/Pasted image 20250506022741.png)

### GitHub Pull Requests
![GitHub Pull Requests 확장툴](/assets/img/posts/20250506/Pasted image 20250506021354.png)

현재 기준 GitHub Pull Requests를 설치한다. [VSCode marketplace - GitHub Pull Requests](https://marketplace.visualstudio.com/items/?itemName=GitHub.vscode-pull-request-github)
예전 이름은 GitHub Pull Requests and Issues였나 보다.
기능은 같아서 PR, Issues를 확인할 수 있다.

### 근데 이게 문제였다

확장 설치하면 열려 있는 PR만 확인이 됐다.
필요한 다른 항목은 쿼리를 수정해줘야 한다.

`Ctrl + Shift + P` 명령 팔레트

```bash
>GitHub Pull Requests: Configure
# 엔터 치면 두 개 나온다
# Configure Remotes...
# Configure Queries...
```

![GitHub Pull Requests: Configure](/assets/img/posts/20250506/Pasted image 20250506024023.png)

나는 닫힌 PR을 확인해야 해서 추가했다.

```json
// settings.json
{
  // ... others
  "githubPullRequests.queries": [
	// ... others
    {
	  "label": "My Closed PRs",
	  "query": "is:closed assignee:${user}"
    }
  ]
}
```

필요에 맞게 수정 후 새로고침하면 잘 확인된다.

![GitHub Pull Requests 설정 settings.json](/assets/img/posts/20250506/Pasted image 20250506023804.png)
