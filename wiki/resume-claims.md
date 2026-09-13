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
| WebSocket 업데이트를 30초 단위로 배치 | Redacted-internal | explorer-front PR 근거 |

### DApp 데이터 조회 구조

| 주장 | 레벨 | 비고 |
|---|---|---|
| Gas Top-up의 최초 biholder 호출 25~46회→17회, interval 분당 25회→1~19회 축소 | Redacted-internal | app-pockie-front PR #51 측정 결과 |
| SDK AssetInfoMapProvider가 환율 계산을 위해 발생시키던 asset 조회 의존을 분리하고 GTU API가 이미 제공하는 vault·network asset 중복 조회 제거 | Redacted-internal | app-pockie-front PR #51·BAM-240; PR 본문과 commit 7676c6e 코드 대조 |
| BiFi bridge pair 1회+pair별 N회 조회를 outbound·inbound 각 1회와 React Query 캐시로 재구성 | Redacted-internal | pockie-ui commit c6ad5e1; 변경 전 Promise.allSettled pair별 조회, 변경 후 query 2개·staleTime Infinity |
| BiFi balance 조회를 background dispatcher 경유에서 client 단일 호출로 변경하고 거래 성공 직후 갱신 | Redacted-internal | pockie-ui PR #171·#200 근거 |

### WebView와 BFF

| 주장 | 레벨 | 비고 |
|---|---|---|
| Pockie miniDApp의 BiFi·Swap·BTCFi 거래 화면을 Mobile App·Chrome Extension에서 공통 WebView로 재사용 | Redacted-internal | pockie-ui PR 근거 |
| Pockie 거래 화면은 BFF 계약을 소비하고 지갑 서명·전송은 각 호스트에 위임 | Redacted-internal | pockie-ui PR 근거 |
| Pockie BFF config v2에서 플랫폼·앱 버전별 feature flag로 기능 노출을 제어 | Redacted-internal | pockie-api-v2 PR 근거 |
| BTCFi Partners를 파트너사 모바일 지갑의 iOS·Android WebView에 연동 | Redacted-internal | btcfi-partners-front PR 근거 |
| BTCFi Partners의 postMessage 이벤트와 widget route를 설계해 일반 웹과 WebView에서 상품 로직 재사용 | Redacted-internal | btcfi-partners-front PR 근거 |
| Swap 견적·거래 데이터 생성·상태 조회를 NestJS BFF로 분리하고 외부 SDK 오류 처리 정리 | Redacted-internal | pockie-api-v2 Swap BFF 엔드포인트·에러 정규화 근거 |
| 플랫폼·버전별 feature flag를 BFF config v2에 구현 | Redacted-internal | pockie-api-v2 PR 근거 |

### AI Agent 런타임

| 주장 | 레벨 | 비고 |
|---|---|---|
| stdio 기반 요청별 프로세스 실행을 필요한 도구만 실행하는 구조로 개선 | Redacted-internal | Donald repo PR 근거 |
| 별도 confidence 검증과 CI 상태 확인으로 자동 리뷰 제출 조건 관리 | Redacted-internal | Donald repo PR 근거 |
| 최종 머지는 사람이 확인하는 운영 원칙 유지 | Self-attested | 운영 정책 |
| Codex App Server 기반 세션 구조로 전환 | Redacted-internal | Donald repo PR 근거 |
| 도구 실행 전 보안 검증과 MCP·권한 선택 허용 구조 설계 | Redacted-internal | Donald repo PR 근거 |

## 스마트마인드

| 주장 | 레벨 | 비고 |
|---|---|---|
| Workspace First Load 최대 40% 단축 | Public | 공개 이력서·기술 글, 당시 측정 기준 |
| pnpm·Turborepo 전환과 빌드 캐시로 앱별 빌드 7분→1분 단축 | Public | 공개 이력서·기술 글, 당시 측정 기준 |
| AI 팀이 정의한 ANTLR 문법을 Monaco Editor에 연결해 구문 강조·오류 진단·키워드 자동완성 구현 | Public | 공개 이력서·기술 글; ANTLR grammar 저작으로 표현하지 않음 |
| iframe+postMessage와 module federation 기반 Microfrontend 설계 | Public | 공개 이력서·기술 글 |
| Query Viewer에 서버 페이지네이션·가상 스크롤·미디어 lazy loading 적용 | Public | 공개 이력서·기술 글 |
| FastAPI·Docker Compose 기반 모델 서빙과 데이터 파이프라인 개발 | Public | 공개 이력서 |
| 2023년부터 본인 포함 2~3명 파트의 스크럼 운영·업무 배분·우선순위 결정 담당 | Self-attested | 본인 확인 |

## 주의 사항

| 주장 | 주의 이유 |
|---|---|
| Explorer 성능 수치 | 로컬 Lighthouse 측정으로 프로덕션 실사용자 측정(RUM)과 구분 필요 |
| 빌드 시간 7분→1분 | 당시 프로젝트와 CI 환경의 측정 기준임을 면접에서 명시 |
| 2024.09–현재 2년 | 2026년 9월 기준 표기이며 지원 시점에 따라 갱신 필요 |
