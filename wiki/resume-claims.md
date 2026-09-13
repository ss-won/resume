# Resume Claims — Evidence Map

현재 공개 이력서의 주요 주장과 증거 레벨 매핑.

Evidence levels: **Public** · **Redacted-internal** · **Self-attested** · **Derived**

---

## 프로필

| 주장 | 레벨 | 비고 |
|---|---|---|
| React·TypeScript 기반 프론트엔드 개발 | Public | 경력·기술 스택으로 확인 |
| WebView 제품, BFF, 성능 최적화, 사내 개발 도구 개발 | Redacted-internal | 관련 저장소와 PR 근거 |
| 화면 구현 전 데이터 흐름과 책임 범위를 먼저 정리 | Self-attested | 본인 업무 방식 |
| 성능 문제를 실제 측정 결과로 개선 | Redacted-internal | Explorer Lighthouse 측정 결과 |
| NestJS·FastAPI 등 프론트엔드 밖의 영역도 담당 | Public + Redacted-internal | 공개 이력과 관련 저장소 근거 |

## 파이랩테크놀로지

### 블록 스캐너(Explorer) 성능 최적화

| 주장 | 레벨 | 비고 |
|---|---|---|
| 주요 목록 화면 LCP 평균 45%, TBT 평균 74% 단축 | Derived | 3개 route 로컬 Lighthouse 측정값 평균 |
| /blocks LCP 3.7s→1.9s, TBT 1,010ms→270ms | Redacted-internal | 로컬 Lighthouse 측정, 프로덕션 RUM 아님 |
| /txs LCP 3.7s→2.2s, TBT 1,330ms→200ms | Redacted-internal | 로컬 Lighthouse 측정 |
| /tokens LCP 3.3s→1.8s, TBT 510ms→190ms | Redacted-internal | 로컬 Lighthouse 측정 |
| 최대 75개 row 테이블의 가상화를 롤백하고 단계적 렌더링으로 전환 | Redacted-internal | explorer-front PR 근거 |
| 실시간 행 추가량 제한 및 신규·대기 거래 알림 배치 | Redacted-internal | explorer-front #133: 블록 자동 추가 상한 25행, 배치 간격 600ms. 기존 30초 표기는 오류로 정정. LCP·TBT는 렌더링 변경 전체의 전후 결과이며 배치 단독 기여도는 측정하지 않음 |
| 무거운 행이 계속 추가되며 테이블 재렌더링 부담이 발생 | Self-attested | 2026-09-14 본인 설명. 실시간 처리 개선의 동기이며 개별 효과 수치로 환산하지 않음 |

### DApp 데이터 조회 구조

| 주장 | 레벨 | 비고 |
|---|---|---|
| Gas Top-up의 최초 biholder 호출 25~46회→17회, interval 분당 25회→1~19회 축소 | Redacted-internal | app-pockie-front PR #51 측정 결과 |
| SDK AssetInfoMapProvider가 환율 계산을 위해 발생시키던 asset 조회 의존을 분리하고 GTU API가 이미 제공하는 vault·network asset 중복 조회 제거 | Redacted-internal | app-pockie-front PR #51·BAM-240; PR 본문과 commit 7676c6e 코드 대조 |
| BiFi bridge pair 1회+pair별 N회 조회를 outbound·inbound 각 1회와 React Query 캐시로 재구성 | Redacted-internal | pockie-ui commit c6ad5e1; 변경 전 Promise.allSettled pair별 조회, 변경 후 query 2개·staleTime Infinity |
| BiFi balance 조회 개선 (CV 대표 성과에서는 제외) | Redacted-internal | pockie-ui #171: 토큰별 refreshSingleBalance → 다중 토큰 잔액 API 1회. #200: 성공 후 refetch 호출 추가. 최신 잔액 즉시 반영을 보장한다는 뜻은 아님 |

### WebView와 BFF

| 주장 | 레벨 | 비고 |
|---|---|---|
| Pockie miniDApp의 BiFi·Swap·BTCFi 화면 개발 및 postMessage 지갑 기능 연동 | Redacted-internal | pockie-ui 제품/기여 기록. 공통 아키텍처 전체를 신규·단독 설계했다고 주장하지 않음 |
| Pockie BFF config v2에서 플랫폼·앱 버전별 feature flag로 기능 노출을 제어 | Redacted-internal | pockie-api-v2 PR 근거 |
| BTCFi Partners의 파트너별 거래 흐름 분리, UI·데이터 계층 공유 및 의존 경계 CI 테스트 | Redacted-internal | btcfi-partners-front #132 원본 PR 본문 확인. 파트너별 flows 물리 분리이며 모든 상품 흐름 공통화가 아님 |
| 웹앱 외에 파트너 지갑 WebView용 widget 화면 제공 | Self-attested | 2026-09-14 본인 추가 확인. 특정 파트너 요청에 맞춘 제공 방식이며 모든 파트너·플랫폼 지원으로 확대하지 않음 |
| NestJS Swap BFF 개발·견적/거래 데이터/상태 API 연동 | Redacted-internal | pockie-api-v2 #12·#16~19. 프론트에서 BFF로 이전했다는 전후 관계나 모든 엔드포인트 신규 작성은 주장하지 않음 |
| 플랫폼·버전별 feature flag를 BFF config v2에 구현 | Redacted-internal | pockie-api-v2 PR 근거 |

