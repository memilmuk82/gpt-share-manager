# Phase F-1 Task Plan

## 1. Phase 목적

Phase F-1의 목적은 `gpt-share-manager` 프로젝트의 실행 가능한 최소 골격을 만든다.

단, 이번 Phase는 Codex에게 전체 구조를 한 번에 만들게 하는 방식으로 진행하지 않는다.

목표는 다음 두 가지다.

```text
1. Flask + PostgreSQL + Tailwind + pytest 기본 실행 환경을 만든다.
2. 사용자가 각 구성 요소의 역할을 이해하면서 직접 적용한다.
```

이번 수정으로 Python 의존성 관리는 `requirements.txt`가 아니라 `uv + pyproject.toml + uv.lock`을 기준으로 진행한다.

## 2. 권장 작업 위치와 추론 수준

```text
권장 작업 위치: WSL2 Ubuntu + VS Code Remote WSL
ChatGPT 역할: 단계별 안내와 리뷰
Codex 역할: 선택적 보조, 오류 분석, 반복 작업 지원
권장 추론 수준: 중간 → 오류 발생 시 높음
```

이유:

```text
초기 환경 구성은 사용자가 직접 손으로 해보는 것이 학습 가치가 크다.
한 번에 많은 파일을 자동 생성하면 구조를 이해하기 어렵다.
아직 권한/DB 모델/보안 정책 구현 단계는 아니므로 Pro 상시 사용은 필요 없다.
```

## 3. F-1 진행 방식

Phase F-1은 다음 Step으로 나누어 진행한다.

```text
Step 1. 프로젝트 폴더 생성
Step 2. Git 초기화
Step 3. uv 설치/확인
Step 4. uv 프로젝트 초기화
Step 5. Flask 최소 앱 실행
Step 6. 개발 의존성 pytest 추가
Step 7. app factory 구조로 확장
Step 8. config.py / extensions.py / routes 분리
Step 9. Dockerfile 작성
Step 10. docker-compose.yml로 PostgreSQL 추가
Step 11. /healthz에서 DB 연결 확인
Step 12. Tailwind CLI 빌드 흐름 추가
Step 13. pytest 기본 테스트 추가
Step 14. PROJECT_STATUS.md에 F-1 결과 기록
Step 15. Phase Maintenance 수행
Step 16. Git 커밋 메시지 규칙에 따라 상태 저장
```

각 Step은 다음 기준을 따른다.

```text
한 Step에서 너무 많은 파일을 만들지 않는다.
사용자가 작성/적용할 명령어와 코드를 확인한다.
실행 결과를 보고 다음 Step으로 넘어간다.
오류가 나면 해당 오류를 해결한 뒤 다음 Step으로 간다.
```



## 3-1. F-1의 점진적 구조화 기준

F-1은 처음부터 최종 폴더 구조를 만들기보다 실행 흐름을 이해하면서 확장한다.

진행 기준:

```text
처음에는 단순 app.py로 Flask 실행을 확인한다.
그 다음 create_app() 구조로 확장한다.
라우트가 늘어나면 routes/로 분리한다.
설정값이 필요해지면 config.py로 분리한다.
DB 연결 준비가 필요해지면 extensions.py를 둔다.
```

하지 않을 것:

```text
처음부터 models/services/repositories 전체 구조를 만들지 않는다.
사용자/예약/CSV 도메인 파일을 미리 만들지 않는다.
Repository 패턴을 선행 도입하지 않는다.
```

F-1에서 구조화의 목적은 “좋아 보이는 구조”가 아니라 다음이다.

```text
Flask 실행 흐름을 이해한다.
Docker/DB 연결을 위한 최소 구조를 만든다.
다음 Phase인 SQLAlchemy/Alembic 적용을 방해하지 않는 구조를 만든다.
```

## 문서 배치 기준

F-1 프로젝트 시작 시 문서는 아래 위치에 둔다.

```text
gpt-share-manager/
├─ README.md
├─ PROJECT_SPECIFICATION.md
├─ PROJECT_INSTRUCTIONS.md
├─ PROJECT_STATUS.md
└─ docs/
   ├─ architecture/
   │  └─ REPOSITORY_STRUCTURE.md
   ├─ development/
   │  ├─ PHASE_F1_TASK_PLAN.md
   │  └─ DEVELOPMENT_LOG.md
   ├─ guides/
   │  ├─ CODEX_PROMPT_PHASE_F1.md
   │  └─ GIT_WORKFLOW.md
   ├─ decisions/
   │  ├─ AI_COLLABORATION_REVIEW.md
   │  ├─ TECH_STACK_DECISIONS.md
   │  └─ PROGRESSIVE_STRUCTURING.md
   └─ adr/
      ├─ 0001-use-uv.md
      ├─ 0002-use-postgresql-only.md
      ├─ 0003-human-controlled-ai-collaboration.md
      ├─ 0004-progressive-structuring.md
      ├─ 0005-use-jinja-vanilla-tailwind.md
      └─ 0006-use-phase-based-korean-commit-messages.md
```

