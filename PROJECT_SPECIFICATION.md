# GPT Share Manager - Project Specification

## 1. 프로젝트 개요

### 프로젝트명

```text
gpt-share-manager
```

### 프로젝트 목적

`gpt-share-manager`는 부서 또는 팀에서 공동으로 사용하는 GPT 계정의 사용 시간을 예약·관리하기 위한 Flask 기반 웹 애플리케이션이다.

이 프로젝트는 기존 Google Apps Script 기반 `GPT Pro 공동 사용 지원 시스템`의 포트폴리오/확장형 후속 버전이다.

기존 운영 버전은 다음 구조로 유지한다.

```text
Google Apps Script
Google Sheets
Vanilla JavaScript
Tailwind CSS
Google Workspace 계정 기반
```

Flask 버전은 다음 구조로 별도 개발한다.

```text
Flask
PostgreSQL
Vanilla JavaScript
Tailwind CSS
Docker Compose
OCI 배포
```

## 2. 이 프로젝트의 이중 목표

이 프로젝트는 단순히 작동하는 앱을 빠르게 만드는 것만을 목표로 하지 않는다.

목표는 두 가지다.

```text
1. GPT 공동 사용 예약·관리 시스템의 Flask 버전 완성
2. AI와 협업하면서도 개발자가 전체 프로세스를 이해하고 통제하는 개발 방식 확립
```

따라서 이 프로젝트는 다음 방향으로 진행한다.

```text
AI가 전체 앱을 대신 만들어 주는 방식이 아니다.
사용자가 이해 가능한 단위로 설계, 구현, 테스트, 리뷰를 반복한다.
AI는 설계 보조, 코드 초안 제시, 오류 분석, 대안 비교, 코드 리뷰를 담당한다.
사용자는 요구사항을 결정하고, 코드를 읽고, 적용하고, 실행 결과를 확인한다.
```

이 원칙은 교육적 목적과도 연결된다.

```text
나중에 학생들과 AI 협업 개발 수업으로 확장할 수 있는 방식을 남긴다.
학생들이 배워야 할 것은 '딸깍으로 완성하기'가 아니라, AI 결과를 이해하고 검토하고 통제하는 과정이다.
```

## 3. 기존 Apps Script 버전과의 관계

### 기존 운영 버전

기존 Apps Script 버전은 학교 내부 실제 운영 안정성을 우선하는 버전이다.

```text
목적: 실제 운영
저장소: Google Sheets
배포: Google Apps Script Web App
계정 인증: Google Workspace
운영 방향: 단순하고 안정적인 업무 도구
```

### Flask 버전

Flask 버전은 기존 정책과 기능을 바탕으로 서버 기반 구조, PostgreSQL 데이터 모델, Docker/OCI 배포, CSV 이력 관리, 테스트 자동화 등을 갖춘 별도 프로젝트다.

```text
목적: 포트폴리오/확장/서버 기반 운영 실험
저장소: PostgreSQL
배포: Docker Compose → OCI Ubuntu
계정 인증: Google OAuth
운영 방향: 서버 기반 웹앱 설계 역량 증명
```

### 분리 원칙

```text
기존 Apps Script 운영 코드는 수정하지 않는다.
Flask 버전은 별도 저장소와 별도 문서 체계로 진행한다.
기존 정책은 기본적으로 승계하되, 서버 기반 구조에 맞게 재설계한다.
```

## 4. AI 협업 개발 원칙

이 프로젝트의 AI 사용 방식은 다음과 같다.

```text
사용자 = 주 개발자 / 의사결정자 / 코드 적용자
ChatGPT = 설계 파트너 / 리뷰어 / 보안·구조 검토자
Codex = 보조 개발자 / 코드 초안 작성자 / 테스트 실행 보조자
VS Code = 사용자가 직접 코드를 읽고 적용하는 작업 공간
```

중요 원칙:

```text
AI에게 전체 프로젝트를 한 번에 생성시키지 않는다.
단계별 최소 단위로 진행한다.
복사·붙여넣기는 불필요한 노동이 아니라 코드 검토와 학습 과정으로 본다.
코드는 사용자가 이해 가능한 범위에서만 적용한다.
과한 주석과 과잉 설명은 피하되, 변경 이유와 검증 방법은 반드시 남긴다.
```

