# 이슈 백로그 · 분배안

> 상태: 2026-11-24. 담당 A ~ E를 실제 팀원에게 이었다: **A=@hhy0123 · B=@skinopero**(프론트), **C=@Choyeonik · D=@FG-Kaki · E=@JHee0209**(백엔드). 개발 저장소 이슈는 라벨 `owner:A` ~ `owner:E`와 Assignee가 같다. 리뷰 요청은 개발 저장소 `.github/CODEOWNERS`가 경로별로 보낸다.
> 기준: 화면은 [`07-screens.md`](07-screens.md), 서버 동작은 [`04-features.md`](04-features.md), 요구사항은 [`03-requirements.md`](03-requirements.md).
> 초벌이다. 작업하다 생기는 이슈는 같은 원칙으로 더한다. 기술 · 운영 결정은 [11-23 (9)](reviews/decision-meeting-2026-11-23-9.md), 기술 구성은 [`ARCHITECTURE.md`](ARCHITECTURE.md).

## 분배 원칙

1. 프론트 2명(A · B), 백엔드 3명(C · D · E).
2. **이슈 하나 = PR 하나 = 반나절 ~ 하루.** 하루를 넘길 것 같으면 쪼갠다.
3. 작업량을 비슷하게 맞춘다. 이슈 수가 아니라 무게로 본다(추천 계산, 가상 데이터 생성은 무거움).
4. 맡은 범위가 겹치지 않게 한다. 한 테이블 · 한 화면 · 한 공용 컴포넌트는 한 사람이 만든다. 다른 사람은 그것을 **쓰기만** 한다.
5. 선행 이슈(다른 이슈를 막는 것)를 한 사람에게 몰지 않는다. 1단계 선행은 사람마다 1 ~ 2개.

## 이슈 하나에 들어가는 것

- 프론트 화면 이슈: 07-screens 해당 절의 '꼭 있어야 할 것' 중 이 이슈 몫을 체크리스트로, 본문에 「목업과 다른 점」(07-screens 「확정 목업」, 각 화면 절의 「목업과 다른 점」 행).
- 백엔드 이슈: 해당 API 계약(개발 저장소 `CONTRACTS_API.md`)과 04-features 인수 조건 테스트. 테스트는 이슈를 따로 만들지 않고 각 이슈의 완료 조건에 넣는다.
- **요구사항 문장은 옮겨 적지 않는다.** 본문에는 문서 링크와 요구사항 · 화면 ID만 두고, 직접 적는 것은 체크리스트와 「목업과 다른 점」뿐이다. 요구사항이 바뀌면 문서만 고치고, 바뀐 ID로 이슈를 찾아(`gh issue list --search "FR-RSV-11"`) 체크리스트만 고친다.

## 누가 무엇을

| 담당 | 범위 | 이슈 수 | 무게 |
| --- | --- | --- | --- |
| A (프론트, @hhy0123) | 손님 화면, 골목 3D 스크롤 공용 컴포넌트와 지도를 쓰는 화면(손님 흐름 · 방문 흐름), 알림함 UI(손님 · 사장님 공용), 사장님 · 상인회 조회 화면 일부(예약 상세 · 건별 수수료 · 기금 적립 내역, 11-24 (5) 균형용) | 31 (여유 9) | 보드는 일러스트 기반(풀 3D 엔진 아님)이라 보통 |
| B (프론트, @skinopero) | 프론트 기반(설정 · 라우팅 · 공통 UI · API 클라이언트), 로그인 · 가입, 사장님 · 상인회 화면(지도 화면 제외), 시연 도구 | 29 (여유 4) | 화면은 많지만 표 · 지표 위주 |
| C (백엔드, @Choyeonik) | 백엔드 기반, 계정 · 가게 · 손님, 알림, 분석 | 23 (여유 4) | 영역은 넓고 계산은 가벼움 |
| D (백엔드, @FG-Kaki) | DB 기반 · 설정값 · 서버 시계, 예약, 가상 잔액, 수수료 · 정산 | 24 (여유 3) | 상태 규칙이 많음 |
| E (백엔드, @JHee0209) | 공공데이터 · 시드, 추천, 쿠폰, 소개 판정, 가상 데이터 생성 | 20 (여유 2) | 추천 계산 · 데이터 생성이 무거움 |