루트에는 핵심 기준 문서만 둔다. 세부 설명과 결정 기록은 `docs/` 아래에 둔다.

## 4. 최종 목표 구조

F-1이 끝났을 때 최종적으로 아래 구조에 가까워진다.

```text
gpt-share-manager/
├─ README.md
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
│  │  ├─ __init__.py
│  │  ├─ main.py
│  │  └─ health.py
│  ├─ templates/
│  │  ├─ base.html
│  │  └─ index.html
│  └─ static/
│     ├─ css/
│     │  └─ input.css
│     └─ js/
│        └─ app.js
├─ tests/
│  ├─ __init__.py
│  └─ test_health.py
└─ docs/
   ├─ architecture/
   ├─ development/
   ├─ guides/
   ├─ decisions/
   └─ adr/
```

중요:

```text
이 구조를 한 번에 생성하지 않는다.
Step별로 필요한 파일부터 만든다.
requirements.txt / requirements-dev.txt는 기본 구조에 포함하지 않는다.
```

## 5. Step별 계획

### Step 1. 프로젝트 폴더 생성

사용자 직접 수행.

```bash
mkdir -p ~/projects
cd ~/projects
mkdir gpt-share-manager
cd gpt-share-manager
```

확인:

```bash
pwd
```

기대:

```text
/home/<user>/projects/gpt-share-manager
```

### Step 2. Git 초기화

사용자 직접 수행.

```bash
git init
git status
```

확인:

```text
On branch master 또는 main
No commits yet
```

### Step 3. uv 설치/확인

목표:

```text
Python 의존성 관리 도구를 uv로 통일한다.
```

확인:

```bash
uv --version
```

설치되어 있지 않으면 uv 공식 설치 방법 중 하나를 사용한다.

Linux/WSL2 예시:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

설치 후 새 터미널을 열거나 PATH를 갱신한 뒤 다시 확인한다.

```bash
uv --version
```

### Step 4. uv 프로젝트 초기화

목표:

```text
pyproject.toml 기반 프로젝트를 시작한다.
```

프로젝트 루트에서 실행한다.

```bash
uv init --app --bare
```

생성/확인 대상:

```text
pyproject.toml
```

필요 시 Python 버전은 F-1 과정에서 확정한다.

```bash
uv python list
uv python pin 3.12
```

단, Python 버전 pin은 로컬/OCI 호환성 확인 후 적용한다.

### Step 5. Flask 최소 앱 실행

목표:

```text
아직 app factory를 만들지 않고, Flask가 실행되는지만 확인한다.
```

의존성 추가:

```bash
uv add flask
```

생성 파일:

```text
app.py
```

검증:

```bash
uv run flask --app app run --debug
```

브라우저:

```text
http://127.0.0.1:5000
```

health check 확인:

```bash
curl http://127.0.0.1:5000/healthz
```

### Step 6. 개발 의존성 pytest 추가

목표:

```text
개발 전용 의존성을 dependency group으로 분리한다.
```

명령:

```bash
uv add --dev pytest
```

확인:

```bash
uv run pytest --version
```

### Step 7. app factory 구조로 확장

목표:

```text
단일 app.py에서 Flask 프로젝트 구조로 이동한다.
```

생성/변경:

```text
app/__init__.py
app/routes/main.py
```

이 단계에서 app.py는 제거하거나 최소 실행 진입점으로만 둔다.

### Step 8. config/extensions/routes 분리

목표:

```text
이후 SQLAlchemy, OAuth, 환경변수 확장을 담을 구조를 만든다.
```

생성:

```text
app/config.py
app/extensions.py
app/routes/health.py
```

### Step 9. Dockerfile 작성

목표:

```text
Flask 앱을 컨테이너로 실행할 준비를 한다.
```

원칙:

```text
Dockerfile은 pyproject.toml과 uv.lock을 기준으로 의존성을 설치한다.
requirements.txt를 복사하지 않는다.
.venv는 이미지 빌드 컨텍스트에 포함하지 않는다.
```

### Step 10. docker-compose.yml로 PostgreSQL 추가

목표:

```text
PostgreSQL 컨테이너를 띄운다.
```

서비스:

```text
web
db
```

필수:

```text
db healthcheck 포함
web은 db service_healthy 이후 시작
.env 사용
```

### Step 11. /healthz에서 DB 연결 확인

목표:

```text
Flask에서 PostgreSQL에 SELECT 1을 실행한다.
```

응답 예시:

```json
{"status":"ok","database":"ok"}
```

