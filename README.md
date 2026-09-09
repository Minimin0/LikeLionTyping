# LikeLionTyping

멋쟁이 타자처럼은 축제 방문객이 세 가지 라디오 채널 중 하나를 선택하고,
정해진 문장을 입력해 완료 기록을 경쟁하는 타자 게임 서비스입니다.

## Repositories

| Area | Repository | Role |
| --- | --- | --- |
| Frontend | [Minimin0/LikeLionTyping-Frontend](https://github.com/Minimin0/LikeLionTyping-Frontend) | React + Vite Client |
| Backend | [Minimin0/LikeLionTyping-Backend](https://github.com/Minimin0/LikeLionTyping-Backend) | Java + Spring Boot + MySQL API |
| Project Hub | [Minimin0/LikeLionTyping](https://github.com/Minimin0/LikeLionTyping) | 기획 / 문서 / QA / Release 관리 |

## Technology

Frontend
- React
- Vite

Backend
- Java 21
- Spring Boot
- Gradle
- MySQL
- Flyway

Infrastructure
- AWS EC2
- Nginx 예정

## Schedule

- 09/15: 각 파트 개발 완료
- 09/16~09/18: Integration / QA
- 09/19: Production 운영

## Development Flow

`main`은 운영 기준 브랜치, `develop`은 통합 개발 브랜치입니다.
기능 개발은 `feat/*`, 버그 수정은 `fix/*`, 설정/문서 작업은 `chore/*`에서 진행합니다.

```text
feat/*
↓
Pull Request
↓
develop
↓
Integration / QA
↓
main
```

`main` 직접 push는 하지 않습니다.