합계 127개(11-25 (5)로 14개 추가: A30 · A31 · B27 ~ B29 · C23 · D20 ~ D24 · E18 ~ E20, 개발 저장소 #159 ~ #172). 겹치는 곳은 '쓰기만' 한다.

- 3D 보드를 쓰는 화면(손님 지도, 손님 흐름, 방문 흐름)은 모두 A가 만든다. B는 사장님 · 상인회 메뉴에 붙이기만 한다(FR-MAP-02).
- 알림함 UI는 A가 손님 · 사장님 둘 다 만들고, B는 메뉴에 붙이기만 한다.
- 쿠폰 적용(E)은 D의 예약 API를 호출하고, D는 쿠폰 테이블을 직접 고치지 않는다.
- 소개 판정(E)은 코스 예약의 제안 ID · 기준 예약 ID(D)와 방문 처리(D)를 읽고, 수수료(D)는 소개 판정 결과를 읽는다.
- 분석(C)은 D · E의 테이블을 읽기만 한다.

## 1단계 선행

다른 이슈를 막는 것들이다. 사람마다 1 ~ 3개이고, B의 셋은 모두 반나절 크기다.

| A | B | C | D | E |
| --- | --- | --- | --- | --- |
| A1 골목 3D 스크롤 | B1 프론트 설정 · 라우팅, B2 디자인 토큰 · 기본 레이아웃, B3 API 클라이언트 · 목 서버 | C1 백엔드 설정 · 공통 응답, C2 로그인 · 역할 | D1 DB 기반 · 설정값, D2 예약 신청 | E1 권역 · 가게 시드 |

C1(백엔드 설정)은 D1 · E1보다 먼저라 첫날 끝낼 크기로 잡는다. D2(예약 신청)와 C2(로그인)는 다른 사람 이슈를 가장 많이 막는다. 둘 다 API 계약을 먼저 올리고, 프론트 · 다른 백엔드는 그 계약으로 목(mock)을 써서 먼저 진행한다. 손님 핵심 화면(추천 카드 A5)으로 가는 선행이 길어서(C1 → D1 → D2 → D3 → D11 → E6 → E7), **E7 추천 API 계약도 1단계에 먼저 올린다.** B2(디자인 토큰 · 기본 레이아웃)는 화면 이슈 18개를 막으므로 첫날 끝낼 만큼 작게 잡고, 버튼 · 표 · 시트 같은 공통 컴포넌트는 처음 필요한 화면 이슈에서 B가 더한다.

1단계 다음으로는 D11(방문 처리)이 가장 많은 이슈를 막는다(고객 카드 · 분석 · 추천 실제 기록 · 쿠폰 사용 · 소개 판정 · 가상 데이터). D는 D1 → D2 → D3 → D11 순서로 먼저 끝낸다.

## 같이 쓰는 것 규칙

여러 사람이 같은 파일 · 값을 건드리는 곳이다. 각 1단계 이슈에서 정하고, 그 뒤로는 모두 따른다.

| 대상 | 규칙 | 정하는 이슈 |
| --- | --- | --- |
| API 계약 (`CONTRACTS_API.md`) | 영역별 절(또는 파일)로 나누고 자기 영역만 고친다. 에러 형식 · 인증(세션 쿠키 · CSRF) · 페이지네이션 같은 공통 규칙은 C1이 먼저 정한다 | C1 |
| DB 마이그레이션 | D1 · D19가 06-data의 테이블 · 칸을 처음부터 전부 만든다(D1: 권역 · 가게 · 계정 · 손님 · 방문자, D19: 나머지. 11-24에 C2 · C3 · C4를 먼저 풀려고 나눔). 그 뒤 바꿀 일이 생기면 D에게 요청하고, 다른 사람은 읽기 · 쓰기만 한다. 버전은 타임스탬프로 겹치지 않게 한다 | D1 |
| 상태 · 사유 · 설정값 이름 | 예약 상태, 취소 사유, 쿠폰 상태, 설정값 키는 계약 문서 한 곳에만 정의하고 프론트 · 백엔드가 같은 값을 쓴다 | D1 |
| 방문 처리 뒤 작업 | 방문 처리(D11)는 '방문 처리됨' 이벤트를 내보낸다. 수수료(D15) · 쿠폰 사용 확정(E14) · 소개 판정(E15)은 이벤트를 받아 자기 파일에서 처리하고 D11 코드를 고치지 않는다 | D11 |
| 예약 신청 단계 | 예약 신청(D2)은 처리를 단계(손님 식별 · 공유 동의 · 쿠폰 적용 · 예약금)로 나눈 뼈대를 만든다. C4 · C8 · E13 · D10은 자기 단계만 채운다 | D2 |
| 프론트 라우트 | 라우트는 영역별 파일(손님 · 사장님 · 상인회 · 공용)로 나누고, 화면 이슈는 자기 영역 파일에만 경로를 더한다. 다른 영역 레이아웃에 들어가는 화면(A15 · A21 · A22)은 그 영역 파일에 한 줄만 더한다 | B1 |
| 반응형 | 모바일 우선으로 만들고, 데스크톱 넓은 화면에서도 같은 기능 · 같은 흐름이 되게 한다. 넓은 화면은 모든 역할에 맞추고, 하단 탭을 그대로 쓰며 머리말 · 본문 폭만 넓힌다. 화면 폭 구간(브레이크포인트) · 최대 폭은 B26이 디자인 토큰으로 정하고 화면 이슈는 그것을 따른다(NFR-01, 11-24 (6) · (7)) | B2 · B26 |
| 집계 쿼리 | 상태 변경은 JPA, 집계 · 추천 계산은 네이티브 SQL로 쓴다(ARCHITECTURE 「데이터 접근 · 테스트」). 집계 이슈(C16 ~ C21 · E4 ~ E6 · D16 · D17)가 따른다 | C1 |
| 서버 시각 | 현재 시각은 바꿔 끼울 수 있는 시계로만 읽는다. 스케줄러(D7 · C12 · E14)가 이 규칙을 따른다 | D18 (D1 바로 뒤) |
| 시드 · 시연 데이터 | 가게 시드(E1) · 상인회 계정(C2) · 가상 데이터(E16 · E17)를 한 번에 초기화하고 다시 넣는 순서는 E가 책임진다 | E1 · E17 |

## 이슈 올리는 순서

1. 개발 저장소 Feature 템플릿에 「백로그 ID · 화면 ID」 · 「선행」 · 「목업과 다른 점」 칸을 더한다(11-23 (9)).
2. 라벨 `owner:A` ~ `owner:E`를 만든다. 담당자는 11-24에 라벨대로 Assignee로 지정했다(라벨은 남겨 둔다).
3. 이슈를 모두 만든다. 「선행」은 백로그 ID(예: D2)로 먼저 적는다.
4. 만든 뒤 아래 「번호 대응」 표를 채우고, 「선행」을 실제 이슈 번호(#N)로 바꾼다.
5. 화면 이슈는 만들 때 목업과 대조해 「목업과 다른 점」을 채운다(07-screens 「확정 목업」).

### 번호 대응

2026-11-24에 개발 저장소에 105개(#4 ~ #108), 11-24 (5) 뒤 6개(#113 ~ #118), D1 분리로 D19(#120), 11-24 (7)에 B26(#128), 11-25 (5)로 14개(#159 ~ #172)를 더 올렸다. 백로그 ID → 이슈 번호.

| 담당 | 이슈 |
| --- | --- |
| A | A1 [#4](https://github.com/Leave-421/alley-crm/issues/4) · A2 [#7](https://github.com/Leave-421/alley-crm/issues/7) · A3 [#8](https://github.com/Leave-421/alley-crm/issues/8) · A4 [#11](https://github.com/Leave-421/alley-crm/issues/11) · A5 [#22](https://github.com/Leave-421/alley-crm/issues/22) · A6 [#26](https://github.com/Leave-421/alley-crm/issues/26) · A7 [#27](https://github.com/Leave-421/alley-crm/issues/27) · A8 [#28](https://github.com/Leave-421/alley-crm/issues/28) · A9 [#30](https://github.com/Leave-421/alley-crm/issues/30) · A10 [#32](https://github.com/Leave-421/alley-crm/issues/32) · A11 [#34](https://github.com/Leave-421/alley-crm/issues/34) · A12 [#37](https://github.com/Leave-421/alley-crm/issues/37) · A13 [#40](https://github.com/Leave-421/alley-crm/issues/40) · A14 [#41](https://github.com/Leave-421/alley-crm/issues/41) · A15 [#43](https://github.com/Leave-421/alley-crm/issues/43) · A16 [#44](https://github.com/Leave-421/alley-crm/issues/44) · A17 [#46](https://github.com/Leave-421/alley-crm/issues/46) · A18 [#47](https://github.com/Leave-421/alley-crm/issues/47) · A19 [#50](https://github.com/Leave-421/alley-crm/issues/50) · A20 [#53](https://github.com/Leave-421/alley-crm/issues/53) · A21 [#55](https://github.com/Leave-421/alley-crm/issues/55) · A22 [#57](https://github.com/Leave-421/alley-crm/issues/57) · A23 [#59](https://github.com/Leave-421/alley-crm/issues/59) · A24 [#51](https://github.com/Leave-421/alley-crm/issues/51) · A25 [#60](https://github.com/Leave-421/alley-crm/issues/60) · A26 [#61](https://github.com/Leave-421/alley-crm/issues/61) · A27 [#113](https://github.com/Leave-421/alley-crm/issues/113) · A28 [#114](https://github.com/Leave-421/alley-crm/issues/114) · A29 [#115](https://github.com/Leave-421/alley-crm/issues/115) · A30 [#163](https://github.com/Leave-421/alley-crm/issues/163) · A31 [#166](https://github.com/Leave-421/alley-crm/issues/166) |
| B | B1 [#9](https://github.com/Leave-421/alley-crm/issues/9) · B2 [#10](https://github.com/Leave-421/alley-crm/issues/10) · B3 [#62](https://github.com/Leave-421/alley-crm/issues/62) · B4 [#63](https://github.com/Leave-421/alley-crm/issues/63) · B5 [#65](https://github.com/Leave-421/alley-crm/issues/65) · B6 [#66](https://github.com/Leave-421/alley-crm/issues/66) · B7 [#67](https://github.com/Leave-421/alley-crm/issues/67) · B8 [#68](https://github.com/Leave-421/alley-crm/issues/68) · B9 [#70](https://github.com/Leave-421/alley-crm/issues/70) · B10 [#72](https://github.com/Leave-421/alley-crm/issues/72) · B11 [#75](https://github.com/Leave-421/alley-crm/issues/75) · B12 [#76](https://github.com/Leave-421/alley-crm/issues/76) · B13 [#78](https://github.com/Leave-421/alley-crm/issues/78) · B14 [#83](https://github.com/Leave-421/alley-crm/issues/83) · B15 [#84](https://github.com/Leave-421/alley-crm/issues/84) · B16 [#86](https://github.com/Leave-421/alley-crm/issues/86) · B17 [#88](https://github.com/Leave-421/alley-crm/issues/88) · B18 [#90](https://github.com/Leave-421/alley-crm/issues/90) · B19 [#92](https://github.com/Leave-421/alley-crm/issues/92) · B20 [#94](https://github.com/Leave-421/alley-crm/issues/94) · B21 [#98](https://github.com/Leave-421/alley-crm/issues/98) · B22 [#100](https://github.com/Leave-421/alley-crm/issues/100) · B23 [#101](https://github.com/Leave-421/alley-crm/issues/101) · B24 [#117](https://github.com/Leave-421/alley-crm/issues/117) · B25 [#118](https://github.com/Leave-421/alley-crm/issues/118) · B26 [#128](https://github.com/Leave-421/alley-crm/issues/128) · B27 [#167](https://github.com/Leave-421/alley-crm/issues/167) · B28 [#168](https://github.com/Leave-421/alley-crm/issues/168) · B29 [#171](https://github.com/Leave-421/alley-crm/issues/171) |
| C | C1 [#5](https://github.com/Leave-421/alley-crm/issues/5) · C2 [#24](https://github.com/Leave-421/alley-crm/issues/24) · C3 [#102](https://github.com/Leave-421/alley-crm/issues/102) · C4 [#38](https://github.com/Leave-421/alley-crm/issues/38) · C5 [#64](https://github.com/Leave-421/alley-crm/issues/64) · C6 [#91](https://github.com/Leave-421/alley-crm/issues/91) · C7 [#95](https://github.com/Leave-421/alley-crm/issues/95) · C8 [#96](https://github.com/Leave-421/alley-crm/issues/96) · C9 [#73](https://github.com/Leave-421/alley-crm/issues/73) · C10 [#74](https://github.com/Leave-421/alley-crm/issues/74) · C11 [#97](https://github.com/Leave-421/alley-crm/issues/97) · C12 [#104](https://github.com/Leave-421/alley-crm/issues/104) · C13 [#39](https://github.com/Leave-421/alley-crm/issues/39) · C14 [#42](https://github.com/Leave-421/alley-crm/issues/42) · C15 [#69](https://github.com/Leave-421/alley-crm/issues/69) · C16 [#77](https://github.com/Leave-421/alley-crm/issues/77) · C17 [#56](https://github.com/Leave-421/alley-crm/issues/56) · C18 [#85](https://github.com/Leave-421/alley-crm/issues/85) · C19 [#87](https://github.com/Leave-421/alley-crm/issues/87) · C20 [#54](https://github.com/Leave-421/alley-crm/issues/54) · C21 [#99](https://github.com/Leave-421/alley-crm/issues/99) · C22 [#116](https://github.com/Leave-421/alley-crm/issues/116) · C23 [#165](https://github.com/Leave-421/alley-crm/issues/165) |
| D | D1 [#12](https://github.com/Leave-421/alley-crm/issues/12) · D2 [#13](https://github.com/Leave-421/alley-crm/issues/13) · D3 [#18](https://github.com/Leave-421/alley-crm/issues/18) · D4 [#14](https://github.com/Leave-421/alley-crm/issues/14) · D5 [#71](https://github.com/Leave-421/alley-crm/issues/71) · D6 [#36](https://github.com/Leave-421/alley-crm/issues/36) · D7 [#103](https://github.com/Leave-421/alley-crm/issues/103) · D8 [#105](https://github.com/Leave-421/alley-crm/issues/105) · D9 [#35](https://github.com/Leave-421/alley-crm/issues/35) · D10 [#58](https://github.com/Leave-421/alley-crm/issues/58) · D11 [#19](https://github.com/Leave-421/alley-crm/issues/19) · D12 [#31](https://github.com/Leave-421/alley-crm/issues/31) · D13 [#33](https://github.com/Leave-421/alley-crm/issues/33) · D14 [#48](https://github.com/Leave-421/alley-crm/issues/48) · D15 [#81](https://github.com/Leave-421/alley-crm/issues/81) · D16 [#82](https://github.com/Leave-421/alley-crm/issues/82) · D17 [#89](https://github.com/Leave-421/alley-crm/issues/89) · D18 [#93](https://github.com/Leave-421/alley-crm/issues/93) · D19 [#120](https://github.com/Leave-421/alley-crm/issues/120) · D20 [#160](https://github.com/Leave-421/alley-crm/issues/160) · D21 [#164](https://github.com/Leave-421/alley-crm/issues/164) · D22 [#169](https://github.com/Leave-421/alley-crm/issues/169) · D23 [#170](https://github.com/Leave-421/alley-crm/issues/170) · D24 [#159](https://github.com/Leave-421/alley-crm/issues/159) |
| E | E1 [#6](https://github.com/Leave-421/alley-crm/issues/6) · E2 [#16](https://github.com/Leave-421/alley-crm/issues/16) · E3 [#79](https://github.com/Leave-421/alley-crm/issues/79) · E4 [#15](https://github.com/Leave-421/alley-crm/issues/15) · E5 [#17](https://github.com/Leave-421/alley-crm/issues/17) · E6 [#20](https://github.com/Leave-421/alley-crm/issues/20) · E7 [#21](https://github.com/Leave-421/alley-crm/issues/21) · E8 [#49](https://github.com/Leave-421/alley-crm/issues/49) · E9 [#106](https://github.com/Leave-421/alley-crm/issues/106) · E10 [#52](https://github.com/Leave-421/alley-crm/issues/52) · E11 [#23](https://github.com/Leave-421/alley-crm/issues/23) · E12 [#25](https://github.com/Leave-421/alley-crm/issues/25) · E13 [#29](https://github.com/Leave-421/alley-crm/issues/29) · E14 [#45](https://github.com/Leave-421/alley-crm/issues/45) · E15 [#80](https://github.com/Leave-421/alley-crm/issues/80) · E16 [#107](https://github.com/Leave-421/alley-crm/issues/107) · E17 [#108](https://github.com/Leave-421/alley-crm/issues/108) · E18 [#161](https://github.com/Leave-421/alley-crm/issues/161) · E19 [#162](https://github.com/Leave-421/alley-crm/issues/162) · E20 [#172](https://github.com/Leave-421/alley-crm/issues/172) |

## 이슈 목록

'선행'은 먼저 끝나야 하는 이슈다. '(여유)'는 03-requirements 우선순위(11-23 (9) 확정) 기준이다.

### A · 손님 화면 · 지도 화면 (31)

| ID | 이슈 | 화면 · 요구사항 | 선행 |
| --- | --- | --- | --- |
| A1 | 골목 3D 스크롤: 골목 3개 · 골목마다 가게 5곳 배치 · 스크롤로 골목 안 걷기 (공용 컴포넌트, 데이터 층과 그리는 층 분리 — ARCHITECTURE 「3D 골목 보드」) | G-01, FR-MAP-01 · 02 | — |
| A2 | (여유) 업종 빠른 칩 · 다중 선택 필터 · 업종별 가게 수 | FR-MAP-04 | A1, E1 |
| A3 | (여유) Spotlight Focus (기준 1 + 추천 3 밝게) · 가게 시트 3단 | FR-MAP-05 · 06 | A1 |
| A4 | 가게 확대 · 가게 정보(영업시간 · 휴무일 · 주소) · 추천 3곳 자리 · 예약하기 바 · 시트에서 날짜 · 시간 고르기 | G-01, FR-MAP-01, FR-STO-02 | A1, B2 |
| A5 | 추천 카드 (배지 · 이유 문구) + 추천 API 연결 | G-01, FR-CRS-01 · 05 · 10 | A4, E7 |
| A6 | 추천 카드 쿠폰 배지 · 상세 · 다운로드 (비회원은 로그인 후 복귀) | G-01, FR-CPN-02 · 03 | A5, E12 |
| A7 | '다음 코스로 예약하기' 버튼과 잠김 안내 | G-01, FR-RSV-11 | A5 |
| A8 | 예약하기 입력: 일시 · 인원 · 비회원 정보 · 공유 동의 | G-02, FR-RSV-01, FR-CUS-01 | A4, D2 |
| A9 | 예약하기 마무리: 쿠폰 선택(기본 적용 안 함) · 완료(예약번호) | G-02, FR-CPN-06, FR-AUTH-03 | A8, E13 |
| A10 | 다음 코스 예약 | G-03 | A8, D12 |
| A11 | 내 예약 목록 · 코스 묶음 · 상태 | G-04, FR-RSV-02 · 12 | D4, D13 |
| A12 | 예약 취소(환불 안내) · 예약 변경 | G-04 · 05, FR-RSV-06 · 07 | A11, D6 |
| A13 | 비회원 예약 조회 | G-13 | A11, C13 |
| A14 | 마이: 회원정보 · 가상 잔액 · 충전 · 거래 내역 | G-10 | C2, D9 |
| A15 | 알림함 (손님 · 사장님 공용) | G-11, O-10 | C14 |
| A16 | 정책 · 개인정보 | G-12 | B2 |
| A17 | (여유) 쿠폰함 | G-10, FR-CPN-09 | A14, E14 |
| A18 | (여유) 연결선 · 도보 정보 · 길찾기 | G-01 · 06, FR-MAP-07 ~ 09 | A5 |
| A19 | (여유) 늦을 것 같아요 · 추천 리롤 · 거절 | G-07, FR-RSV-10, FR-CRS-06 | A15, D14, E8 |
| A20 | (여유) 오늘의 코스 | G-14, FR-CRS-11 ~ 13 | A24, E10 |
| A21 | 상인회 방문 흐름 | A-03, FR-ANL-03 | A1, B2, C20 |
| A22 | (여유) 손님 흐름 | O-07, FR-ANL-02 | A1, B2, C17 |
| A23 | (여유) 예약하기 예약금 안내 · 잔액 부족 시 충전 안내 | G-02, FR-RSV-08 | A9, D10 |
| A24 | 홈: 동네 그림 · 골목 진입 · 오늘의 코스 자리 · 바로 가기 | G-14, FR-MAP-01 | A1, B2 |
| A25 | 골목 고르기 | G-15, FR-MAP-01 | A1, B2 |
| A26 | (여유) 활동 기록 | G-16 | A11, A17 |
| A27 | 사장님 예약 상세 (예약번호 · 진행 단계 · 예약금 · 쿠폰 · 취소 · 환불 기준) | O-13, FR-RSV-02 · 04 · 08 · 10 | B6, D4 |
| A28 | 상인회 공동 기금 적립 내역 (월별 · 건별 · 확정 상태) | A-07, FR-STL-05 · 06 | B18, D17 |
| A29 | 사장님 건별 수수료 내역 (방문 금액 · 쿠폰 할인 · 쿠폰 비용 · 수수료, 보낸 가게 숨김) | O-15, FR-STL-03 | B14, D16 |
| A30 | 알림함 상인회 쿠폰 행사 카드 · 선착순 받기 · '마감' 표시, 예약하기 쿠폰 목록에 상인회 쿠폰 (11-25 (5)) | G-11 · 02 · 03, FR-CPN-13 · 14 | A15, A9, E19 |
| A31 | 방문 금액 알림 · 내 예약 금액 표시 · 금액 신고 · 미처리 신고 버튼 (11-25 (5)) | G-11 · 04, FR-STL-07 · 08 | A11, A15, D21, C23 |

### B · 프론트 기반 · 사장님 · 상인회 화면 (29)

| ID | 이슈 | 화면 · 요구사항 | 선행 |
| --- | --- | --- | --- |
| B1 | 프론트 프로젝트 설정(React + JS, TS 전환 대비) · 라우팅(영역별 라우트 파일) · 역할 가드 · Vite 프록시 | FR-AUTH-01, 07-screens 「공통」 | — |
| B2 | 디자인 토큰 · 기본 레이아웃 · 하단 탭 · 시연 데이터 표시 (첫날 크기, 공통 컴포넌트는 화면 이슈에서 더함. 넓은 화면 배치는 B26, 11-24 (7)) | NFR-10 · 11 | B1 |
| B3 | API 클라이언트 · 목 서버 설정 | — | B1 |
| B4 | 로그인 · 회원가입 | G-08 · 09, FR-AUTH-02 · 05 | B2, C2 |
| B5 | 가게 가입 신청 · 승인 대기 | O-11, FR-STO-01, FR-AUTH-04 | B4, C5 |
| B6 | 예약 관리 목록 · 상태 · '추천으로 왔어요' | O-01, FR-RSV-02 · 04 | B2, D4 |
| B7 | 예약 승인 · 거절 · 변경 요청 처리 | O-01 · 02, FR-RSV-03 · 07 | B6, D3 |
| B8 | 방문 처리(방문 금액 입력 → 쿠폰 할인 → 수수료 미리보기) · 쿠폰 사용 확인 | O-01, FR-RSV-09, FR-CPN-08 | B6, D11, E14 |
| B9 | 새 예약 실시간 반영 · 지연 입력 표시 | O-01, FR-NTF-01, FR-RSV-10 | B6, C15 |
| B10 | 예약 운영 설정 (영업 상태 · 예약 받기 · 슬롯 · 동시 예약 · 한 팀 최대 인원 · 예약 가능 기간 · 예약금 · 취소 마감 · 환불 비율) | O-03, FR-RSV-05 · 06 · 08, FR-STO-02 | B2, D5, C22 |
| B11 | 고객 목록 · 등급 필터 | O-04, FR-CUS-04 | B2, C10 |
| B12 | 고객 카드 · 메모 | O-05, FR-CUS-03 | B11, C9 |
| B13 | 세그먼트 분석 | O-06, FR-ANL-01 | B2, C16 |
| B14 | 소개 · 수수료 내역 · 소개 실적 · 가게 잔액 · 가게 충전 버튼 · '충전 필요' 안내 | O-08, FR-STL-03 · 04 · 06 (11-25 (4)) | B2, D16, D9, D10 |
| B15 | 쿠폰 설정 | O-09, FR-CPN-01 · 11 | B2, E11 |
| B16 | 상인회 대시보드 | A-01, FR-ANL-06 | B2, C18 |
| B17 | 상인회 가게 성과 비교 | A-02, FR-ANL-04 · 07 | B2, C19 |
| B18 | 상인회 공동 기금 · 월 정산 | A-04, FR-STL-05 | B2, D17 |
| B19 | 상인회 가게 관리: 가입 승인 · 참여 가게 목록 | A-05, FR-STO-01 · 02 | B2, C5, C6 |
| B20 | 시연 도구: 역할 전환 · 시각 조작 | 07-screens 「화면 한눈에」 | B1, D18 |
| B21 | (여유) 가게 탈퇴 신청 · 상인회 탈퇴 처리 · 정보 공유 설정 | O-16, A-08, A-09, FR-STO-03, FR-CUS-06 | B19, C7, C11 |
| B22 | (여유) 쿠폰 성과 · 추가 지표 | O-06 · 09, A-01, FR-ANL-08 · 09 | B15, C21 |
| B23 | (여유) 상인회 데스크톱 대시보드 (1440px) | A-06 | B16, B17, B18 |
| B24 | 가게 정보 관리 (영업시간 · 휴무일 필수, 소개 · 메뉴 · 편의 · 좌석 · 가격대 · 사진은 여유) | O-12, FR-STO-02 | B2, C22 |
| B25 | (여유) 예약 · 취소 분석 (사유별 취소율 · 60일 재방문율) | O-14, FR-ANL-06 · 07 | B11, C19 |
| B26 | 넓은 화면 기본 배치(반응형): 모든 역할, 하단 탭 유지, 머리말 · 본문 폭만 넓힘, 폭 구간 · 최대 폭 토큰 | NFR-01, 11-24 (7) | B2 |
| B27 | 상인회 쿠폰 관리: 행사 만들기 · 쓸 수 있는 가게 고르기 · 기금 예산 표시 · 중단 (화면 번호 · 배치는 B가 정함, 11-25 (5)) | A-10(임시), FR-CPN-12 | B18, E18, D20 |
| B28 | 상인회 신고 처리: 신고 목록 · 사장님 확인 요청 · 결과 기록 (화면 번호 · 배치는 B가 정함, 11-25 (5)) | A-11(임시), FR-STL-08 | B18, C23 |
| B29 | 사장님 신고 확인 요청 보기 · 금액 정정 · 늦은 방문 처리 (요소 위치는 임시. O-13(A27)에 두면 A27 화면에 붙이기만, 11-25 (5)) | O-10 · 13(임시), FR-STL-09 | B8, D22, D23 |

### C · 백엔드 기반 · 계정 · 가게 · 손님 · 알림 · 분석 (23)

| ID | 이슈 | 요구사항 | 선행 |
| --- | --- | --- | --- |
| C1 | 백엔드 프로젝트 설정 · 공통 응답 · 에러 형식 · CI · Testcontainers 테스트 기반 | NFR-01 | — |
| C2 | 회원가입 · 로그인(세션 쿠키 + CSRF) · 역할, 상인회 계정 초기 데이터 | FR-AUTH-01 · 02 · 05 | C1 |
| C3 | 역할별 열람 범위 서버 가드 | FR-CUS-05, NFR-03 | C2 |
| C4 | 손님 식별 (회원 계정 · 비회원 전화번호) | FR-CUS-02 | C2, D1 |
| C5 | 가게 가입 신청 · 승인 · 거절 · 사장님 계정 | FR-STO-01, FR-AUTH-04 | C2, E1 |
| C6 | 가게 목록 · 영업 상태 · 예약 가능 여부 | FR-STO-02 | C5 |
| C7 | (여유) 가게 탈퇴: 사장님 신청 → 상인회 처리(미정산 확인) | FR-STO-03 | C6, D17 |
| C8 | 공유 동의 기록 | FR-CUS-01 | C4 |
| C9 | 고객 카드 · 메모 | FR-CUS-03 | C4, D11 |
| C10 | 손님 등급 계산 | FR-CUS-04 | C9 |
| C11 | (여유) 공유 정보 정책 (이름 · 연락처 · 방문한 가게 목록은 끌 수 없음) | FR-CUS-06 | C8 |
| C12 | 비회원 파기 스케줄 | FR-CUS-07, NFR-06 | C4, D7 |
| C13 | 비회원 예약 조회 (예약번호 + 전화번호, 제한 세션) | FR-AUTH-03 | C4, D2 |
| C14 | 알림 저장 · 조회 · 손님 알림 종류 | FR-NTF-02 · 03 | C2 |
| C15 | 사장님 실시간 알림 (SSE) | FR-NTF-01, NFR-05 | C14 |
| C16 | 세그먼트 분석 API | FR-ANL-01 | C4, D11 |
| C17 | (여유) 사장님 손님 흐름 API | FR-ANL-02 | C20 |
| C18 | 성공 지표: 수락률 · 재방문율 · 수수료 총액 | FR-ANL-06 | D11, E15 |
| C19 | 가게 성과 비교 · 취소율 | FR-ANL-04 · 07 | C18 |
| C20 | 방문 동선 집계 · 5명 미만 숨김 공통 | FR-ANL-03 · 05 | D11 |
| C21 | (여유) 추가 지표 · 쿠폰 지표 | FR-ANL-08 · 09 | C19, E14 |
| C22 | 사장님 가게 정보 · 영업 상태 · 예약 받기 변경 API (주소 · 위치는 상인회만) | FR-STO-02 | C6 |
| C23 | 금액 · 미처리 신고 접수(정산 확정 전까지) · 상인회 확인 요청 · 결과 기록 API, 사장님 확인 요청 알림 (11-25 (5)) | FR-STL-08 | C14, D17, D24 |


### D · DB 기반 · 예약 · 돈 (24)

| ID | 이슈 | 요구사항 | 선행 |
| --- | --- | --- | --- |
| D1 | DB 기반 1: 권역 · 가게 · 계정 · 손님 · 방문자 테이블, enum 값 계약 전체, 설정값 관리 | NFR-04, 06-data | C1 |
| D2 | 예약 신청 (단계별 뼈대 — 「같이 쓰는 것 규칙」) | FR-RSV-01 | D19 |
| D3 | 예약 승인 · 거절 | FR-RSV-03 | D2 |
| D4 | 예약 상태 · 취소 사유 · 날짜별 목록 (보낸 가게 숨김) | FR-RSV-02 · 04 | D2 |
| D5 | 가게 예약 설정 · 슬롯 계산 (영업시간 · 휴무일 · 한 팀 최대 인원 · 가게별 환불 비율) | FR-RSV-05 | D2 |
| D6 | 손님 취소 · 환불 규칙 (가게별 환불 비율, 기본값은 권역 설정값) | FR-RSV-06 | D4, D9 |
| D7 | 자동 거절 · 자동 취소 스케줄 | NFR-06 | D3, D6 |
| D8 | (여유) 예약 변경 · 재승인 · 변경 자동 거절 | FR-RSV-07 | D3 |
| D9 | 가상 잔액 · 거래 내역 | FR-STL-06, NFR-02 | D19 |
| D10 | (여유) 예약금 받기 · 가상 충전(회원 · 가게) · 잔액 부족 거절 | FR-RSV-08, FR-STL-06 (가게 충전, 11-25 (4)) | D2, D9 |
| D11 | 방문 처리 · 방문 금액 · '방문 처리됨' 이벤트 | FR-RSV-09 | D3 |
| D12 | 다음 코스 예약 · 제안 ID · 기준 예약 연결 · 같은 날은 기준 예약보다 늦은 시각만 · 취소 · 거절된 기준 예약은 거절 | FR-RSV-11 | D2 |
| D13 | 코스 묶음 조회 · 기준 가게 취소 · 거절 표시 | FR-RSV-12 | D12 |
| D14 | (여유) 지연 입력 | FR-RSV-10 | D4, C14 |
| D15 | 소개 수수료 계산 · 잔액 차감 · 기금 입금 | FR-STL-02 | D9, D11, E15 |
| D16 | 수수료 내역 · 소개 실적 | FR-STL-03 · 04 | D15 |
| D17 | 월 정산 · 확정 · 공동 기금 | FR-STL-05 | D15 |
| D18 | 서버 시계 바꿔 끼우기 · 시연용 시각 조작 API | NFR-06, ARCHITECTURE 「서버 시각」 | D1 |
| D19 | DB 기반 2: 고객 카드 · 공유 동의 · 예약 · 추천 기록 · 쿠폰 · 잔액 · 수수료 · 정산 · 알림 · 공공데이터 테이블 (06-data 나머지 전부) | 06-data | D1 |
| D20 | 공동 기금 예산 잡기 · 해제 (기금 마이너스 불가, 잔액 부족 시 행사 생성 거절) (11-25 (5)) | FR-CPN-12, FR-STL-06 | D9, D24 |
| D21 | 방문 금액 알림 보내기 (방문 처리됨 이벤트 → 회원 알림) (11-25 (5)) | FR-STL-07, FR-NTF-03 | D11, C14 |
| D22 | 금액 정정 · 수수료 차액 추가 거래 (원래 기록 유지, 원래 달 정산) (11-25 (5)) | FR-STL-09, FR-STL-02 | D15, C23 |
| D23 | 늦은 방문 처리 (자동 취소 → 방문, 미처리 신고 '맞음'일 때만) (11-25 (5)) | FR-STL-09, FR-RSV-02 | D11, C23 |
| D24 | DB: 상인회 쿠폰 행사 · 쿠폰 발급 주체 · 신고 · 방문 금액 정정 테이블과 거래 종류 enum 추가 (11-25 (5)) | 06-data | D19 |

### E · 공공데이터 · 추천 · 쿠폰 · 가상 데이터 (20)

| ID | 이슈 | 요구사항 | 선행 |
| --- | --- | --- | --- |
| E1 | 권역 · 가게 15곳 시드 (영업시간 · 휴무일 · 주소 포함) | NFR-07 | D1 |
| E2 | 공공데이터 적재 · 데이터 출처 구분 | NFR-10, 06-data 「공공데이터」 | E1 |
| E3 | 가게 클릭 · 추천 노출(탐색 기록) · 정식 코스 제안 기록 · 익명 방문자 ID 연결 | FR-CRS-07 | E1, C4, D19 |
| E4 | 추천 후보 걸러내기 | FR-CRS-01 | E1, D4 |
| E5 | 공공데이터 기본값 점수 | FR-CRS-04 | E2 |
| E6 | 실제 기록 점수 · 섞기 · 성별 · 연령대 집단 | FR-CRS-03 · 04 | E5, D11 |
| E7 | 순위 · 배지 · 이유 문구 · 추천 API | FR-CRS-05 · 10 | E4, E6 |
| E8 | (여유) 리롤 · 거절 · 추천 알림 | FR-CRS-02 · 06 | E7, C14 |
| E9 | 쿠폰 다운로드 동시성 · 총수량 원자성(조건부 UPDATE) | NFR-09 | E12 |
| E10 | (여유) 오늘의 코스 | FR-CRS-11 ~ 13 | E7 |
| E11 | 쿠폰 행사 설정 | FR-CPN-01 · 11 | E1, D19 |
| E12 | 쿠폰 발급 · 30일 제한 · 출처 기록 | FR-CPN-03 · 04 · 10 | E11, C2 |
| E13 | 쿠폰 적용 · 해제 | FR-CPN-05 · 06 | E12, D2 |
| E14 | 쿠폰 상태 · 만료 · 사용 확인 | FR-CPN-07 · 08 | E13, D11 |
| E15 | 소개 판정(제안 ID · 기준 예약 · 당일 마감) · 보낸 가게 | FR-STL-01 | E3, D12, D11 |
| E16 | 가상 데이터 1: 손님 · 예약 · 취소 · 방문 | NFR-08 | D11 |
| E17 | 가상 데이터 2: 이동 · 탐색 기록 · 코스 제안 · 소개 · 패턴 3개 확인 | NFR-08 | E16, E7, E15 |
| E18 | 상인회 쿠폰 행사 만들기 · 중단 (정률은 최대 할인액 필수, 쓸 수 있는 가게, 기간) (11-25 (5)) | FR-CPN-12 | E11, D20, D24 |
| E19 | 상인회 쿠폰 선착순 발급 · 한 사람당 1장 · 수량 원자성 · 행사 알림 · '마감' (11-25 (5)) | FR-CPN-13 | E18, E9, C14 |
| E20 | 상인회 쿠폰 적용(쓸 수 있는 가게 · 한 장만) · 기금 부담 비용 기록 · 행사 끝 예산 반환 요청 (11-25 (5)) | FR-CPN-14 | E19, E13, E14, D20 |


## 아직 정하지 않은 것

- 크기 추정(스토리 포인트를 쓸지)
- 프론트 TypeScript 전환(정해지면 B1에서 반영), 배포 구성, 3D 보드 그리는 방식(화면 구조는 11-24 (4)에 정함) (ARCHITECTURE 「미결」)
- 미결 값이 걸린 이슈는 설정값의 임시 기본값으로 진행하고, 정해지면 값만 바꾼다: E5 거리 지수 β, E16 가상 손님 수
