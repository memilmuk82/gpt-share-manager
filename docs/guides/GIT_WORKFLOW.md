# Git Workflow

## 1. 문서 목적

이 문서는 `gpt-share-manager` 프로젝트의 Git 사용 방식, 커밋 메시지 규칙, Phase별 커밋 기준을 정의한다.

이 프로젝트는 단순히 빠르게 앱을 완성하는 것이 아니라, 사용자가 전체 개발 프로세스를 이해하고 통제하는 것을 목표로 한다. 따라서 Git 기록도 학습과 유지보수의 일부로 본다.

## 2. 기본 원칙

```text
커밋은 작업 흐름을 설명하는 기록이다.
커밋 메시지는 나중에 읽어도 변경 이유와 성격을 알 수 있어야 한다.
작업자가 이해하지 못한 변경은 커밋하지 않는다.
테스트하지 않은 핵심 변경은 커밋하지 않는다.
Codex가 만든 변경도 사용자가 diff를 검토한 뒤 커밋한다.
```

## 3. 커밋 메시지 언어 원칙

이 프로젝트는 한국어 커밋 메시지를 허용하고 권장한다.

추천 형식은 다음이다.

```text
[Phase] type: 한국어 설명
```

예시:

```text
[F-0] docs: 프로젝트 명세와 AI 협업 개발 원칙 정리
[F-1] build: uv 프로젝트 초기화
[F-1] feat: Flask 최소 앱 실행
[F-1] test: health check 테스트 추가
[F-2] feat: SQLAlchemy User 모델 추가
[F-2] refactor: app factory 구조로 분리
[F-3] fix: OAuth 콜백 세션 검증 오류 수정
```

영어 type prefix를 쓰는 이유:

```text
커밋 성격을 빠르게 구분할 수 있다.
GitHub, changelog, 자동화 도구와 궁합이 좋다.
짧은 영어 prefix 뒤에 한국어 설명을 붙이면 국내 수업/업무 맥락에서 읽기 쉽다.
```

한국어 설명을 쓰는 이유:

```text
개발자와 학생이 변경 내용을 더 빨리 이해할 수 있다.
학교 현장과 수업 자료로 재사용하기 쉽다.
혼자 또는 국내 팀 중심 프로젝트에서는 영어 문장보다 유지보수성이 높을 수 있다.
```

## 4. type prefix 규칙

| type | 의미 | 사용 예시 |
|---|---|---|
| `docs` | 문서 추가/수정 | `[F-0] docs: 프로젝트 명세서 작성` |
| `feat` | 기능 추가 | `[F-1] feat: Flask 최소 앱 실행` |
| `fix` | 버그 수정 | `[F-3] fix: 로그인 세션 검증 오류 수정` |
| `refactor` | 동작 변경 없는 구조 개선 | `[F-2] refactor: DB 설정 로직 분리` |
| `test` | 테스트 추가/수정 | `[F-1] test: health check 테스트 추가` |
| `style` | UI, 포맷, Tailwind, 코드 포맷 | `[F-4] style: 사용자 목록 테이블 간격 조정` |
| `build` | uv, Docker, CI, 빌드 설정 | `[F-1] build: uv 프로젝트 초기화` |
| `chore` | 기타 유지보수 | `[F-1] chore: 불필요한 캐시 파일 제외` |

주의:

```text
refactor는 기능 변경이 없어야 한다.
기능 추가와 refactor를 한 커밋에 섞지 않는다.
보안/권한 정책 변경은 feat나 fix로 숨기지 않고 메시지에 명확히 드러낸다.
```

## 5. 좋은 커밋 메시지 기준

좋은 메시지:

```text
[F-1] feat: /healthz 상태 확인 라우트 추가
[F-2] build: Alembic 초기 migration 설정 추가
[F-4] fix: 마지막 활성 admin 비활성화 방지 검증 수정
```

나쁜 메시지:

```text
수정
업데이트
작업함
코드 정리
오류 고침
```

좋은 메시지는 다음을 포함한다.

```text
무엇을 바꿨는가
어느 Phase 작업인가
변경 성격이 무엇인가
나중에 로그를 봐도 이해 가능한가
```

## 6. 언제 커밋하는가

커밋 권장 시점:

```text
한 Step이 정상 실행되었을 때
관련 테스트가 통과했을 때
문서 기준점이 바뀌었을 때
Phase Maintenance가 끝났을 때
다음 작업으로 넘어가기 전에 현재 상태를 보존해야 할 때
```

