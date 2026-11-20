# {{SERVICE}} 기획 저장소 — Claude Code 진입점

골목 상권 공동 예약 CRM의 기획 문서 저장소. 코드와 API 계약은 개발 저장소 [Leave-421/alley-crm](https://github.com/Leave-421/alley-crm)에 있다.

## 문서 지도

| 파일 | 내용 |
| --- | --- |
| `docs/plan/v1 결정 정리.md` | 기획 확정본 (기준) |
| `docs/reviews/` | 결정 회의 · 점검 기록 (날짜 늦은 것이 우선, 고치지 않고 덧붙임) |
| `docs/00-backlog.md` ~ `07-screens.md` | 백로그 · 문제 · 흐름 · 요구사항 · 기능 · 정책 · 데이터 · 화면 |
| `docs/PRD.md` · `ARCHITECTURE.md` · `requirements-changes.md` | 제품 요약 · 구조 · 요구사항 변경 이력 |
| `docs/plan/` | Git 전략 · 코드 컨벤션 · 환경 변수 가이드 |
| `docs/research/` | 조사 자료 (결정 문서 아님, 근거 참고용) |

## 원칙

- 결정 기록에 없는 결정을 대신 내리지 않는다. 기준 문서로 답이 정해지지 않으면 사용자에게 묻는다.
- 요구사항 ID · 우선순위 · 번호는 결정 기록이 명시할 때만 바꾼다.
- 문서 정합성 작업은 `doc-editor` 에이전트, 팀원 리뷰 글 정리는 `review-brief` 스킬을 쓴다.
- v1 제외 항목(캠페인 발송 · 쿠폰 · 노쇼 기능)을 요구사항으로 되살리지 않는다(결정 회의 기록이 있을 때만).
- **사용자가 요청하기 전에는 commit · push · PR 생성 · merge를 하지 않는다.**

## AI 협업자 · 기여자 등록 금지

Claude Code · AI 계정을 Collaborator · Assignee · Reviewer · CODEOWNERS · 커밋 Author · `Co-authored-by`에 넣지 않고, "Generated with Claude Code" 문구를 넣지 않는다. `git config user.name` · `user.email`을 바꾸지 않는다.
