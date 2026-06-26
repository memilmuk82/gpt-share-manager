# GPT Share Manager - Project Instructions

## 1. 문서 목적

이 문서는 `gpt-share-manager` 프로젝트의 작업 원칙을 정의한다.

이 프로젝트는 기존 Google Apps Script 기반 GPT 공동 사용 예약 시스템의 Flask + PostgreSQL + Docker/OCI 후속 버전이다.

이 문서는 다음 대상이 지켜야 할 기준이다.

```text
개발자
ChatGPT
Codex
추후 새 대화창
추후 유지보수자
```

## 2. 최우선 철학

이 프로젝트의 핵심 철학은 다음과 같다.

```text
AI가 개발자를 대체하지 않는다.
AI는 개발자의 이해와 판단을 보조한다.
모든 개발 프로세스의 최종 통제권은 사용자에게 있다.
```

이 프로젝트는 AI 자동 생성 결과물을 그대로 수용하는 방식으로 진행하지 않는다.

사용자는 코드를 직접 읽고, 적용하고, 실행하고, 결과를 확인한다. AI는 설계 보조, 코드 초안 제시, 오류 분석, 코드 리뷰, 대안 비교를 담당한다.

이 원칙을 두는 이유:

```text
AI 도구가 바뀌어도 유지보수할 수 있어야 한다.
코드 흐름을 이해하지 못한 상태로 앱만 완성하지 않는다.
학생들에게 설명 가능한 개발 과정을 남겨야 한다.
복사·붙여넣기 자체도 코드 리뷰와 학습 과정으로 본다.
```

## 3. 최우선 금지 사항

```text
승인 없는 기능 삭제 금지
승인 없는 정책 변경 금지
승인 없는 DB 구조 변경 금지
승인 없는 권한 정책 변경 금지
승인 없는 보안 완화 금지
승인 없는 대규모 리팩토링 금지
승인 없는 필요성 불명확한 선행 구조화 금지
테스트 없는 파일 이동/함수 이동 금지
테스트 없이 다음 Phase 진행 금지
GPT 계정 ID/PW 저장 금지
실제 사용자 CSV GitHub 업로드 금지
React/Vue/Svelte 임의 도입 금지
SQLite 임시 도입 금지
requirements.txt 중심 의존성 관리로 임의 회귀 금지
Codex 자동 커밋/자동 push 금지
Codex에게 전체 프로젝트를 한 번에 자동 생성시키는 방식 금지
```

## 4. 작업 전 필수 안내

모든 작업 전에는 먼저 아래 항목을 제시한다.

```text
이번 단계 목표
권장 작업 위치
- ChatGPT
- Codex
- VS Code 수동 수정

권장 추론 수준
- 즉시
- 중간
- 높음
- Pro

사용자 역할
AI 역할
변경 대상 파일
변경 대상 함수/위치
변경 이유
영향 범위
예상 부작용
검증 방법
다음 단계로 넘어가는 기준
```

예시:

```text
권장 작업 위치: VS Code 수동 수정 + ChatGPT 리뷰
권장 추론 수준: 중간
이유: 단일 파일의 최소 Flask 앱 생성 단계이며, 사용자가 직접 실행 결과를 확인하는 것이 학습에 적합함
```

또는

```text
권장 작업 위치: ChatGPT
권장 추론 수준: Pro
이유: DB 구조와 권한 정책에 영향을 주는 설계 작업임
```

## 5. 코드 제시 원칙

코드는 다음 방식으로 제시한다.

```text
필요한 파일만 제시한다.
파일 전체 출력은 피한다.
바뀌는 최소 블록만 제시한다.
과한 주석을 달지 않는다.
복붙 가능한 단위로 제시한다.
코드보다 먼저 변경 이유와 검증 방법을 설명한다.
```

코드 제시 기본 형식:

```text
이번 단계 목표
변경 파일
변경 위치
왜 필요한가
작성할 코드
실행 명령어
기대 결과
오류 시 확인할 지점
다음 단계 기준
```

사용자가 원하지 않는 방식:

```text
전체 앱을 한 번에 생성
수십 개 파일을 한 번에 생성
코드 한 줄마다 과도한 주석 추가
사용자가 이해하지 못한 상태에서 다음 단계 진행
작동만 하면 된다는 식의 진행
```

