# 멋쟁이 타자처럼 — 최종 Release Plan

확정일: 2026-09-13  
최종 통합/Release 목표: 2026-09-15  
운영 목표: 2026-09-19

> 이 문서는 2026-09-13 회의에서 확정한 최종 개발·운영 기준이다. 기존 기획/PR 제안과 충돌하면 이 문서의 Release 범위를 우선한다. 단, 실제 코드가 아직 반영되지 않은 항목은 9/15 통합 대상이며 문서만으로 구현 완료를 의미하지 않는다.

## 1. Production 기준선

- Frontend/Backend의 실제 통합 기준선은 `develop`이다.
- 기존 Frontend PR #3, #4, #5는 통째로 merge하지 않는다.
- 각 PR의 필요한 기능/UI만 최신 `develop`에서 새 브랜치를 만들어 이식한다.
- 검증된 Production API/session/recovery 구조는 유지한다.

## 2. 최종 UI / UX

- 최종 디자인: 라디오 / ON AIR 스타일.
- Landing 포함 사용자 UI는 기획디자인팀 전달안을 최종 시각 기준으로 사용한다.
- 디자인 변경이 Backend 계약이나 공식 기록 정책을 변경해서는 안 된다.

### Game Core 최종 채택

PR #4에서 아래 UX를 모두 반영한다.

- 한글 자모 단위 입력 표시
- 오타 위치 표시
- 실시간 타수
- 자동 포커스 복구
- 진행률 표시
- 3초 카운트다운
- 타이핑 화면 연출

단, `sessionStorage`, 새로고침 복구, completion recovery, 중복 제출 방지, 실제 Backend API 구조는 현재 Production 방식을 유지한다.

## 3. 최종 사용자 흐름 / Target Routes

```text
/
  Landing

/participate
  참가자 정보 입력

/categories
  카테고리 선택

/game/:categoryId
  게임

/result/:gameSessionId
  결과 / completion recovery

/rankings
  공개 랭킹

/admin
  운영진
```

- 결과 화면은 게임 내부 상태가 아니라 별도 `/result/:gameSessionId` route로 유지한다.
- 참가자 화면에서는 Admin 진입 버튼을 제거한다.
- 운영자는 `/admin`으로 직접 접근한다.

## 4. 참가 / 이용권 정책

- 전화번호 1개당 닉네임 1개.
- 최초 참가자는 전체 서비스 기준 FREE 1회.
- FREE를 어느 카테고리에서 사용해도 다른 카테고리의 추가 FREE는 없다.
- 재도전은 500원 결제 확인 후 Admin이 PAID 이용권을 발급한다.
- PAID 재도전 횟수는 발급된 이용권 기준으로 처리한다.
- 이용권 사용 가능 여부의 최종 판단은 Backend가 담당한다.

## 5. 기록 / 랭킹 정책

- 공식 완료 기록은 정수 millisecond `elapsedMs`이다.
- 재도전 GameSession은 각각 저장한다.
- 랭킹에는 참가자별/카테고리별 `COMPLETED` 기록 중 가장 빠른 기록만 사용한다.
- 느린 최신 기록이 기존 Personal Best를 덮어쓰지 않는다.
- PB, 공식 기록 인정 여부, 현재 순위는 Backend가 최종 결정한다.
- Ranking UI는 select가 아니라 카테고리 탭/버튼 방식으로 구성한다.

## 6. Admin 최종 범위

이번 Release에서 Admin이 지원하는 기능은 아래 4개뿐이다.

1. 관리자 로그인
2. 전화번호 또는 닉네임 기반 참가자 조회
3. 결제 확인 후 PAID 이용권 발급
4. 문제 GameSession 무효화 + 필요 시 이용권 복구

이번 Release에서 지원하지 않는 기능:

- 닉네임 변경
- 전화번호 수정
- 참가자 삭제
- 기록 시간/순위 직접 수정
- 이용권 삭제/환불/별도 취소
- standalone pass restore
- 등록 마감 ON/OFF
- 카테고리/문장 수정
- DB 초기화 버튼

## 7. Production 콘텐츠 Freeze

Backend Production DB가 콘텐츠 Source of Truth이다.

### CH01 — 성결대 멋사

1. `안녕하세요 성결대학교 멋쟁이사자처럼입니다!`
2. `프론트엔드 백엔드 기획디자인 세 부서가 한 팀이 됩니다`
3. `상상을 코드로 아이디어를 현실로 만드는 개발동아리!`
4. `함께 고민하고 함께 성장합니다`
5. `저희의 아기사자가 되어주세요!`

### CH02 — 멋쟁이사자처럼

1. `전국 약 80개 대학이 함께하는 멋쟁이사자처럼`
2. `대표 활동은? 바로 해커톤입니다`
3. `제한된 시간 폭발하는 아이디어!`
4. `오늘의 버그가 내일의 실력이 됩니다`
5. `당신의 도전을 기다립니다 아기사자님!`

### CH03 — 페스티벌 라디오

