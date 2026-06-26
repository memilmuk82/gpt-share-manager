# gpt-share-manager

Flask + PostgreSQL + Vanilla JavaScript + Tailwind CSS + Docker Compose + OCI 기반의 GPT 공동 사용 예약·관리 시스템이다.

이 프로젝트는 기존 Google Apps Script 운영 버전의 후속 포트폴리오/확장형 프로젝트이며, 단순 자동 생성이 아니라 **사용자 통제형 AI 협업 개발** 방식으로 진행한다.

## 핵심 목표

```text
1. GPT 공동 사용 예약·관리 시스템의 Flask 버전 완성
2. 전체 개발 프로세스를 이해하고 통제하는 AI 협업 개발 방식 확립
3. 학생들에게 설명 가능한 개발 흐름과 문서 구조 확보
```

## 먼저 읽을 문서

```text
PROJECT_SPECIFICATION.md   무엇을 만들지 정의
PROJECT_INSTRUCTIONS.md    어떻게 작업할지 정의
PROJECT_STATUS.md          현재 어디까지 왔는지 기록
```

## 세부 문서

```text
docs/architecture/   저장소 구조, 시스템 구조
docs/development/    Phase 계획, 개발 로그
docs/guides/         Codex 프롬프트, 작업 가이드
docs/decisions/      기술 선택과 AI 협업 방향
docs/adr/            주요 의사결정 기록
```

## 현재 단계

```text
현재 Phase: Phase F-1 착수 준비
진행 방식: WSL2 Ubuntu + VS Code Remote WSL + uv
Codex 사용: 자동 구현이 아니라 보조 개발자/리뷰어로 사용
```

## 작업 원칙

```text
AI가 전체 앱을 대신 만들지 않는다.
사용자가 이해 가능한 단위로 구현한다.
작동하는 코드에서 시작해 필요할 때 구조화한다.
각 Phase 종료 시 Phase Maintenance를 수행한다.
```