## 6. 작업 방식 선택 원칙

### 6-1. 수동 패치 방식

다음 경우에는 사용자가 직접 붙여넣을 수 있도록 최소 코드만 제시한다.

```text
작은 함수 수정
단일 파일 수정
문구 수정
Tailwind 조정
간단한 Jinja 템플릿 수정
학습 가치가 큰 초기 환경 구성
```

원칙:

```text
파일 전체 출력 금지
바뀌는 최소 블록만 출력
변경 전/후 코드 구분
사용자가 직접 적용
사용자가 실행 결과 확인
```

### 6-2. Codex 보조 방식

Codex는 다음 경우에 사용한다.

```text
반복 파일 생성
테스트 실행
오류 로그 분석
import 경로 정리
여러 파일의 일관성 검토
git diff 요약
```

Codex 사용 원칙:

```text
Codex는 승인 전 파일을 수정하지 않는다.
Codex는 먼저 변경 계획을 제시한다.
사용자가 승인한 범위만 수정한다.
수정 후 git diff를 확인한다.
승인 전 commit 금지.
승인 전 push 금지.
```

### 6-3. Codex 브랜치 패치 방식

다음 경우에는 Codex가 승인 후 파일을 수정하고 사용자가 diff를 확인할 수 있다.

```text
여러 파일 수정
반복 CRUD 생성
테스트 코드 추가
SQLAlchemy 모델 생성
Alembic migration 생성
Dockerfile/docker-compose 수정
리팩토링
```

단, 이 방식도 자동 위임이 아니다.

```text
사용자가 요구사항을 이해해야 한다.
사용자가 diff를 검토해야 한다.
사용자가 테스트 결과를 확인해야 한다.
사용자 승인 후에만 commit한다.
```

### 6-4. 판단 기준

```text
작고 학습 가치가 큰 변경 → 수동 패치 방식
반복적이고 파일 수가 많은 변경 → Codex 보조 방식
설계/정책 판단 → ChatGPT
최종 보안/구조 리뷰 → ChatGPT
```

## 7. 모델 사용 계획

각 작업 전 권장 추론 수준을 먼저 안내한다.

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

사용 원칙:

```text
Pro는 전체 작업에 상시 사용하지 않는다.
Pro는 설계, 권한, 보안, DB, 배포, 최종 검토에 집중 사용한다.
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
파일 생성 보조
코드 패치 보조
테스트 실행 보조
반복 구현 보조
git diff 기반 검토
Docker 명령 실행
pytest 실행
Alembic migration 생성 보조
```

Codex는 자동 구현자가 아니라 보조 개발자다.

## 8. Python 의존성 관리 원칙

이 프로젝트는 `uv + pyproject.toml + uv.lock`을 기본 의존성 관리 방식으로 사용한다.

원칙:

```text
requirements.txt를 기본 의존성 관리 파일로 사용하지 않는다.
패키지 추가는 uv add를 우선 사용한다.
개발 전용 패키지는 uv add --dev를 사용한다.
명령 실행은 uv run을 우선 사용한다.
uv.lock은 Git에 포함한다.
.venv는 Git에 포함하지 않는다.
Docker 빌드에서는 uv sync --locked 기반 재현 설치를 목표로 한다.
```

기본 명령:

```bash
uv init --app --bare
uv add flask
uv add --dev pytest
uv run flask --app app run --debug
uv run pytest
```

외부 환경에서 requirements 형식이 꼭 필요한 경우:

```text
직접 requirements.txt를 수동 관리하지 않는다.
필요 시 uv export로 생성한다.
생성된 requirements 파일은 호환 목적의 산출물이며 원본 의존성 정의는 pyproject.toml과 uv.lock이다.
```

기술 선택 변경 규칙:

```text
uv에서 pip/Poetry로 변경하려면 별도 승인 필요.
Python 버전 변경은 F-1에서 로컬/OCI 호환성을 확인한 뒤 기록한다.
의존성 추가는 변경 이유와 운영/개발 의존성 구분을 먼저 설명한다.
```

## 9. Flask 구조 원칙

권장 구조:

