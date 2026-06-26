# gpt-share-manager Repository Layout Bundle

이 묶음은 `gpt-share-manager` 프로젝트의 Phase F-0 문서와 Phase F-1 착수용 문서를 저장소 구조에 맞게 재배치한 버전이다.

## 핵심 변경

```text
루트에는 핵심 기준 문서만 둔다.
세부 문서는 docs/ 아래에 역할별로 둔다.
주요 의사결정은 docs/adr/에 기록한다.
```

## 루트 파일

```text
README.md
PROJECT_SPECIFICATION.md
PROJECT_INSTRUCTIONS.md
PROJECT_STATUS.md
```

## docs 파일

```text
docs/architecture/REPOSITORY_STRUCTURE.md
docs/development/PHASE_F1_TASK_PLAN.md
docs/development/DEVELOPMENT_LOG.md
docs/guides/CODEX_PROMPT_PHASE_F1.md
docs/decisions/AI_COLLABORATION_REVIEW.md
docs/decisions/TECH_STACK_DECISIONS.md
docs/decisions/PROGRESSIVE_STRUCTURING.md
docs/adr/*.md
```

## 사용 방법

프로젝트 루트에 이 구조 그대로 복사한다.

새 대화창이나 Codex 작업 전에는 다음 순서로 읽는다.

```text
1. PROJECT_INSTRUCTIONS.md
2. PROJECT_STATUS.md
3. PROJECT_SPECIFICATION.md
4. docs/development/PHASE_F1_TASK_PLAN.md
```

Codex를 사용할 때는 `docs/guides/CODEX_PROMPT_PHASE_F1.md`를 사용한다.
