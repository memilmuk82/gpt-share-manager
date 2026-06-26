# ADR 0005: Jinja2 + Vanilla JavaScript + Tailwind 사용

## 상태

승인됨

## 맥락

이 프로젝트는 관리자/예약 중심의 서버 렌더링 웹앱이며, React/Vue/Svelte 같은 SPA 구조는 초기 복잡도를 키운다.

## 결정

Jinja2 SSR + Vanilla JavaScript + Tailwind CSS를 사용한다.

## 대안

- React/Vue/Svelte SPA
- Jinja2 SSR + Vanilla JavaScript + Tailwind

## 결과

프론트 복잡도를 줄이고 기존 Apps Script Vanilla JS 경험을 이어갈 수 있다.
