# Repository Structure

## 권장 저장소 구조

```text
gpt-share-manager/
├─ README.md
├─ PROJECT_SPECIFICATION.md
├─ PROJECT_INSTRUCTIONS.md
├─ PROJECT_STATUS.md
├─ .gitignore
├─ .env.example
├─ .python-version
├─ pyproject.toml
├─ uv.lock
├─ package.json
├─ Dockerfile
├─ docker-compose.yml
├─ app/
│  ├─ __init__.py
│  ├─ config.py
│  ├─ extensions.py
│  ├─ routes/
│  ├─ templates/
│  └─ static/
├─ tests/
├─ migrations/
└─ docs/
   ├─ architecture/
   │  └─ REPOSITORY_STRUCTURE.md
   ├─ development/
   │  ├─ PHASE_F1_TASK_PLAN.md
   │  └─ DEVELOPMENT_LOG.md
   ├─ guides/
   │  └─ CODEX_PROMPT_PHASE_F1.md
   ├─ decisions/
   │  ├─ AI_COLLABORATION_REVIEW.md
   │  ├─ TECH_STACK_DECISIONS.md
   │  └─ PROGRESSIVE_STRUCTURING.md
   └─ adr/
      ├─ 0001-use-uv.md
      ├─ 0002-use-postgresql-only.md
      ├─ 0003-human-controlled-ai-collaboration.md
      ├─ 0004-progressive-structuring.md
      └─ 0005-use-jinja-vanilla-tailwind.md
```

## 루트 문서 원칙

루트에는 프로젝트를 시작할 때 바로 확인해야 하는 문서만 둔다.

```text
README.md
PROJECT_SPECIFICATION.md
PROJECT_INSTRUCTIONS.md
PROJECT_STATUS.md
```

## docs/ 문서 원칙

세부 문서, Phase 문서, 의사결정 기록, 가이드 문서는 `docs/` 아래에 둔다.

이유:

```text
루트 과밀 방지
문서 역할 구분
새 대화창 인수인계 단순화
학생들에게 설명 가능한 문서 구조 확보
```

## 점진적 구조화와의 관계

이 저장소 구조도 처음부터 과도하게 확장하지 않는다.

F-1에서는 필요한 문서와 최소 앱 구조만 만든다. `models/`, `services/`, `repositories/`는 실제 필요가 생기는 Phase에서 추가한다.
