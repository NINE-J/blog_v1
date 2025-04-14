---
title: IntelliJ IDEA에서 프로젝트 경고
description: Microsoft Defender may affect IDE
author: Nine
Created: 2025-04-06
categories:
  [IDE,
  IntelliJ]
tags:
  [devlog,
  IDE,
  IntelliJ,
  WindowsDefender]
image:
  path: /assets/img/posts/20250406/thumbnail-2025-04-06-IntelliJ-Microsoft-Defender-may-affect-IDE.png
  lqip: data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAoAAAAGCAYAAAD68A/GAAAAAklEQVR4AewaftIAAABUSURBVI3BMQ6AIBAAwRWxoICe8P9PWdqYszESmkuMiHxAZqYQQmWAYZClSSkRY0RVcc6hqnjvyTkjIogIlmYuO8e68ykG9IbT0C2VztJs18Mfw6AX8jIcdWoFOX8AAAAASUVORK5CYII=
  alt: IntelliJ IDEA 프로젝트 경고 Microsoft Defender may affect IDE
---
## 📌개요

IntelliJ IDEA에서 프로젝트를 열 때 "Microsoft Defender may affect IDE" 경고가 뜨는 건 Microsoft Devender(Windows Defender)의 실시간 보호 기능이 IDE 성능에 영향을 줄 수 있다는 의미다.

## 📌내용

Windwos Defender의 실시간 보호 기능은 파일 시스템의 변경 사항을 실시간으로 검사하여 악성 코드나 의심스러운 활동을 탐지한다.

IntelliJ와 같은 IDE는 빌드, 인덱싱, 파일 읽기/쓰기 작업이 빈번하게 발생하기 때문에 Defender의 스캔이 성능 저하를 유발할 수 있다.

이 경고는 사용자가 이를 해결할 수 있도록 몇 가지 옵션을 제공한다.

![IntelliJ IDEA](/assets/img/posts/20250406/Pasted image 20250406124804.png)

### Exclude folders

현재 열려 있는 프로젝트를 Defender가 특정 폴더를 실시간 스캔에서 제외하도록 설정한다.
해당 폴더 내 파일을 스캔하지 않게 되어 IDE 성능이 향상될 수 있다.

예를 들어, IntelliJ는 `.idea`(프로젝트 설정), `target`(Maven/Gradle 빌드 결과물), 또는 소스 코드 폴더에서 빈번하게 파일을 생성하거나 수정한다.

이런 폴더를 제외하면 Defender가 불필요한 스캔을 하지 않아 성능 저하를 줄일 수 있다.

### Ignore for this project

해당 프로젝트에 대해 경고를 다시 표시하지 않도록 설정한다.
단, 이 경우 Defender 설정이 변경되지는 않으며 단순히 경고 알림만 비활성화된다.
성능 문제는 여전히 남아 있을 수 있다.

### Never ask again

모든 프로젝트에 대해 이 경고를 비활성화한다.
역시 Defender 설정 자체에는 영향을 주지 않는다.

### 제외하면 어디에 기록되지?

`Exclude folders`를 선택하면 IntelliJ가 Windows Defender의 제외 목록에 해당 폴더를 추가한다.
이 설정은 IntelliJ 자체에 저장되는 것이 아니라 Windows Defender의 설정에 기록된다.

#### Windows Defender 제외 설정 위치

Windows Defender의 제외 목록은 Windows 시스템 설정에 저장된다.
일반적으로 이 정보는 레지스트리나 Defender의 내부 데이터베이스에 기록되며, 사용자가 직접 편집할 수 있는 특정 파일로 존재하지 않는다.

하지만 Windows Defender 설정을 통해 확인할 수 있다.

`설정 > Windows 보안 > 바이러스 및 위협 방지 > 바이러스 및 위협 방지 설정 관리`에서 제외 목록을 확인할 수 있고 제거할 수 있다.

![Windows Defender](/assets/img/posts/20250406/Pasted image 20250406125851.png)

#### IntelliJ의 역할

IntelliJ는 사용자가 `Exclude folders`를 선택하면 Windows Defender API를 호출하여 해당 프로젝트 폴더를 제외 목록에 추가한다고 한다.

## 🎯결론

간단한 테스트를 위해 만든 프로젝트를 모두 계속 등록하게 되면 어딘가에 기록이 쌓이는지 궁금해서 찾아보게 됐다.

폴더 또는 파일의 수정이 빈번하게 발생하는 프로젝트를 계속 Windows Defender가 스캔하며 성능이 저하될 수 있다는 경고다.

경고를 무시하고 진행해도 되고, 성능을 위해 Defender의 제외 목록에 등록할 수도 있다.