이 방식은 생산성만 놓고 보면 느릴 수 있다. 그러나 다음 장점이 있다.

```text
전체 개발 흐름을 이해할 수 있다.
AI 도구가 바뀌어도 유지보수할 수 있다.
학생들에게 설명 가능한 개발 과정을 남길 수 있다.
코드 리뷰 능력과 요구사항 정리 능력을 함께 기를 수 있다.
```



## 4-1. 점진적 구조화 원칙

이 프로젝트는 처음부터 과도한 완성형 아키텍처를 만들지 않는다.

핵심 방향은 다음이다.

```text
작동하는 코드
→ 불편함 발견
→ 최소 범위 구조화
→ 테스트
→ 다음 기능
```

이 원칙을 두는 이유:

```text
처음부터 복잡한 폴더 구조를 만들면 코드 흐름을 이해하기 어렵다.
초급~중급 전환 단계에서는 구조보다 실행 흐름 이해가 먼저다.
수업에서도 학생들이 “왜 나누는지”를 체감해야 한다.
AI가 만든 복잡한 구조를 맹목적으로 수용하지 않게 해야 한다.
```

따라서 Phase F-1은 단순한 `app.py`에서 시작할 수 있다. 이후 앱이 커지고 불편함이 명확해질 때 `create_app()`, `config.py`, `extensions.py`, `routes/`로 분리한다.

수업용 표현:

```text
작동하는 코드에서 유지보수 가능한 코드로 이동한다.
```

## 4-2. 문서 배치 원칙

이 프로젝트는 문서를 모두 루트에 두지 않는다.

루트에는 새 대화창, 새 작업 환경, GitHub 첫 진입 시 바로 확인해야 하는 핵심 문서만 둔다.

```text
README.md
PROJECT_SPECIFICATION.md
PROJECT_INSTRUCTIONS.md
PROJECT_STATUS.md
```

나머지 문서는 `docs/` 아래에 역할별로 배치한다.

```text
docs/architecture/   저장소 구조, 시스템 구조, ERD, API 구조
docs/development/    Phase 계획, 개발 로그, 작업 기록
docs/guides/         Codex 프롬프트, 배포 가이드, 운영 가이드
docs/decisions/      AI 협업 방향, 기술 선택, 점진적 구조화 설명
docs/adr/            주요 의사결정 기록
```

이 구조를 쓰는 이유는 다음이다.

```text
루트가 문서로 과밀해지는 것을 방지한다.
새 작업자는 핵심 문서 3~4개만 먼저 읽으면 된다.
세부 문서는 필요할 때 docs/에서 찾아볼 수 있다.
학생들에게도 문서의 역할과 위치를 설명하기 쉽다.
```

중요한 원칙:

```text
PROJECT_STATUS.md는 루트에 둔다.
PROJECT_INSTRUCTIONS.md는 루트에 둔다.
PROJECT_SPECIFICATION.md는 루트에 둔다.
Phase별 세부 계획과 Codex 프롬프트는 docs/ 아래에 둔다.
기술 선택 이유는 docs/decisions/ 또는 docs/adr/에 둔다.
```

## 4-3. Git 기록과 커밋 메시지 원칙

이 프로젝트에서 Git 기록은 단순한 저장 기록이 아니라 개발 과정과 판단을 남기는 학습 자료다.

커밋 메시지는 다음 형식을 기본으로 한다.

```text
[Phase] type: 한국어 설명
```

예시:

```text
[F-0] docs: 프로젝트 명세와 AI 협업 개발 원칙 정리
[F-1] build: uv 프로젝트 초기화
[F-1] feat: Flask 최소 앱 실행
```

이 방식을 선택한 이유:

```text
Phase 흐름을 git log만 보고도 추적할 수 있다.
영어 type prefix로 변경 성격을 빠르게 구분할 수 있다.
한국어 설명으로 학교/수업/개인 학습 맥락에서 읽기 쉽다.
AI/Codex가 만든 변경도 사용자가 검토하고 승인한 기록으로 남길 수 있다.
```

