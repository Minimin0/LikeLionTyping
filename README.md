# LikeLionTyping

멋쟁이 타자처럼은 축제 방문객이 세 가지 라디오 채널 중 하나를 선택하고,
정해진 문장을 입력해 완료 기록을 경쟁하는 타자 게임 서비스입니다.

## Final Release 기준

2026-09-13 회의에서 9/15 최종 통합·Release 기준을 확정했습니다.

- 최종 통합/Release: **2026-09-15**
- 운영 목표: **2026-09-19**
- 통합 기준: Frontend / Backend `develop`
- 최종 UI: **라디오 / ON AIR 스타일**
- 신규 기능: 사실상 Freeze, 최종 UI 통합·버그 수정·QA 중심
- 자세한 기준: [docs/FINAL_RELEASE_PLAN_2026-09-13.md](docs/FINAL_RELEASE_PLAN_2026-09-13.md)

> 위 Release Plan은 기존 제안/PR 설명과 충돌하는 경우 9/15 Release 범위의 최종 기준으로 사용합니다. 실제 코드가 아직 반영되지 않은 항목은 9/15 통합 대상입니다.

## Repositories

| Area | Repository | Role |
| --- | --- | --- |
| Frontend | [Minimin0/LikeLionTyping-Frontend](https://github.com/Minimin0/LikeLionTyping-Frontend) | React + Vite + TypeScript Client |
| Backend | [Minimin0/LikeLionTyping-Backend](https://github.com/Minimin0/LikeLionTyping-Backend) | Java + Spring Boot + MySQL API |
| Project Hub | [Minimin0/LikeLionTyping](https://github.com/Minimin0/LikeLionTyping) | 기획 / 문서 / QA / Release 관리 |

## Technology

Frontend
- React
- Vite
- TypeScript
- React Router
- TanStack Query
- Axios
- Vitest / React Testing Library

Backend
- Java 21
- Spring Boot
- Gradle
- MySQL
- Flyway
- Spring Security

Infrastructure
- AWS EC2
- Nginx
- Spring Boot / MySQL loopback 운영

## 확정 서비스 정책

- 최초 참가자는 전체 서비스 기준 FREE 1회
- 재도전은 500원 결제 확인 후 Admin이 PAID 이용권 발급
- 전화번호 1개당 닉네임 1개
- 재도전 기록은 누적 저장하지만 Ranking에는 카테고리별 개인 최고 기록만 반영
- Production 콘텐츠는 3개 카테고리 / 15개 문장으로 Freeze
- Admin 범위는 로그인 / 참가자 조회 / PAID 발급 / 경기 무효화+이용권 복구

## Schedule

- 09/13: 정책 / 최종 개발 방향 확정
- 09/14: 최신 `develop` 기반 최종 코드 이식 및 통합 PR
- 09/15: 최종 통합, 전체 QA, `develop → main` Release
- 09/16~09/18: Domain / HTTPS / CORS / 행사 PC / 운영 리허설
- 09/19: Production 운영

## Development Flow

`main`은 최종 Release 기준 브랜치, `develop`은 통합 개발 브랜치입니다.
기능 개발은 `feat/*`, 버그 수정은 `fix/*`, 설정/문서 작업은 `chore/*` 또는 `docs/*`에서 진행합니다.

```text
feat/* / fix/* / docs/*
↓
Pull Request
↓
develop
↓
Integration / QA
↓
Release PR
↓
main
```

`main` 직접 push는 하지 않습니다.
