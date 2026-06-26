# GPT Share Manager - Project Status

## 1. 프로젝트 개요

### 프로젝트명

```text
gpt-share-manager
```

### 목적

Flask + PostgreSQL + Vanilla JavaScript + Tailwind CSS + Docker Compose + OCI 기반의 GPT 공동 사용 예약·관리 시스템을 만든다.

이 프로젝트는 기존 Google Apps Script 기반 운영 버전의 후속 포트폴리오/확장형 프로젝트다.

## 2. 기존 운영 버전 기준

기존 Apps Script 버전은 다음 상태를 기준으로 한다.

```text
Phase 13-B 완료
TEST_runAll PASS 73 / FAIL 0
사용자 CSV 일괄 등록 완료
Client_Backup.html 삭제 확정
```

Flask 버전은 기존 운영 버전을 직접 수정하지 않고 별도 프로젝트로 진행한다.

## 3. 현재 Phase

```text
현재 Phase: Phase F-0
상태: 사용자 통제형 AI 협업 개발 원칙, 점진적 구조화 원칙, 문서 배치 원칙, Git 작업 흐름 반영 완료 / Phase F-1 착수 준비
```

## 4. 현재까지 완료된 결정

### 프로젝트 방향

```text
Flask 버전은 기존 Apps Script 운영 버전과 별도 프로젝트로 진행
프로젝트명: gpt-share-manager
포트폴리오/확장/OCI 배포 목적
```

### 핵심 개발 철학

```text
AI가 앱을 대신 완성하는 방식으로 진행하지 않음
사용자가 전체 프로세스의 통제권을 가짐
코드는 사용자가 이해 가능한 단위로 제시
복사·붙여넣기는 코드 리뷰와 학습 과정으로 인정
Codex는 자동 구현자가 아니라 보조 개발자/리뷰어로 사용
최종 목표는 앱 완성과 개발 프로세스 이해를 함께 달성하는 것
```

### 교육적 목표

```text
학생들에게 설명 가능한 AI 협업 개발 방식으로 남긴다.
딸깍식 자동 완성보다 요구사항, 설계, 구현, 테스트, 리뷰 흐름을 중시한다.
AI 도구가 바뀌어도 유지보수할 수 있는 원리 이해를 목표로 한다.
```



### 점진적 구조화 / Phase Maintenance

```text
처음부터 완성형 아키텍처를 만들지 않음
작동하는 코드에서 시작
불편함이 명확해질 때 최소 범위로 구조화
각 Phase 종료 시 Phase Maintenance 수행
단일 파일이 너무 길어져 리뷰를 포기하는 상황 방지
학생 수업에서도 적용 가능한 개발 흐름으로 정리
```

### 기술 스택

```text
Backend:
Flask
SQLAlchemy
Alembic
PostgreSQL
Gunicorn

Python Tooling:
uv
pyproject.toml
uv.lock

Frontend:
Jinja2 SSR
Vanilla JavaScript
Tailwind CSS

Infra:
Docker
Docker Compose
Nginx
OCI Ubuntu

Auth:
Google OAuth
senedu.kr 도메인 제한
```

### DB / 의존성 관리 방향

```text
PostgreSQL only
SQLite 사용 안 함
Alembic 필수 사용
uv + pyproject.toml + uv.lock 사용
requirements.txt 중심 관리 사용 안 함
```

### 인증/권한

```text
Google OAuth + senedu.kr 도메인 제한 목표
F-1/F-2 개발 단계에서는 mock login 제한 허용
admin/subadmin/user 권한 구조
최소 1명의 활성 admin 유지
```

### 보안 정책

```text
GPT 계정 ID 저장 금지
GPT 비밀번호 저장 금지
공용 계정 접속 정보를 DB/Settings/GuideItems에 저장하지 않음
민감정보 입력 금지 안내 유지
GuideItems HTML 실행 금지
XSS 방지
```

주의:

```text
예약 성공 후 계정 ID/PW를 안내하는 방식은 MVP에 포함하지 않음.
필요 시 별도 Credential Delivery 정책으로 분리하고 별도 승인 후 검토.
```

### CSV 정책

```text
CSV 템플릿 다운로드 MVP 포함
CSV 업로드 MVP 포함
CSV 서버 검증
CSV all-or-nothing 저장
CSV 업로드 이력 저장
CSV 검증 실패 로그 저장
```

### 테스트 전략

```text
pytest 사용
각 Phase 테스트 통과 전 다음 Phase 진행 금지
권한/예약/CSV/Settings/GuideItems/Alembic 테스트 포함
```

### 작업 환경

```text
WSL2 Ubuntu
VS Code Remote WSL
Codex CLI 또는 Codex VS Code Extension
Docker Desktop WSL integration
```

### Codex 사용 원칙

