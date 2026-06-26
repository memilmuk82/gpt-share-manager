# ADR 0001: uv를 Python 의존성 관리 도구로 사용

## 상태

승인됨

## 맥락

Flask + PostgreSQL + Docker Compose + OCI 배포를 목표로 하므로 로컬과 배포 환경의 의존성 재현성이 중요하다.

## 결정

`requirements.txt` 중심 관리 대신 `uv + pyproject.toml + uv.lock`을 사용한다.

## 대안

- pip + requirements.txt
- Poetry
- uv

## 결과

의존성 관리가 조금 낯설 수 있지만, lock file과 재현 가능한 실행 환경을 초기에 학습할 수 있다.