```text
gpt-share-manager/
├─ app/
│  ├─ __init__.py
│  ├─ config.py
│  ├─ extensions.py
│  ├─ models/
│  ├─ routes/
│  ├─ services/
│  ├─ templates/
│  └─ static/
├─ migrations/
├─ tests/
├─ docker-compose.yml
├─ Dockerfile
├─ pyproject.toml
├─ uv.lock
├─ .python-version
├─ .env.example
├─ PROJECT_SPECIFICATION.md
├─ PROJECT_INSTRUCTIONS.md
└─ PROJECT_STATUS.md
```

원칙:

```text
route는 요청/응답 처리에 집중한다.
business logic은 services에 둔다.
DB 모델은 models에 둔다.
권한 검증은 route 또는 decorator에서 명확히 수행한다.
공통 확장은 extensions.py에서 초기화한다.
설정값은 config.py와 환경변수로 관리한다.
```



## 9-1. 점진적 구조화 원칙

이 프로젝트는 처음부터 완성형 구조를 강제하지 않는다.

기본 흐름:

```text
작동하는 코드 작성
→ 불편함 확인
→ 최소 범위 구조화
→ 테스트
→ 다음 기능 진행
```

원칙:

```text
처음에는 단순 구조를 허용한다.
구조화는 불편함이 명확해진 뒤 수행한다.
파일 분리는 학습과 리뷰를 돕는 범위에서만 수행한다.
필요성이 명확하지 않은 계층은 미리 만들지 않는다.
AI/Codex가 제안한 구조도 사용자가 이해하지 못하면 반영하지 않는다.
```

구조화 검토 기준:

```text
단일 파일 300줄 이상: 구조화 검토
단일 파일 500줄 이상: 강하게 분리 검토
함수 50줄 이상: 역할 분리 검토
같은 코드 반복: helper/service 분리 검토
테스트 작성 어려움: 책임 분리 검토
다음 기능 추가가 어려움: 구조화 검토
```

금지:

```text
처음부터 service/repository/model/form/schema 계층을 전부 만들지 않는다.
기능 추가와 대규모 리팩토링을 한 번에 수행하지 않는다.
테스트 없이 파일 이동을 하지 않는다.
패턴 이름이 멋있다는 이유로 도입하지 않는다.
```


## 10. SQLAlchemy / Alembic 원칙

```text
PostgreSQL only로 개발한다.
SQLite 임시 도입 금지.
DB 스키마 변경은 Alembic migration으로 관리한다.
수동 ALTER TABLE을 운영 절차로 사용하지 않는다.
migration 파일은 리뷰 대상이다.
migration 적용 전후 테스트를 수행한다.
```

모델 변경 시 보고 항목:

```text
변경 모델
변경 컬럼
nullable 여부
default 값
index/unique 제약
foreign key 영향
migration 필요 여부
기존 데이터 영향
rollback 가능성
```

## 11. PostgreSQL 원칙

```text
email은 unique로 관리한다.
role은 허용값을 검증한다.
boolean 값은 서버에서 엄격하게 normalize한다.
created_at/updated_at을 둔다.
중요한 관리자 작업은 로그를 남긴다.
CSV 업로드 결과와 실패 로그는 별도 테이블에 저장한다.
```

## 12. Frontend 원칙

```text
Jinja2 SSR + Vanilla JS + Tailwind를 사용한다.
React/Vue/Svelte를 임의 도입하지 않는다.
사용자 입력값 출력 시 escape 처리한다.
HTML 문자열을 실행하지 않는다.
innerHTML 사용 시 신뢰할 수 없는 값을 직접 삽입하지 않는다.
서버 검증을 프론트 검증으로 대체하지 않는다.
```

## 13. 보안 원칙

### GPT 계정 정보

```text
GPT 계정 ID 저장 금지
GPT 비밀번호 저장 금지
공용 계정 접속 정보를 DB/Settings/GuideItems에 저장하지 않음
```

예약 성공 후 계정 ID/PW를 안내하는 기능은 MVP에 포함하지 않는다.

별도 구현이 필요한 경우:

```text
Credential Delivery 정책으로 분리
별도 승인 필요
DB 평문 저장 금지
Settings/GuideItems 저장 금지
로그 저장 금지
노출 대상 제한
노출 시점 제한
Secret 관리 방식 검토
```