```text
Codex는 승인 전 자동 수정 금지
Codex는 승인 전 commit 금지
Codex는 승인 전 push 금지
작은 변경은 수동 패치 방식 우선
여러 파일 수정은 승인 후 Codex 브랜치 패치 방식 허용
수정 후 git diff 확인
Codex는 사용자의 구현 보조자이지 대체자가 아님
```

### Git 작업 흐름 / 커밋 메시지

```text
Git 기록은 개발 과정과 판단을 남기는 학습 자료로 본다.
커밋 메시지는 [Phase] type: 한국어 설명 형식을 사용한다.
영어 type prefix와 한국어 설명을 함께 사용한다.
Codex가 만든 변경도 사용자가 diff를 검토한 뒤 커밋한다.
승인 없는 Codex commit/push는 금지한다.
```

기본 type:

```text
docs
feat
fix
refactor
test
style
build
chore
```

### 모델 사용 원칙

```text
Pro:
설계, DB, 권한, 보안, OAuth, Docker/OCI, 최종 검토

높음:
백엔드 구현 검토, 오류 분석, 테스트 설계

중간:
단순 CRUD, Jinja 화면, Vanilla JS 렌더링, 문서 초안

즉시:
브레인스토밍, 문구, Tailwind, 단순 HTML

Codex:
파일 생성 보조, 패치 보조, 테스트 실행 보조, 반복 구현 보조
```

## 5. 생성된 문서와 배치

### 루트 문서

```text
README.md
PROJECT_SPECIFICATION.md
PROJECT_INSTRUCTIONS.md
PROJECT_STATUS.md
```

### docs 문서

```text
docs/architecture/REPOSITORY_STRUCTURE.md
docs/development/PHASE_F1_TASK_PLAN.md
docs/development/DEVELOPMENT_LOG.md
docs/guides/CODEX_PROMPT_PHASE_F1.md
docs/guides/GIT_WORKFLOW.md
docs/decisions/AI_COLLABORATION_REVIEW.md
docs/decisions/TECH_STACK_DECISIONS.md
docs/decisions/PROGRESSIVE_STRUCTURING.md
docs/adr/0001-use-uv.md
docs/adr/0002-use-postgresql-only.md
docs/adr/0003-human-controlled-ai-collaboration.md
docs/adr/0004-progressive-structuring.md
docs/adr/0005-use-jinja-vanilla-tailwind.md
docs/adr/0006-use-phase-based-korean-commit-messages.md
```

### 문서 배치 결정

```text
루트에는 프로젝트 기준 문서만 둔다.
세부 문서는 docs/ 아래에 역할별로 둔다.
기술 선택 이유는 decisions와 adr에 기록한다.
```


## 6. 미완료 작업

### Phase F-0

```text
사용자 통제형 AI 협업 개발 원칙 문서 반영 완료
Phase F-1 작업 계획 갱신 완료
Codex 보조 지시문 갱신 완료
ERD 상세화 예정
Route/API 상세화 예정
```

### Phase F-1

```text
WSL2 Ubuntu에서 프로젝트 폴더 생성
Git 초기화
uv 설치/확인
uv 프로젝트 초기화
Flask 최소 앱 실행
Phase F-1 종료 시 Phase Maintenance 수행
pytest 개발 의존성 추가
app factory 구조 확장
Dockerfile 생성
docker-compose.yml 생성
PostgreSQL 연결
환경변수 구조 생성
기본 health check 작성
Tailwind CLI 빌드 흐름 준비
pytest 기본 테스트 작성
pyproject.toml / uv.lock 생성
```

### Phase F-2

```text
SQLAlchemy 모델 작성
Alembic 설정
초기 migration 생성
seed 데이터 구조 작성
```

### Phase F-3

```text
Google OAuth 적용
senedu.kr 도메인 제한
사용자 session 구조
권한 decorator
mock login 제거 또는 개발 전용 제한
```

### Phase F-4

```text
사용자 목록
사용자 추가
사용자 수정
사용자 활성화/비활성화
최소 활성 admin 보호
등록 요청 승인/반려
```

### Phase F-5

```text
예약 생성
예약 충돌 검증
충돌 확인 후 저장
사용 시작
사용 완료
예약 취소
관리자 삭제
```

### Phase F-6

```text
CSV 템플릿 다운로드
CSV 업로드
CSV 검증
CSV all-or-nothing 저장
CSV 업로드 이력
CSV 검증 실패 로그
```

### Phase F-7

```text
Settings 관리
Settings 변경 로그
GuideItems 관리
GuideItems escape/XSS 확인
```

### Phase F-8

```text
pytest 통합
권한 테스트
예약 충돌 테스트
CSV 테스트
마이그레이션 테스트
보안 점검
```

### Phase F-9