커밋을 미뤄야 하는 경우:

```text
코드가 실행되지 않는 상태
테스트가 실패했는데 원인을 기록하지 않은 상태
변경 범위가 너무 커서 리뷰하지 않은 상태
Codex가 만든 diff를 사용자가 아직 확인하지 않은 상태
정책/보안 변경인데 승인 기록이 없는 상태
```

예외:

```text
실험 브랜치에서는 WIP 커밋을 허용할 수 있다.
main 브랜치에는 가능한 한 실행 가능한 상태만 커밋한다.
```

## 7. Branch 전략

초기 개인 개발 단계에서는 `main` 하나로 시작할 수 있다.

다만 다음 경우에는 브랜치를 만든다.

```text
여러 파일을 수정하는 작업
Codex가 직접 패치를 적용하는 작업
DB migration이 포함된 작업
권한/보안 정책에 영향이 있는 작업
실패 가능성이 큰 실험
```

브랜치 이름 예시:

```text
phase-f1-basic-flask
phase-f2-db-models
phase-f3-google-oauth
phase-f4-user-management
experiment-tailwind-layout
```

## 8. Codex 사용 시 Git 원칙

Codex는 자동 커밋/자동 push를 하지 않는다.

Codex 작업 흐름:

```text
1. 사용자 또는 ChatGPT가 작업 범위를 정한다.
2. Codex는 변경 대상 파일과 영향 범위를 먼저 제시한다.
3. 사용자가 승인한다.
4. Codex가 승인된 범위만 수정한다.
5. 사용자가 git diff를 확인한다.
6. 테스트를 실행한다.
7. 사용자가 커밋 메시지를 결정한다.
8. 사용자 승인 후 commit한다.
```

Codex에게 금지할 것:

```text
승인 없는 파일 수정
승인 없는 commit
승인 없는 push
전체 프로젝트 자동 생성
의미 없는 대규모 refactor
.gitignore에 포함되어야 할 파일 커밋
실제 .env 또는 secret 커밋
```

## 9. 기본 명령어

상태 확인:

```bash
git status
```

변경 내용 확인:

```bash
git diff
```

스테이징:

```bash
git add <파일명>
```

전체 스테이징은 신중하게 사용한다.

```bash
git add .
```

커밋:

```bash
git commit -m "[F-1] feat: Flask 최소 앱 실행"
```

로그 확인:

```bash
git log --oneline --decorate --graph
```

최근 커밋 변경 파일 확인:

```bash
git show --stat
```

## 10. Phase별 커밋 예시

### Phase F-0

```text
[F-0] docs: 프로젝트 명세와 AI 협업 개발 원칙 정리
[F-0] docs: 문서 배치와 ADR 구조 정리
[F-0] docs: Git 작업 흐름과 커밋 규칙 추가
```

### Phase F-1

```text
[F-1] build: uv 프로젝트 초기화
[F-1] feat: Flask 최소 앱 실행
[F-1] test: health check 테스트 추가
[F-1] refactor: app factory 구조로 분리
[F-1] build: Docker Compose PostgreSQL 구성 추가
[F-1] docs: Phase F-1 진행 상태 갱신
```

### Phase F-2

```text
[F-2] feat: SQLAlchemy 기본 모델 추가
[F-2] build: Alembic 초기 migration 추가
[F-2] test: 사용자 모델 제약조건 테스트 추가
```

## 11. 문서 갱신과 커밋

다음 경우 `PROJECT_STATUS.md`를 갱신한다.

```text
Phase가 바뀔 때
테스트 기준이 바뀔 때
승인 완료 항목이 추가될 때
별도 승인 필요 항목이 생길 때
다음 작업 기준점이 바뀔 때
```

다음 경우 `docs/development/DEVELOPMENT_LOG.md`를 갱신한다.

```text
왜 그런 결정을 했는지 기록해야 할 때
기술 선택이 바뀔 때
오류 해결 과정이 의미 있을 때
Phase 종료 시 회고를 남길 때
```

다음 경우 ADR을 추가한다.

```text
장기적으로 영향을 주는 기술 선택
다른 대안이 있었던 결정
나중에 다시 논쟁될 수 있는 결정
교육 자료로 설명할 가치가 있는 결정
```

## 12. 최종 원칙

```text
Git 기록은 결과물의 부산물이 아니다.
Git 기록은 개발 과정과 판단을 남기는 학습 자료다.
```

이 프로젝트의 커밋은 속도보다 설명 가능성을 우선한다.
