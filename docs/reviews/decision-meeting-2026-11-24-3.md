# 결정 회의 기록 · 2026-11-24 (3) 데이터 접근 · 테스트 규칙

> 개발 저장소의 기존 스택(Spring MVC · Spring Data JPA · Spring Security 세션 · Flyway · MySQL 8.4 · Gradle)을 점검한 결과다. 스택은 그대로 쓰고 아래 두 가지를 보완한다. 자세한 내용은 [`ARCHITECTURE.md`](../ARCHITECTURE.md) 「데이터 접근 · 테스트」.

| 주제 | 결정 | 이유 |
| --- | --- | --- |
| 집계 쿼리 | 상태 변경은 JPA, **집계 · 추천 계산은 네이티브 SQL**로 쓴다. 쿠폰 총수량은 조건부 UPDATE로 원자 처리한다 | 수락률 · 이동 · 세그먼트 · 추천 점수는 GROUP BY · 서브쿼리가 많아 JPQL로는 복잡하고 느림. 조건부 UPDATE가 낙관적 락 재시도보다 단순하고 확실함 |
| 테스트 DB | **Testcontainers**로 실제 MySQL 8.4를 띄운다. H2로 대신하지 않는다 | 각자 로컬 DB를 맞출 필요가 없고 Flyway 마이그레이션도 검증됨. H2는 MySQL 문법 차이로 집계 쿼리에서 어긋남 |
