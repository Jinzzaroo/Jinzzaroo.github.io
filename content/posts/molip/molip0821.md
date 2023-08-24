---
title: "[몰입교육] 깃헙 액션"
date: 2023-08-21T09:30:58+09:00
author : "Jinzzaroo"
draft: false
categories : ["몰입교육"]
tags : ["CI/CD"]
---

GitHub Actions 알아보기
===================

## Overview
> Github Actions는 빌드, 테스트 및 배포 파이프 라인을 자동화할 수 있는 CI/CD 플랫폼이다.

## Components
### Workflows 
- 자동화 프로세스
- YAML
- 리포지토리의 .github/workflows 디렉토리에 정의

### Events
- workflow 트리거
- pull request, issue open, commit push 할 때 시작

### Jobs
- 동일한 runner에서 실행되는 workflow에 있는 steps의 집합
- 각 step은 실행될 쉘 스크립트 혹은 action
- 서로 다른 job끼리 기본적으로 비의존적이지만 의존성 부여 가능

### Actions
- workflow 파일의 반복 코드 줄이기 용도
- 반복되는 task 수행하는 커스텀 애플리케이션

### Runners
- 트리거될 때 workflows를 실행하는 server
- 각 runner는 한 번에 하나의 job

---

### Workflow 파일


```yaml
name: learn-github-actions
run-name: ${{ github.actor }} is learning GitHub Actions
on: [push]
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v
```


| 코드 | 설명 |
| --- | --- |
| name: learn-github-actions | Optional - GitHub repository의 "Actions" 탭에 표시되는 workflow의 이름입니다. 이 필드를 생략하면 workflow 파일의 이름이 대신 사용됩니다. |
| run-name: ${{ github.actor }} is learning GitHub Actions | Optional - 워크플로에서 생성된 workflow run의 이름은 repository의 "Actions" 탭에 있는 workflow run에 표시됩니다. 이 예에서는 github context와 함께 expression을 사용하여 워크플로 실행을 트리거한 actor의 username을 표시합니다.|
| on: [push] | 이 workflow의 트리거를 지정합니다. 이 예제에서는 push event를 사용하므로 누군가 repository에 변경 사항을 push하거나 pull request를 merge할 때마다 workflow run이 트리거됩니다. 이는 모든 분기에 대한 push에 의해 트리거됩니다.  |
| jobs: | learn-github-actions workflow에서 실행되는 모든 job을 함께 그룹화합니다.  |
|   check-bats-version: | check-bats-version이라는 이름의 job을 정의합니다. 하위 키는 작업의 속성을 정의합니다. |
|     runs-on: ubuntu-latest | 최신 버전의 Ubuntu Linux runner에서 실행되도록 job을 구성합니다. 이것은 job이 GitHub에서 hosting하는 새로운 가상 머신에서 실행됨을 의미합니다. |
|     steps: | check-bats-version job에서 실행되는 모든 step을 함께 그룹화합니다.  이 section 아래에 중첩된 각 항목은 별도의 action 또는 쉘 스크립트입니다. |
|       - uses: actions/checkout@v3 |  uses 키워드는 이 step이 action/checkout action의 v3을 실행하도록 지정합니다. 이것은 runner에서 repository를 확인하는 작업으로, 코드에 대해 스크립트 또는 기타 작업 (예: 빌드 및 테스트 도구)을 실행할 수 있습니다. workflow가 repository의 코드를 사용할 때마다 checkout 작업을 사용해야 합니다. |
|       - uses: actions/setup-node@v3 with : node-version: '14' | 이 step에서는 actions/setup-node@v3 작업을 사용하여 지정된 버전의 Node.js를 설치합니다. (이 예제에서는 버전 14를 사용합니다.) 이렇게 하면 node 및 npm 명령이 모두 PATH에 저장됩니다. |
|       - run: npm install -g bats | run 키워드는 runner에서 명령을 실행하도록 job에 지시합니다. 이 경우 npm을 사용하여 bats 소프트웨어 테스트 패키지를 설치합니다. |
|       - run: bats -v | 마지막으로 소프트웨어 버전을 출력하는 매개변수와 함께 bats 명령을 실행합니다. |