### 민감정보

```text
개인정보 입력 금지 안내 유지
민감정보 입력 금지 안내 유지
평가자료 입력 금지 안내 유지
학생부 자료 입력 금지 안내 유지
학교 내부 보안자료 입력 금지 안내 유지
```

### XSS

```text
사용자 입력 escape
GuideItems HTML 실행 금지
Settings 안내 문구 escape
innerHTML 직접 삽입 금지
```

## 14. 권한 원칙

```text
admin/subadmin/user 구조 유지
등록 사용자만 시스템 사용 가능
비활성 사용자는 예약 불가
관리자 기능은 서버에서 권한 검증
최소 1명의 활성 admin 유지
마지막 활성 admin 비활성화 금지
마지막 활성 admin 권한 제거 금지
```

관리자 route에는 반드시 권한 검증을 둔다.

## 15. CSV 원칙

```text
CSV 템플릿 다운로드는 MVP에 포함한다.
CSV 업로드는 서버에서 최종 검증한다.
프론트 파싱은 UX 보조다.
하나라도 실패하면 아무 사용자도 저장하지 않는다.
업로드 이력은 csv_upload_logs에 저장한다.
검증 실패 상세는 csv_validation_errors에 저장한다.
```

CSV 컬럼:

```text
email,name,department,extension,role,active,is_auth_manager,sort_order
```

검증 항목:

```text
email 필수
name 필수
department 필수
senedu.kr 도메인
CSV 내부 이메일 중복
기존 사용자 이메일 중복
role 허용값
active 허용값
is_auth_manager 허용값
sort_order 0 이상 정수
```

## 16. 테스트 원칙

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

보고 형식:

```text
실행한 테스트
전체 테스트 수
PASS 수
FAIL 수
실패 항목
원인
수정 후 재실행 결과
```

원칙:

```text
테스트 통과 전 다음 Phase 진행 금지.
백엔드 변경 시 테스트 추가 또는 보강.
보안/권한 변경 시 회귀 테스트 필수.
```

## 17. Docker / OCI 원칙

```text
로컬 Docker Compose 안정화 후 OCI 배포.
처음부터 OCI에서 개발하지 않는다.
환경변수는 .env.example에 예시만 둔다.
실제 .env는 GitHub에 올리지 않는다.
Docker 이미지 빌드는 pyproject.toml과 uv.lock을 기준으로 재현 가능하게 구성한다.
운영 secret은 별도 관리한다.
Nginx/Gunicorn/HTTPS는 OCI 배포 Phase에서 다룬다.
```

## 18. 문서 관리 원칙

### PROJECT_SPECIFICATION.md

역할:

```text
무엇을 만들지 정의
MVP 범위
제외 범위
기능 요구사항
데이터 모델
Route/API 초안
Phase 로드맵
AI 협업 개발 철학
```

### PROJECT_INSTRUCTIONS.md

역할:

```text
작업 원칙
승인 정책
코드 제시 방식
Codex 사용 원칙
모델 사용 계획
보안/권한/테스트 원칙
```

### PROJECT_STATUS.md

역할:

```text
현재 Phase
완료/미완료 작업
승인 완료 항목
별도 승인 필요 항목
테스트 상태
다음 작업
새 대화창 인수인계
```

## 19. Phase 진행 원칙

각 Phase는 다음 순서로 진행한다.

```text
1. 작업 전 권장 위치와 추론 수준 제시
2. 변경 대상/영향 범위/검증 방법 제시
3. 사용자 승인
4. 최소 단위 코드 제시 또는 Codex 보조 요청
5. 사용자가 코드 확인 후 적용
6. 실행 결과 확인
7. 테스트 결과 기록
8. PROJECT_STATUS.md 갱신
9. 다음 Phase로 이동 여부 판단
```



## 19-1. Phase Maintenance 원칙

각 Phase 종료 시 `Phase Maintenance`를 수행한다.

Phase Maintenance는 대규모 리팩토링이 아니라 다음 Phase를 진행하기 위한 최소 정리다.

수행 순서:

```text
1. 기능 동작 확인
2. 테스트 실행
3. 코드 리뷰
4. 파일 크기와 책임 확인
5. 필요한 최소 구조화
6. PROJECT_STATUS.md 갱신
7. 다음 Phase 위험 요소 기록
```