### AI Agent 런타임

| 주장 | 레벨 | 비고 |
|---|---|---|
| MCP 서버 전체 실행을 필요한 서버의 호출 시 실행으로 변경 | Redacted-internal | Donald #36 원본 PR: MCP lazy proxy. 런타임 전환과 별개 변경이며 복합 응답시간 수치를 단독 효과로 쓰지 않음 |
| 별도 confidence 검증과 CI 상태 확인으로 자동 리뷰 제출 조건 관리 | Redacted-internal | Donald repo PR 근거 |
| 최종 머지는 사람이 확인하는 운영 원칙 유지 | Self-attested | 운영 정책 |
| Claude SDK 실행 경로를 Codex App Server 세션·worker로 전환 | Redacted-internal | Donald #48 원본 PR·worker/queue 파일 목록 및 synthesis 확인. 기존 기반 위 런타임 전환이며 전체 에이전트 신규 개발 아님 |
| 요청 단위 read/write 분류를 도구별 영향·가역성에 따른 실행 정책으로 재설계 | Redacted-internal | Donald #50·#52 원본 PR 확인. 승인/차단 조건이 있으며 보안 완전 보장으로 표현하지 않음 |
| 자동 리뷰에 저장소별 규칙·confidence·CI 검증 적용 | Redacted-internal | Donald #19·#46·#47·#52·#58. #52에 최종 merge 별도 사람 확인 명시 |

### 성능 개선 외 추가 선정 근거

| 주장 | 레벨 | 비고 |
|---|---|---|
| Explorer 마이그레이션 (CV 대표 성과에서 제외) | Redacted-internal + Self-attested | explorer-front #121. 팀 next-boilerplate 공용 버전 및 Node 22 기준 정리가 목적이었다는 본인 설명에 따라 대표 bullet 제외 |

### 의사결정 배경 (2026-09-14 본인 확인)

- BTCFi Partners: 파트너별 상품 조건·지갑 연동 방식이 달라 공유 모듈 변경이 다른 화면에 영향을 줌. 파트너 수와 확장 불확실성, 단일 웹 root 요구, 빠른 배포를 고려해 모노레포 대신 기존 저장소 내 경계와 CI 검사 선택. 영향 완전 제거나 배포 시간 개선 수치는 주장하지 않음.
- AI: Claude 종량제 요금 변동에 대응하려는 전환. 오픈소스 upstream 업데이트 추적 부담도 고려해 Codex App Server 선택. 실제 비용 절감·안정화 성과는 측정하지 않음.
- BiFi: bridge pair 목록이 자주 바뀌지 않아 반복 조회를 줄임. 코드로 확인한 API 요청 수는 1+N → 2회이며 N² 복잡도 주장은 사용하지 않음.
| Jest → Vitest, Playwright 렌더링·레이아웃·WebSocket 회귀 테스트 | Redacted-internal | explorer-front #140 본인 PR 본문에 테스트 파일과 검증 명시 |

## 스마트마인드

| 주장 | 레벨 | 비고 |
|---|---|---|
| Workspace First Load 최대 40% 단축 | Public | 공개 이력서·기술 글, 당시 측정 기준 |
| pnpm·Turborepo 전환과 빌드 캐시로 앱별 빌드 7분→1분 단축 | Public | 공개 이력서·기술 글, 당시 측정 기준 |
| AI 팀이 정의한 ANTLR 문법을 Monaco Editor에 연결해 구문 강조·오류 진단·키워드 자동완성 구현 | Public | 공개 이력서·기술 글; ANTLR grammar 저작으로 표현하지 않음 |
| iframe+postMessage와 module federation 기반 Microfrontend 설계 | Public | 공개 이력서·기술 글 |
| Query Viewer에 서버 페이지네이션·가상 스크롤·미디어 lazy loading 적용 | Public | 공개 이력서·기술 글 |
| 단기 과제·PoC에서 FastAPI·Docker Compose 기반 모델 서빙과 데이터 파이프라인 개발 | Public + Self-attested | 공개 이력서 및 2026-09-14 본인 확인. 상용 서비스 구축·장기 운영 경험으로 확대하지 않음 |
| 2023년부터 본인 포함 2~3명 파트의 스크럼 운영·업무 배분·우선순위 결정 담당 | Self-attested | 본인 확인 |

## 주의 사항

| 주장 | 주의 이유 |
|---|---|
| Explorer 성능 수치 | 로컬 Lighthouse 측정으로 프로덕션 실사용자 측정(RUM)과 구분 필요 |
| 빌드 시간 7분→1분 | 당시 프로젝트와 CI 환경의 측정 기준임을 면접에서 명시 |
| 2024.09–현재 2년 | 2026년 9월 기준 표기이며 지원 시점에 따라 갱신 필요 |