```text
OCI Ubuntu 배포
Nginx
Gunicorn
HTTPS
환경변수/Secret 관리
백업 전략
```

## 7. 승인 완료 항목

```text
A1. 프로젝트명: gpt-share-manager
A2. 기존 Apps Script 버전과 별도 프로젝트
B1. 핵심 문서 생성
B2. 추가 문서는 후속 Phase에서 생성 가능
C1. Flask + SQLAlchemy + Alembic + PostgreSQL + Gunicorn
C2. Jinja2 + Vanilla JS + Tailwind
C3. 로컬 Docker Compose 안정화 후 OCI 배포
D1. PostgreSQL only
D2. Alembic 필수
D3. 기존 Apps Script 데이터 구조를 PostgreSQL로 이관 설계
D4. csv_upload_logs, csv_validation_errors MVP 포함
D5. admin_action_logs는 MVP 최소 범위 또는 후속 Phase
E1. Google OAuth + senedu.kr 제한
E2. 초기 개발 단계 mock login 제한 허용
E3. admin/subadmin/user 권한 구조
E4. 최소 1명의 활성 admin 유지
F1. GPT 계정 ID/PW 저장 금지 유지
F2. 민감정보 입력 금지 안내 유지
F3. GuideItems HTML 실행 금지와 XSS 방지 유지
G1. MVP 기능 범위 승인
G2. MVP 이후 백로그 승인
H1. CSV 템플릿 다운로드 MVP 포함
H2. CSV 업로드 이력/검증 실패 로그 MVP 포함
H3. CSV all-or-nothing 유지
I1. pytest 기반 테스트 전략
I2. 테스트 통과 전 다음 Phase 진행 금지
J1. WSL2 Ubuntu + VS Code + Codex 보조 기반 진행
J2. Codex는 승인 전 자동 수정 금지, 수동 패치/브랜치 패치 병행
J3. 작업 전 권장 작업 위치와 추론 수준 안내
K1. 모델 사용 전략 문서화
K2. Pro 절약형 작업 원칙 문서화
L1. Phase F-0 ~ F-9 구조
M1. 금지 사항 문서화
N1. 사용자 통제형 AI 협업 개발 원칙 반영
N2. 학생 수업 확장 가능성을 프로젝트 목표에 포함
N3. 점진적 구조화 원칙 반영
N4. Phase Maintenance 원칙 반영
```

## 8. 별도 승인 필요 항목

```text
예약 성공 후 GPT 계정 ID/PW 직접 안내 기능
Credential Delivery 정책
OCI Vault 또는 별도 Secret 관리
admin_action_logs 전체 범위 구현
CSV 템플릿 버전 관리
고급 관리자 대시보드
OCI 자동 배포 스크립트
백업 자동화
이메일/알림 기능
```

## 9. 현재 테스트 상태

아직 Flask 프로젝트 코드가 생성되지 않았으므로 테스트는 없다.

```text
pytest: 미구성
Docker Compose: 미구성
Alembic migration: 미구성
```

기존 Apps Script 테스트 기준:

```text
TEST_runAll PASS 73 / FAIL 0
```

## 10. 다음 작업

### 다음 권장 작업

```text
Phase F-1 Step 1 시작
WSL2 Ubuntu에서 프로젝트 폴더 생성
Git 초기화
uv 설치/확인
uv 프로젝트 초기화
Flask 최소 앱 실행
Phase F-1 종료 시 Phase Maintenance 수행
```

### Phase F-1 시작 전 제시할 내용

```text
권장 작업 위치: VS Code Remote WSL + ChatGPT 단계별 안내
권장 추론 수준: 중간
Codex 사용: 선택적 보조

이유:
- 첫 환경 구성은 사용자가 직접 손으로 진행하는 것이 학습 가치가 큼
- 아직 여러 파일 자동 생성이 필요한 단계가 아님
- 문제가 발생하면 Codex 또는 ChatGPT로 오류 분석

검증 방법:
- uv --version
- git status
- pyproject.toml 생성 확인
- uv run flask --app app run --debug
- 브라우저에서 localhost 확인
```

## 11. 새 대화창 인수인계

새 대화창에서는 다음 순서로 진행한다.

```text
1. PROJECT_SPECIFICATION.md 확인
2. PROJECT_INSTRUCTIONS.md 확인
3. PROJECT_STATUS.md 확인
4. 현재 Phase가 F-0/F-1 경계인지 확인
5. 사용자 통제형 AI 협업 원칙 확인
6. 승인 완료 항목 확인
7. 별도 승인 필요 항목 확인
8. 작업 전 권장 작업 위치와 추론 수준 제시
9. 변경 대상/영향 범위/검증 방법 제시
10. 사용자가 이해 가능한 최소 단위로 진행
11. 테스트 결과 보고
```