세부 기준은 아래 문서에 둔다.

```text
docs/guides/GIT_WORKFLOW.md
docs/adr/0006-use-phase-based-korean-commit-messages.md
```

## 5. 목표 사용자

```text
일반 사용자:
- 공용 GPT 계정 예약
- 현재 사용 상태 확인
- 본인 예약 확인
- 사용 시작/완료/취소

관리자:
- 사용자 관리
- 등록 요청 승인/반려
- 예약 관리
- CSV 일괄 등록
- Settings 관리
- GuideItems 관리
- CSV 업로드 이력 확인
- 검증 실패 로그 확인

보조 관리자:
- 운영 보조
- 제한된 관리 기능 수행
```

## 6. 기술 스택

### Backend

```text
Flask
SQLAlchemy
Alembic
PostgreSQL
Gunicorn
```

### Python / Dependency Management

```text
Python: F-1에서 로컬/OCI 호환성을 확인한 뒤 확정
기본 후보: Python 3.12 또는 3.13
Dependency Manager: uv
Project Metadata: pyproject.toml
Lock File: uv.lock
```

원칙:

```text
requirements.txt 중심으로 시작하지 않는다.
운영/개발 의존성은 pyproject.toml과 dependency-groups로 관리한다.
재현 가능한 설치를 위해 uv.lock을 Git에 포함한다.
requirements.txt가 필요한 외부 환경이 생기면 uv export로 별도 생성한다.
```

### Frontend

```text
Jinja2 SSR
Vanilla JavaScript
Tailwind CSS
```

명시적 제외:

```text
React 사용 안 함
Vue 사용 안 함
Svelte 사용 안 함
초기 버전에서 SPA 구조로 시작하지 않음
```

### Infrastructure

```text
Docker
Docker Compose
Nginx
OCI Ubuntu
```

### Authentication

```text
Google OAuth
senedu.kr 도메인 제한
```

개발 단계에서는 제한적으로 mock login을 허용할 수 있다.

```text
F-1/F-2: 개발용 mock login 허용
F-3 이후: Google OAuth 적용
운영/OCI: mock login 비활성화
```

## 6-1. 기술 선택 검토

### Python 의존성 관리

후보:

```text
pip + requirements.txt
Poetry
uv
```

채택:

```text
uv
```

채택 이유:

```text
pyproject.toml 기반으로 프로젝트 메타데이터와 의존성을 함께 관리할 수 있다.
uv.lock을 통해 로컬, WSL2, Docker, OCI 환경의 의존성 재현성을 높일 수 있다.
운영 의존성과 개발 의존성을 dependency group으로 구분할 수 있다.
Docker 환경에서 uv sync --locked 기반 설치 흐름을 만들 수 있다.
Poetry보다 명령 흐름이 단순하고, pip 호환 명령도 제공한다.
```

채택하지 않은 선택지:

```text
requirements.txt:
- 단순하지만 lock 파일과 개발 의존성 분리가 약하다.
- Flask 튜토리얼에는 적합하지만 Docker/OCI 장기 유지 프로젝트에는 아쉽다.

Poetry:
- 충분히 좋은 선택지지만 이 프로젝트에서는 uv보다 무겁게 느껴질 수 있다.
- Docker 빌드 흐름에서 uv가 더 단순한 선택이 될 가능성이 높다.
```

교육적 의미:

```text
학생들에게 단순 pip install만 보여주는 것보다 pyproject.toml, lock file, dev dependency, reproducible install 흐름을 설명할 수 있다.
다만 처음부터 모든 내부 동작을 파고들지 않고, 프로젝트 유지보수에 필요한 수준까지만 다룬다.
```

## 7. 개발 원칙

```text
운영 버전 안정성 침해 금지
정책 변경은 명시적 승인 후 반영
DB 구조 변경은 Alembic migration으로 관리
권한 검증은 서버에서 수행
프론트 검증은 UX 보조일 뿐 보안 검증이 아님
기능 추가와 리팩토링을 섞지 않음
테스트 통과 전 다음 Phase로 진행하지 않음
```

추가 개발 원칙:

```text
작업 단위는 사용자가 이해하고 검토할 수 있는 크기로 제한한다.
AI가 작성한 코드는 사용자가 직접 읽고 적용한다.
작동하는 결과만이 아니라 왜 그렇게 작동하는지도 확인한다.
각 단계는 실행 결과 확인 후 다음 단계로 넘어간다.
```

## 8. MVP 범위

MVP에 포함한다.

```text
사용자 인증
senedu.kr 도메인 제한
사용자/권한 관리
미등록 사용자 등록 요청
예약 생성
예약 충돌 검증
충돌 확인 후 저장
즉시 사용 시작
사용 완료
예약 취소
Settings 관리
GuideItems 관리
CSV 템플릿 다운로드
CSV 업로드
CSV 서버 검증
CSV all-or-nothing 저장
CSV 업로드 이력
CSV 검증 실패 로그
기본 관리자 화면
기본 테스트
Docker Compose 실행
```

## 9. MVP 이후 백로그

MVP 이후로 분리한다.

```text
CSV 템플릿 버전 관리
고급 관리자 대시보드
상세 감사 로그 전체화
예약 통계 고도화
OCI 자동 배포 스크립트
백업 자동화
이메일/알림 기능
Credential Delivery 정책
```

## 10. 권한 정책

### 역할

```text
admin
subadmin
user
```

### 기본 원칙

```text
등록된 사용자만 시스템을 사용할 수 있다.
비활성 사용자는 예약 시스템을 사용할 수 없다.
관리자 기능은 서버에서 권한 검증을 수행한다.
최소 1명의 활성 admin을 유지한다.
마지막 활성 admin 비활성화 금지.
마지막 활성 admin 권한 제거 금지.
```

## 11. 보안 정책

### GPT 계정 정보

기본 정책은 다음과 같다.

```text
GPT 계정 ID 저장 금지
GPT 비밀번호 저장 금지
공용 계정 접속 정보를 DB/Settings/GuideItems에 저장하지 않음
```

운영상 “예약 성공 후 계정 ID/PW를 안내”하는 방식은 보안 위험이 크므로 MVP에는 포함하지 않는다.

사유:

```text
앱이 사실상 비밀번호 저장소가 된다.
DB, 로그, 화면, 브라우저 캐시, 스크린샷을 통해 노출될 수 있다.
권한 오류 또는 XSS가 발생하면 계정 정보가 바로 유출된다.
공용 계정 비밀번호 변경/회수/감사 관리가 어려워진다.
```

예외 정책:

```text
운영상 반드시 필요하다고 판단되면 별도 Phase에서 Credential Delivery 정책으로 분리한다.
그 경우에도 DB에 평문 저장하지 않는다.
Settings/GuideItems에 저장하지 않는다.
로그에 남기지 않는다.
노출 시점과 대상을 예약 승인 사용자로 제한한다.
OCI Vault 또는 별도 Secret 관리 방식을 검토한다.
별도 승인 전에는 구현하지 않는다.
```

### 민감정보 입력 방지

```text
개인정보 입력 금지 안내
민감정보 입력 금지 안내
평가자료 입력 금지 안내
학생부 자료 입력 금지 안내
학교 내부 보안자료 입력 금지 안내
```

### XSS 방지

```text
사용자 입력값 출력 시 escape 처리
GuideItems HTML 실행 금지
Settings 안내 문구 escape 처리
innerHTML 직접 삽입 금지
신뢰할 수 없는 값은 DOM에 직접 삽입하지 않음
```

## 12. 데이터 모델 초안

기존 Apps Script 시트 구조를 PostgreSQL 테이블로 이관한다.

```text
Users                  → users
Reservations           → reservations
UsageLog               → usage_logs
GuideItems             → guide_items
Settings               → settings
RegistrationRequests   → registration_requests
SettingsLog            → settings_logs
```

Flask 버전에서 추가할 테이블:

```text
csv_upload_logs
csv_validation_errors
```

후속 또는 최소 범위로 검토할 테이블:

```text
admin_action_logs
```

## 13. 테이블 초안

### users

```text
id
email
name
department
extension
role
active
is_auth_manager
sort_order
created_at
updated_at
```