체크리스트:

```text
□ 기능이 의도대로 작동하는가
□ pytest 또는 수동 검증을 수행했는가
□ 단일 파일이 과도하게 길어지지 않았는가
□ 하나의 파일이 여러 책임을 갖고 있지 않은가
□ 긴 함수가 리뷰 가능한 크기인가
□ 중복 코드가 다음 Phase를 방해하지 않는가
□ 테스트 없이 파일 이동을 하지 않았는가
□ 기능 추가와 구조 정리를 섞지 않았는가
□ 사용자가 주요 파일 역할을 설명할 수 있는가
□ PROJECT_STATUS.md를 갱신했는가
```

AI/Codex에게 Phase Maintenance를 요청할 때는 다음 방식으로 요청한다.

```text
현재 구조에서 리뷰하기 어려운 부분을 찾아라.
전체 리팩토링이 아니라 최소 구조화만 제안해라.
변경 대상 파일과 영향 범위를 먼저 제시해라.
승인 전 파일을 수정하지 마라.
테스트 방법을 제시해라.
```


## 20. 새 대화창 인수인계 원칙

새 대화창에서는 다음 순서로 확인한다.

```text
1. PROJECT_SPECIFICATION.md 확인
2. PROJECT_INSTRUCTIONS.md 확인
3. PROJECT_STATUS.md 확인
4. 현재 Phase 확인
5. 승인 완료 항목 확인
6. 별도 승인 필요 항목 확인
7. 작업 전 권장 작업 위치와 추론 수준 제시
8. 변경 대상/영향 범위/검증 방법 제시
9. 승인 후 진행
10. 테스트 결과 보고
```

## 21. 최종 기준

이 프로젝트는 다음 상태를 목표로 한다.

```text
앱이 작동한다.
사용자가 앱 구조를 설명할 수 있다.
사용자가 주요 파일의 역할을 이해한다.
사용자가 AI가 제시한 코드를 리뷰할 수 있다.
사용자가 오류 발생 시 어디를 봐야 하는지 안다.
학생들에게 AI 협업 개발 과정을 설명할 수 있다.
```


추가 최종 기준:

```text
좋은 구조는 복잡한 구조가 아니다.
좋은 구조는 사용자가 설명할 수 있고, 테스트할 수 있고, 다음 기능을 추가할 수 있는 구조다.
파일을 열었을 때 리뷰를 포기하게 만드는 구조는 좋은 구조가 아니다.
```

## 문서 배치 원칙

문서도 코드처럼 역할에 따라 배치한다.

### 루트에 둘 문서

```text
README.md
PROJECT_SPECIFICATION.md
PROJECT_INSTRUCTIONS.md
PROJECT_STATUS.md
```

루트 문서는 새 대화창, 새 작업자, Codex 작업 전 반드시 먼저 확인해야 하는 기준 문서다.

### docs/에 둘 문서

```text
docs/architecture/   저장소 구조, ERD, API 구조, 배포 구조
docs/development/    Phase 계획, 개발 로그, 작업 기록
docs/guides/         Codex 프롬프트, 배포/운영 가이드
docs/decisions/      기술 선택과 AI 협업 방향 설명
docs/adr/            Architecture Decision Record
```

### 금지 사항

```text
문서를 편의상 루트에 계속 추가하지 않는다.
문서 위치를 바꿀 때는 링크와 참조 경로를 함께 수정한다.
PROJECT_STATUS.md를 docs/ 아래로 옮기지 않는다.
PROJECT_INSTRUCTIONS.md를 docs/ 아래로 옮기지 않는다.
PROJECT_SPECIFICATION.md를 docs/ 아래로 옮기지 않는다.
```

### ADR 원칙

중요한 기술 선택은 ADR로 남긴다.

예시:

```text
docs/adr/0001-use-uv.md
docs/adr/0002-use-postgresql-only.md
docs/adr/0003-human-controlled-ai-collaboration.md
docs/adr/0004-progressive-structuring.md
```

ADR은 길게 쓰지 않는다. 아래 항목만 기록한다.

```text
상태
맥락
결정
대안
결과
```
