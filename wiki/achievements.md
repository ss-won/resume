# Key Achievements — 정소원 (Sowon Jung)

Evidence levels: **Public** = verifiable from public sources · **Redacted-internal** = private GitHub evidence, no links · **Self-attested** = engineer-provided business context · **Derived** = calculated from verified data

---

## A. Bifrost Explorer — 대규모 프론트엔드 현대화

**Evidence:** Redacted-internal (67 PRs, all merged) + Public (velog.io/@ss-won)

### 기술 현대화
983개 파일 규모의 마이그레이션으로 Next.js 13 Pages Router → Next.js 15 App Router 전환, React 19 · Chakra UI v3 · Wagmi/Viem v2 · ESLint 9 도입, Ethers.js · 레거시 라우터 제거, 서버/클라이언트 경계·메타데이터·SSR hydration 문제를 함께 정리했다.

### 성능 개선
blocks/transactions/tokens 주요 화면에 점진 렌더링과 무거운 UI 지연 로딩을 적용. 로컬 Lighthouse 측정 기준:

| Route | LCP | TBT | Speed Index |
|---|---|---|---|
| /blocks | ↓49% (3.7s→1.9s) | ↓73% (1,010ms→270ms) | ↓63% |
| /txs | ↓41% (3.7s→2.2s) | ↓85% (1,330ms→200ms) | ↓55% |
| /tokens | ↓45% (3.3s→1.8s) | ↓63% (510ms→190ms) | ↓55% |

CLS를 0~0.003 수준으로 유지. 가상화는 최대 75행 조건에서 mount/unmount 비용이 더 커 제거하고, 초기 렌더링 범위 제한·단계적 렌더링·WebSocket 30초 배치 처리로 대체.

### 테스트 인프라
Jest → Vitest 전환. Playwright 기반 스모크, 필터/정렬, 레이아웃 시프트, 점진 렌더링, WebSocket 갱신 E2E 테스트 도입.

---

## B. 모바일 WebView 거래 제품 구현

**Evidence:** Redacted-internal (pockie-ui, pockie-wallet-extension, pockie-api-v2 합계 164+ PRs) + Self-attested (business outcome)

### WebView 거래 화면 구현
Mobile App과 Chrome Extension에서 동일한 BTCFi·Swap·BiFi WebView 거래 화면을 재사용할 수 있도록 공통 UI 번들, postMessage 연동, Pockie BFF API 기반 거래 상태 조회 구조를 구현. 파트너사와 postMessage 이벤트를 협의·설계해 widget route로 WebView/일반 웹 접근을 분리했다.

BiFi 예치·출금·대출·상환 4개 화면, Swap 견적 조회·승인·거래 데이터 생성·상태 조회를 BFF API와 연결.

### 거래 책임 경계 설계
거래 화면은 BFF 계약을 소비하고, 지갑 서명·전송은 Mobile App 또는 Chrome Extension의 호스트 지갑에 위임하는 구조로 정리. 같은 WebView 거래 화면을 여러 호스트에서 재사용 가능.

### 플랫폼·버전별 기능 출시 제어
iOS·Android·Extension 및 앱 버전별 feature flag와 하위 호환 fallback을 BFF config v2에 구현. 클라이언트 배포 없이 기능 노출을 서버에서 제어.

### 거래 실패 복구
Native BTC 입금 실패 시 WebView storage 복구, 오류 화면 전환, Sentry 사용자 진단, API 재조회 로직으로 사용자가 거래 단계에 고립되는 edge case를 개선.

### 61파일 규모 WebView E2E 기반
page object 모델·네트워크 mocking 포함 Playwright WebView E2E 테스트 기반 구축.

**Outcome (self-attested):** BTCFi Partners · Hashport Wallet WebView — 출시 3개월간 일본 액티브 유저 750명대, 실제 입금 1억 엔대 운영.

---

## C. BTCFi 멀티 파트너 아키텍처

**Evidence:** Redacted-internal (90 PRs btcfi-partners-front + 44 PRs btcfi-boost-front)

257개 파일 규모로 비동기 입금·복구, epoch 출금, 진행 대시보드·CSV export, 상품 config·BFF 재시도/fallback을 포함한 파트너 플로우를 구현. 파트너별 거래 수명주기·정책·locale/catalog를 분리해 공통 제품 코어에서 수명주기와 정책이 다른 상품을 운영할 수 있는 구조를 구축했다.

---

## D. 사내 AI Agent 런타임 개선

**Evidence:** Redacted-internal (21 PRs Donald repo)

### 컨텍스트 주입 구조
core memory와 MCP on-demand search로 분리, 요청별 변동 정보를 프롬프트 tail로 이동해 정적 prefix 안정화. 메모리 주입 예산·우선순위 절단·관측 로그 추가.

### 자동 리뷰 workflow와 품질 게이트
Slack 기반 코드 리뷰 흐름에 리뷰 근거·confidence verifier를 추가, commit/PR에 Jira 티켓 형식이 있을 경우 실제 이슈 정보 검증. CI·테스트·타입 오류·high severity 없는 경우에만 자동 승인 후보로 분류, 최종 결과물은 사람이 확인하는 원칙 유지.