### reservations

```text
id
user_id
title
description
start_at
end_at
status
conflict_confirmed
started_at
ended_at
cancelled_at
created_at
updated_at
```

### usage_logs

```text
id
reservation_id
user_id
started_at
ended_at
duration_minutes
created_at
```

### guide_items

```text
id
category
title
content
sort_order
active
created_at
updated_at
```

### settings

```text
id
setting_key
setting_value
value_type
required
description
created_at
updated_at
```

### registration_requests

```text
id
email
name
department
extension
status
reject_reason
requested_at
processed_at
processed_by
```

### settings_logs

```text
id
setting_key
old_value
new_value
changed_by
changed_at
```

### csv_upload_logs

```text
id
filename
uploaded_by
total_rows
success_rows
failed_rows
status
created_at
```

### csv_validation_errors

```text
id
upload_log_id
row_number
field_name
error_message
raw_row
created_at
```

## 14. 주요 화면

```text
로그인 화면
미등록 사용자 등록 요청 화면
대시보드
예약 생성 화면
오늘 예약/내 예약 화면
현재 사용 상태 화면
관리자 사용자 관리 화면
관리자 CSV 업로드 화면
관리자 CSV 이력/실패 로그 화면
관리자 Settings 화면
관리자 GuideItems 화면
```

## 15. 주요 Route 초안

### Public/Auth

```text
GET  /
GET  /login
GET  /auth/google
GET  /auth/callback
POST /logout
```

### Dashboard/Reservation

```text
GET  /dashboard
GET  /reservations
POST /reservations
POST /reservations/<id>/start
POST /reservations/<id>/finish
POST /reservations/<id>/cancel
DELETE /admin/reservations/<id>
```

### Registration

```text
GET  /registration-request
POST /registration-request
GET  /admin/registration-requests
POST /admin/registration-requests/<id>/approve
POST /admin/registration-requests/<id>/reject
```

### User Admin

```text
GET  /admin/users
POST /admin/users
POST /admin/users/<id>
POST /admin/users/<id>/activate
POST /admin/users/<id>/deactivate
```

### CSV

```text
GET  /admin/users/csv-template
POST /admin/users/csv-upload
GET  /admin/users/csv-uploads
GET  /admin/users/csv-uploads/<id>
```

### Settings / GuideItems

```text
GET  /admin/settings
POST /admin/settings
GET  /admin/guide-items
POST /admin/guide-items
```

### Health

```text
GET /healthz
```

## 16. CSV 정책

### CSV 컬럼

```text
email,name,department,extension,role,active,is_auth_manager,sort_order
```

### 검증 정책

```text
email 필수
name 필수
department 필수
senedu.kr 도메인
CSV 내부 이메일 중복 방지
기존 사용자 이메일 중복 방지
role 허용값 검증
active 허용값 검증
is_auth_manager 허용값 검증
sort_order 0 이상 정수 검증
```

### 저장 정책

```text
서버에서 최종 검증한다.
프론트 검증은 UX 보조다.
하나라도 실패하면 아무 사용자도 저장하지 않는다.
업로드 이력은 csv_upload_logs에 저장한다.
검증 실패 상세는 csv_validation_errors에 저장한다.
```

## 17. 테스트 전략

도구:

```text
pytest
```

필수 테스트:

```text
권한 테스트
사용자 관리 테스트
최소 활성 admin 유지 테스트
예약 충돌 테스트
예약 상태 전환 테스트
CSV 검증 테스트
CSV all-or-nothing 테스트
Settings 저장 테스트
GuideItems escape/XSS 테스트
Alembic migration 테스트
```

원칙:

```text
테스트 통과 전 다음 Phase로 진행하지 않는다.
백엔드 변경 시 테스트를 추가하거나 보강한다.
권한/보안 변경 시 회귀 테스트를 수행한다.
```



## 17-1. Phase Maintenance 원칙

리팩토링은 프로젝트 마지막에 몰아서 하지 않는다.

각 Phase 종료 시 `Phase Maintenance`를 수행한다.

목적:

```text
기능이 작동하는지 확인한다.
테스트가 통과하는지 확인한다.
리뷰하기 어려운 파일이 생겼는지 확인한다.
다음 Phase를 진행하기 전에 최소한의 구조 정리를 한다.
```

체크 기준:

```text
단일 파일 300줄 이상: 구조화 검토
단일 파일 500줄 이상: 강하게 분리 검토
함수 50줄 이상: 역할 분리 검토
하나의 파일이 여러 책임을 가지면 분리 검토
테스트 작성이 어려워지면 분리 검토
```

주의:

```text
Phase Maintenance는 대규모 리팩토링이 아니다.
기능 추가와 구조 변경을 한 번에 섞지 않는다.
테스트 없이 파일을 이동하지 않는다.
필요성이 명확하지 않은 패턴을 미리 도입하지 않는다.
```


## 18. Phase 로드맵

```text
Phase F-0: 명세서/설계
Phase F-1: 사용자가 직접 따라가는 Flask + Docker Compose 기본 골격
Phase F-2: SQLAlchemy 모델 + Alembic
Phase F-3: 인증/권한
Phase F-4: 사용자 관리
Phase F-5: 예약 시스템
Phase F-6: CSV 템플릿/업로드/검증 로그
Phase F-7: Settings / GuideItems
Phase F-8: 테스트/보안 점검
Phase F-9: OCI 배포
```



각 Phase는 기능 구현 후 바로 다음 Phase로 넘어가지 않고, 다음 순서를 따른다.

```text
기능 구현
→ 실행 확인
→ 테스트
→ Phase Maintenance
→ PROJECT_STATUS.md 갱신
→ 다음 Phase 진행 여부 판단
```

## 19. Phase F-1 진행 방식

Phase F-1은 Codex에게 전체 골격을 한 번에 만들게 하지 않는다.

권장 진행:

```text
Step 1. WSL2 Ubuntu에서 프로젝트 폴더 생성
Step 2. Git 초기화
Step 3. uv 설치/확인
Step 4. uv 프로젝트 초기화
Step 5. Flask 최소 앱 실행
Step 6. 개발 의존성 pytest 추가
Step 7. app factory 구조로 확장
Step 8. config/extensions/routes 구조 분리
Step 9. PostgreSQL docker-compose 추가
Step 10. /healthz로 DB 연결 확인
Step 11. Tailwind CLI 빌드 흐름 추가
Step 12. pytest 기본 테스트 추가
```

각 Step마다 다음을 확인한다.

```text
무엇을 만들었는가
왜 필요한가
어떤 파일이 바뀌었는가
어떻게 실행하는가
성공 기준은 무엇인가
다음 단계로 넘어가도 되는가
```

## 20. 모델/Codex 사용 계획

### Pro

사용 대상:

```text
초기 명세서
DB 구조 설계
권한 정책 설계
보안 정책 설계
OAuth 흐름 설계
Docker/OCI 배포 구조
Phase 분해
대규모 리팩토링 판단
배포 전 최종 점검
```

### 높음

사용 대상:

```text
백엔드 일반 구현 검토
Flask route/service 연결
복잡한 오류 분석
테스트 설계
서버-클라이언트 연동
```

### 중간

사용 대상:

```text
단순 CRUD
Jinja 화면
Vanilla JS 렌더링
반복 컴포넌트
문서 초안
```

### 즉시

사용 대상:

```text
브레인스토밍
문구 수정
Tailwind 조정
단순 HTML
README 일부 수정
간단한 설명
```

### Codex

사용 대상:

```text
반복적인 파일 생성 보조
코드 초안 제시
테스트 실행 보조
git diff 기반 리뷰 보조
오류 원인 후보 제시
```

Codex는 자동 구현자가 아니라 보조 개발자로 사용한다.

## 21. 승인 필요 항목

별도 승인 전 구현하지 않는다.

```text
GPT 계정 ID/PW 직접 안내 기능
Credential Delivery 정책
OCI Vault 또는 별도 Secret 관리
admin_action_logs 전체 범위 구현
CSV 템플릿 버전 관리
고급 관리자 대시보드
OCI 자동 배포 스크립트
백업 자동화
이메일/알림 기능
```
