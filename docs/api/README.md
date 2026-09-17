# API Contract

Frontend와 Backend가 공유하는 API 계약을 관리합니다.
현재 단계에서는 구현보다 Endpoint 기준점을 먼저 둡니다.

## Endpoint Candidates

```text
POST /api/participants/identify

GET /api/categories

POST /api/game-sessions

POST /api/game-sessions/{id}/complete

GET /api/rankings?categoryId={id}

POST /api/admin/login

GET /api/admin/dashboard

GET /api/admin/participants?query={phoneOrNickname}

POST /api/admin/participants/{id}/passes

POST /api/admin/game-sessions/{id}/invalidate
```
