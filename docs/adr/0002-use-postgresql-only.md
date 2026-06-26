# ADR 0002: PostgreSQL only로 개발

## 상태

승인됨

## 맥락

최종 목표 DB가 PostgreSQL이며, SQLite를 병행하면 타입, 제약조건, 동시성, migration 차이로 혼란이 생길 수 있다.

## 결정

개발 단계부터 PostgreSQL을 사용한다. SQLite는 도입하지 않는다.

## 대안

- 개발 SQLite + 운영 PostgreSQL
- PostgreSQL only

## 결과

초기 Docker Compose 설정이 필요하지만, 로컬과 운영 환경의 차이를 줄일 수 있다.