### Step 12. Tailwind CLI 빌드 흐름 추가

목표:

```text
Tailwind CDN이 아니라 CLI 기반 빌드 구조를 준비한다.
```

생성:

```text
package.json
app/static/css/input.css
```

### Step 13. pytest 기본 테스트 추가

목표:

```text
create_app 또는 /healthz 기본 동작을 테스트한다.
```

생성:

```text
tests/test_health.py
```

검증:

```bash
uv run pytest
```

### Step 14. PROJECT_STATUS.md 갱신

목표:

```text
F-1 완료 여부와 테스트 결과를 기록한다.
```

## 6. F-1에서 하지 않을 일

명시적으로 하지 않는다.

```text
Google OAuth 구현 안 함
사용자 테이블 구현 안 함
예약 테이블 구현 안 함
CSV 업로드 구현 안 함
Settings/GuideItems 구현 안 함
관리자 화면 구현 안 함
Nginx 구성 안 함
OCI 배포 안 함
Alembic migration 생성 안 함
```

Alembic 설정은 F-2에서 진행한다. 단, `Flask-Migrate` 의존성은 F-1 후반에 추가할 수 있으나 실제 migration 생성은 F-2에서 진행한다.

## 7. 완료 기준

Phase F-1 완료 조건:

```text
uv 기반 pyproject.toml과 uv.lock이 생성된다.
Flask 앱이 로컬에서 실행된다.
Flask 앱이 Docker Compose로 실행된다.
PostgreSQL 컨테이너가 healthy 상태가 된다.
/healthz에서 DB 연결 ok를 반환한다.
Tailwind CSS 빌드가 가능하다.
pytest가 통과한다.
PROJECT_STATUS.md에 F-1 완료 결과를 기록할 수 있다.
```



## 7-1. F-1 Phase Maintenance 완료 기준

F-1 종료 시 다음을 점검한다.

```text
□ 최소 Flask 앱 실행 흐름을 설명할 수 있는가
□ app factory 구조로 바꾼 이유를 설명할 수 있는가
□ routes/config/extensions 분리 이유를 설명할 수 있는가
□ Docker Compose와 로컬 실행의 차이를 설명할 수 있는가
□ 단일 파일이 리뷰하기 어려울 정도로 길어지지 않았는가
□ F-2에서 SQLAlchemy 모델을 추가하기에 구조가 과하지도 부족하지도 않은가
□ pytest가 통과하는가
□ PROJECT_STATUS.md에 F-1 결과가 기록되었는가
```

F-1에서 구조화가 부족하면 F-2로 넘어가기 전에 최소 정리한다.  
반대로 구조가 과하면 불필요한 파일을 늘리지 않는다.

## 8. 예상 리스크

```text
uv 미설치 또는 PATH 미반영
WSL2 Docker integration 미설정
Docker Compose 버전 문제
PostgreSQL 연결 문자열 오류
Tailwind CLI 버전 차이
Windows 경로(/mnt/c)에서 파일 성능 저하
.env 누락
초기 app.py와 app factory 구조 혼동
```

대응:

```text
프로젝트는 WSL2의 ~/projects 아래에 생성한다.
Docker Desktop WSL integration을 켠다.
.env는 .env.example을 복사해서 만든다.
docker compose version을 먼저 확인한다.
한 번에 구조를 바꾸지 말고 Step 단위로 진행한다.
```

## 9. F-1 완료 후 다음 단계

F-1 완료 후 Phase F-2로 넘어가기 전에 다음을 점검한다.

```text
프로젝트 구조가 과하지 않은가?
사용자가 각 파일 역할을 설명할 수 있는가?
환경변수 구조가 명확한가?
Docker Compose가 재현 가능한가?
Tailwind 빌드 결과를 Git에 포함할지 제외할지 결정했는가?
Alembic 적용 전 DB URL과 앱 팩토리 구조가 안정적인가?
uv.lock이 재현 가능한 상태로 생성되었는가?
```

다음 Phase:

```text
Phase F-2: SQLAlchemy 모델 + Alembic
```
## 8. Git 커밋 기준

Phase F-1부터 커밋 메시지는 아래 형식을 따른다.

```text
[Phase] type: 한국어 설명
```

F-1 예시:

```text
[F-1] build: uv 프로젝트 초기화
[F-1] feat: Flask 최소 앱 실행
[F-1] test: health check 테스트 추가
[F-1] refactor: app factory 구조로 분리
[F-1] docs: Phase F-1 진행 상태 갱신
```

커밋 전 확인:

```text
git status 확인
git diff 확인
실행 또는 테스트 결과 확인
커밋 메시지가 변경 성격을 정확히 설명하는지 확인
```

세부 기준은 다음 문서를 따른다.

```text
docs/guides/GIT_WORKFLOW.md
```