1. `기다리던 동아리 페스티벌 오늘만큼은 마음껏 즐겨볼까요!`
2. `좋아하는 노래가 들려오면 친구와 함께 신나게 따라 불러보세요.`
3. `처음 듣는 노래도 이런 날 들으면 왠지 좋아지는 것 같아요!`
4. `신나는 음악과 웃음소리가 가득한 지금 이 순간을 제대로 즐겨봐요.`
5. `오늘 함께 들었던 노래와 추억은 오래 남을 거예요!`

문장의 띄어쓰기와 문장부호를 임의로 수정하지 않는다.

## 8. Mock 정책

Production runtime에서는 Mock 데이터를 사용하지 않는다.

- Mock Category: 금지
- Mock Sentence: 금지
- Mock Participant: 금지
- Mock Ranking: 금지
- Mock GameSession: 금지

MSW/fixture는 테스트 환경에서만 허용한다.

## 9. Frontend 담당별 통합 핵심

### Admin 담당

- 참가자 조회
- PAID 이용권 발급
- 경기 무효화 + 이용권 복구

### Participant / Ranking 담당

- 잘못된 참가자 정보 입력 오류 안내
- 새로고침 후 참가자 정보 유지
- 카테고리 선택형 Ranking

### Game Core 담당

- 한글 자모 단위 표시
- 오타 위치 표시
- 실시간 타수
- 자동 포커스 / 진행률 / 카운트다운 / 타이핑 연출

## 10. 행사 화면 대응 범위

Primary QA viewport:

- 1920px
- 1280px

모바일 최적화보다 행사 PC 완성도를 우선한다.

필수 확인:

- 긴 문장 줄바꿈
- 게임 화면 높이/스크롤
- 입력 포커스
- Ranking 가독성
- 버튼 위치
- 화면 잘림

## 11. Done / QA 기준

최종 통합은 아래 검증을 통과해야 한다.

- lint
- unit/component test
- production build
- 실제 Backend E2E
- Korean IME composition
- 오타 수정 / Backspace / 빠른 Enter
- 시작/완료 중복 요청 방지
- refresh / browser back
- completion recovery
- network failure
- participant session 유지
- category ranking
- FREE/PAID/no-pass
- nickname mismatch

화면 렌더링만으로 Done 처리하지 않는다.

## 12. 신규 기능 Freeze

지금부터 신규 기능 추가는 중단한다.

허용:

- 최종 UI 통합
- 기존 기능 이식
- 버그 수정
- P0/P1 수정
- 보안/Production 장애 수정
- QA

금지:

- 있으면 좋은 추가 기능
- 새로운 Admin 기능
- 새로운 Backend API
- 대규모 구조 변경
- 새로운 게임 모드

## 13. Git / Release 전략

```text
최신 develop
  ├─ feat/final-game-ui
  ├─ feat/final-participant-ranking-ui
  └─ feat/final-admin-ui
        ↓
      PR / QA
        ↓
      develop
        ↓
2026-09-15 Release PR
        ↓
       main
```

- `main` 직접 push 금지.
- 9/15 최종 통합·검증 후 `develop → main` Release PR을 사용한다.

## 14. 운영 안정화

9/15 Release 이후 순서:

1. Domain 연결
2. HTTPS/TLS
3. 실제 HTTPS origin으로 CORS 고정
4. 실제 행사 PC / Korean IME QA
5. Admin 운영 리허설
6. FREE → PAID 재도전 → Ranking 전체 리허설
7. 행사 직전 테스트 데이터 정리

Production API base는 same-origin `/api`를 유지한다.

## 15. 보안 / 운영 원칙

- Admin은 HTTPS 적용 전 공용 네트워크에서 사용하지 않는다.
- Admin 비밀번호/DB/AWS secret은 GitHub, Frontend bundle, 단체 채팅에 남기지 않는다.
- 관리자 접근은 행사에 필요한 최소 인원만 허용한다.
- 현재 AWS 관리자 권한은 안정화 후 least privilege로 축소한다.
- 행사 테스트 데이터는 즉석 SQL 삭제가 아니라 백업 → 대상 확인 → 정리 → 무결성 확인 절차로 처리한다.
- 참가자 전화번호 등 개인정보는 행사/상품 지급에 필요한 기간 이후 삭제 일정을 확정하여 정리한다.

## 16. 최종 일정

- 09/13: 정책/개발 방향 확정
- 09/14: 최신 `develop` 기반 최종 코드 이식 및 통합 PR
- 09/15: 전체 QA, `develop → main`, 최종 Release
- 09/16~09/18: Domain/HTTPS/CORS/행사 PC/Admin 운영 리허설
- 09/19: 행사 운영

## 17. 최종 원칙

> Frontend는 사용자 경험과 시간 측정을 담당하지만, FREE/PAID 이용권, GameSession, 공식 기록, Personal Best, Ranking의 최종 권한은 Backend에 있다.

> 9/15 이후에는 기능을 더 만드는 것보다 실제 행사에서 실패하지 않는 것을 최우선으로 한다.