### MCP 도구 실행 구조
Claude Agent SDK의 stdio 기반 MCP 중복 실행 구조를 dynamic tools 구조로 전환. 병렬 호출 시 MCP 서버 중복 실행 부담 감소.

### Codex app server 전환
Claude Agent SDK 기반 런타임을 Codex app server로 전환하면서 read/write tool 권한을 별도 mode로 나누던 구조를 통합. write tool 사용 시 보안 effective gate와 감사 로그를 거치도록 재설계.

### 보안 gate·감사 로그
prompt injection·Slack 계정 탈취로 민감 도구가 악용될 수 있는 경로를 줄이기 위해 보안 gate 강화. 조직 repo 외부 코드 clone·실행 제한, 전역 npm 업데이트 같은 환경 오염 작업은 workspace sandbox 격리. 차단 사유와 도구 호출 맥락은 감사 채널과 tool call journal에 기록.

---

## E. ui-kit-front — 공유 UI Kit · 디자인 시스템

**Evidence:** Redacted-internal (1 PR merged to main/develop; additional branch-only commits per engineer-provided data)
**Note:** 아래 Figma Code Connect / 아이콘 시스템 작업은 브랜치에만 존재하며 main에 병합되지 않았음.

### main/develop에 병합된 작업 (v0.1.8)
330개 파일 규모로 컴포넌트·아이콘·에셋을 동기화하고 v0.1.8 릴리즈를 작성·머지했다. Snyk의 tailwind-merge 3.3.1→3.4.0 보안 업그레이드 커밋을 처리했다.

### 브랜치 전용 작업 (unmerged · 참고 기록)
- **Figma Code Connect 통합 (FT-112):** 컴포넌트별 Code Connect 연결, Input·Toggle 등 Storybook 설정 개선, Figma Template V2 API 기반 템플릿 파일 추가, Figma 플러그인 아키텍처 모듈화
- **아이콘 시스템 설계:** size prop 정규화·토큰 처리, width/height props 및 tight icon 스마트 기본값, filled/colored icon variant 추가
- **컴포넌트 개선:** Toggle 접근성 및 line toggle 구현, Button ghost variant padding, Slider 수직 존·hover 동기화, Tabbar 컴포넌트·지갑 아이콘 추가

### 파이프라인 구현
합성 컴포넌트(Tabs·Toast 등)는 정적 `figma.connect()` 매핑으로 동적 children 수·내용을 표현할 수 없어 Template V2 API를 도입. `findLayers()`·`findText()`로 런타임 인스턴스 순회, `findConnectedInstances()` + `executeTemplate()`로 자식 컴포넌트 템플릿을 재귀 실행해 실제 Figma 구성 기반 코드를 생성. `figma.template.config.json` + 커스텀 `parser.js`로 Code Connect CLI와 연동. 20개 컴포넌트 중 14개에 동적 API 적용 (정적 getEnum 전용 6개 제외).

### 활용 지침
디자인 시스템·컴포넌트 라이브러리·FDE 포지션에서 "합성 컴포넌트 Code Connect 한계 → Template V2로 해결" 스토리로 활용. 일반 프론트엔드 지원에서는 메인 업적으로 사용하지 않음.

---

## F. ThanoSQL — AI 데이터 분석 플랫폼 (스마트마인드)

**Evidence:** Public (velog.io/@ss-won) + Redacted-internal

### Monaco Editor + ANTLR SQL Editor
AI 팀이 정의한 ANTLR 문법을 Monaco Editor에 연결해 ThanoSQL SQL 구문 강조, 문법 오류 진단, 키워드 자동완성을 제공하는 재사용 편집기 컴포넌트 개발.

### JupyterLab Workspace 통합
개발 도구가 초기화된 JupyterLab Workspace와 ThanoSQL 테이블 생성·조회용 SQL Editor를 개발하고, postMessage를 통해 제품 로그인만으로 JupyterLab 세션에 접근하도록 인증을 위임.

### Query Viewer 성능
비정형 데이터(이미지·오디오·비디오) Query Viewer에 서버 페이지네이션, 가상화, 미디어 lazy loading을 적용해 대용량 조회 화면 렌더링 부담 감소.

### Turborepo 모노레포
앱 단위 라우트로 분산된 개발 구조를 pnpm·Turborepo 기반 모노레포와 공용 UI·유틸 패키지 구조로 정리. 패키지 빌드 분리·빌드 캐시 활용·pnpm 전환으로 평균 빌드 시간 7분 → 1분으로 단축 (당시 측정 기준).

### FastAPI 모델 서빙
에너지 예측 정부과제(P2P-DC)에서 AI 팀이 파인튜닝한 PyTorch `.pt` 모델을 서빙하는 FastAPI 구현, Docker Compose 배포 환경 구성.

### Frontend Part Leader
프론트엔드 파트 리더로서 일정·업무 분배, 팀원 온보딩, 코드 리뷰 담당.
