# Tech Stack Decisions

## 1. 문서 목적

이 문서는 `gpt-share-manager` 프로젝트의 주요 기술 선택 이유를 기록한다.

이 프로젝트는 단순히 최신 도구를 쓰기 위한 프로젝트가 아니다. 사용자가 전체 개발 프로세스를 이해하고, 나중에 학생들에게 설명할 수 있는 방식으로 기술을 선택한다.

## 2. Python 의존성 관리

### 후보

```text
pip + requirements.txt
Poetry
uv
```

### 채택

```text
uv
```

### 채택 이유

```text
pyproject.toml 기반으로 프로젝트 메타데이터와 의존성을 함께 관리할 수 있다.
uv.lock을 통해 로컬, WSL2, Docker, OCI 환경에서 의존성을 재현하기 쉽다.
운영 의존성과 개발 의존성을 dependency group으로 구분할 수 있다.
uv run으로 프로젝트 가상환경 안에서 명령을 실행할 수 있다.
Docker 빌드에서 uv sync --locked 흐름을 사용할 수 있다.
Poetry보다 명령 흐름이 단순하고 pip 호환 인터페이스도 제공한다.
```

### 채택하지 않은 이유

#### pip + requirements.txt

```text
장점:
- 단순하다.
- Flask 튜토리얼 자료가 많다.

단점:
- lock 파일 관리가 약하다.
- 운영/개발 의존성 분리가 불편하다.
- Docker/OCI 장기 유지 프로젝트에서는 재현성 관리가 약하다.
```

#### Poetry

```text
장점:
- pyproject.toml 기반 관리가 가능하다.
- lock 파일이 있다.
- Python 프로젝트 관리 도구로 충분히 검증되어 있다.

단점:
- 이 프로젝트에서는 uv보다 명령 흐름이 무겁게 느껴질 수 있다.
- Docker 빌드에서 uv가 더 단순한 선택이 될 가능성이 높다.
```

## 3. F-1에서 사용할 최소 uv 명령

```bash
uv --version
uv init --app --bare
uv add flask
uv add --dev pytest
uv run flask --app app run --debug
uv run pytest
```

## 4. 원칙

```text
requirements.txt를 직접 관리하지 않는다.
pyproject.toml과 uv.lock을 원본 의존성 정의로 본다.
uv.lock은 Git에 포함한다.
.venv는 Git에 포함하지 않는다.
requirements 형식이 필요하면 uv export로 생성한다.
```

## 5. 교육적 의미

이 선택은 학생들에게 다음 개념을 설명하는 데 도움이 된다.

```text
가상환경
의존성 선언
개발 의존성과 운영 의존성
lock file
재현 가능한 실행 환경
로컬 실행과 Docker 실행의 차이
```

도구 자체보다 중요한 것은 다음이다.

```text
왜 의존성을 관리해야 하는가?
왜 lock file이 필요한가?
왜 내 컴퓨터와 서버의 환경 차이가 문제가 되는가?
```


## 6. 구조화 방식 선택

### 후보

```text
처음부터 완성형 아키텍처 구성
단일 파일로 오래 유지 후 마지막에 리팩토링
점진적 구조화 + Phase Maintenance
```

### 채택

```text
점진적 구조화 + Phase Maintenance
```

### 채택 이유

```text
초기 학습 단계에서 코드 흐름을 파악하기 쉽다.
구조화의 필요성을 경험한 뒤 분리할 수 있다.
파일이 너무 커져 리뷰를 포기하는 문제를 줄일 수 있다.
AI 자동 생성 구조를 맹목적으로 수용하지 않게 한다.
학생 수업으로 확장하기 좋다.
```

### 채택하지 않은 이유

#### 처음부터 완성형 아키텍처 구성

```text
겉보기에는 전문적이지만 초급 학습자에게는 흐름 파악이 어렵다.
왜 분리했는지 모르면 폴더 구조 암기가 된다.
AI가 만든 구조를 이해하지 못한 채 유지보수할 위험이 있다.
```

#### 단일 파일로 오래 유지 후 마지막에 리팩토링

```text
파일이 커지면 리뷰 자체를 하지 않게 된다.
수정 영향 범위가 커진다.
마지막 리팩토링의 위험이 너무 커진다.
```

### 원칙

```text
구조화는 필요가 생긴 뒤 최소 범위로 수행한다.
각 Phase 종료 시 Phase Maintenance를 수행한다.
테스트 없이 구조를 바꾸지 않는다.
```
