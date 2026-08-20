# Resume Claims — Evidence Map

공개 이력서의 각 주요 주장과 그 증거 레벨 매핑.

Evidence levels: **Public** · **Redacted-internal** · **Self-attested** · **Derived**

---

## 파이랩테크놀로지 경력

### 프로필 요약

| 주장 | 레벨 | 비고 |
|---|---|---|
| React·TypeScript 기반 5년차 프론트엔드 개발자 | Public | 이력서 기재 재직 기간 계산 |
| 크립토 자산 지갑(Pockie), DeFi DApp(BiFi·BTCFi), 블록 탐색기, AI 데이터 분석 플랫폼 담당 | Redacted-internal | PR 저장소 분포로 확인 |
| 병목을 찾아 개선하는 과정을 좋아함 | Self-attested | 본인 기술 |

### WebView 거래 제품

| 주장 | 레벨 | 비고 |
|---|---|---|
| Mobile App과 Chrome Extension에서 동일한 BTCFi·Swap WebView 거래 화면 재사용 구조 구현 | Redacted-internal | pockie-ui PR 근거 |
| postMessage 연동, Pockie BFF API 기반 거래 상태 조회 구조 구현 | Redacted-internal | pockie-ui PR 근거 |
| BiFi 예치·출금·대출·상환 4개 화면 구현 | Redacted-internal | pockie-ui #158 근거 |
| Swap 견적 조회·승인·거래 데이터 생성·상태 조회 연결 | Redacted-internal | pockie-ui PR 근거 |
| widget route로 WebView/일반 웹 접근 분리 | Redacted-internal | pockie-ui PR 근거 |
| iOS·Android·Extension 버전별 feature flag + BFF config v2 | Redacted-internal | pockie-api-v2 #42 근거 |
| BTCFi Partners · Hashport Wallet WebView — 출시 3개월간 일본 액티브 유저 750명대 | Self-attested | 외부 검증 불가 |
| 실제 입금 1억 엔대 운영 | Self-attested | 외부 검증 불가 |

### DApp BFF 통합

| 주장 | 레벨 | 비고 |
|---|---|---|
| BiFi·BTCFi·Swap·Gas Top-up 비즈니스 로직을 BFF 계약·TanStack Query hook 기반으로 통합 | Redacted-internal | pockie-ui PR 근거 |

### BTCFi 파트너 제품

| 주장 | 레벨 | 비고 |
|---|---|---|
| JPYC 스테이블코인 예치·인출·수익 청구 지원 파트너 제품 구현 | Redacted-internal | btcfi-partners-front PR 근거 |
| 비동기 입금·복구·epoch 출금·진행 대시보드 구현 | Redacted-internal | btcfi-partners-front PR 근거 |
| 파트너별 수명주기·정책 분리 구조 구축 | Redacted-internal | btcfi-partners-front PR 근거 |
| 초기 구축부터 릴리스까지 담당 | Redacted-internal | PR 타임스탬프로 확인 |

### Bifrost Explorer

| 주장 | 레벨 | 비고 |
|---|---|---|
| Blockscout 기반 Explorer 유지보수 | Redacted-internal | explorer-front 67 PR 근거 |
| Next.js App Router 전환 | Redacted-internal | 983개 파일 PR 근거 |
| /blocks LCP 3.7s→1.9s (↓49%), TBT 1,010ms→270ms (↓73%) | Redacted-internal + caveat | 로컬 Lighthouse 측정 — 프로덕션 RUM 아님 |
| /txs LCP 3.7s→2.2s (↓41%), TBT 1,330ms→200ms (↓85%) | Redacted-internal + caveat | 로컬 Lighthouse 측정 |
| /tokens LCP 3.3s→1.8s (↓45%), TBT 510ms→190ms (↓63%) | Redacted-internal + caveat | 로컬 Lighthouse 측정 |
| 테스트넷·메인넷 Docker image 런타임 환경변수 주입 구조 전환 | Redacted-internal | explorer-front PR 근거 |

### AI Agent 런타임

| 주장 | 레벨 | 비고 |
|---|---|---|
| 코드 리뷰 workflow 구성, confidence verifier, Jira 티켓 검증, 품질 게이트 연결 | Redacted-internal | Donald repo 21 PR 근거 |
| dynamic tools 구조 전환 (MCP 중복 실행 제거) | Redacted-internal | Donald repo PR 근거 |
| Codex app server 기반 전환 | Redacted-internal | Donald repo PR 근거 |
| prompt injection·외부 코드 실행·전역 package 변경 리스크 통제 | Redacted-internal | Donald repo PR 근거 |

### UI Kit (디자인 시스템) — Figma Code Connect

| 주장 | 레벨 | 비고 |
|---|---|---|
| 합성 컴포넌트의 동적 children을 정적 매핑으로 표현할 수 없어 Template V2 도입 | Redacted-internal | ui-kit-front 커밋 근거 (engineer-provided) |
| 런타임에 인스턴스를 순회하고 자식 컴포넌트 템플릿을 재귀 실행 | Redacted-internal | Tabs·Toast `findConnectedInstances` + `executeTemplate` 확인 |
| 20개 컴포넌트 중 14개에 동적 API 적용 | Redacted-internal | 커밋 분석으로 확인 |
| Code Connect CLI와 연동해 Figma MCP 코드 생성 컨텍스트를 정형화 | Redacted-internal + Self-attested | CLI 연동은 `figma.template.config.json`으로 확인; MCP 컨텍스트 개선은 본인 확인 |
| 해당 작업은 브랜치 전용 (main/develop 미병합) | Redacted-internal | PR 1건(v0.1.8 릴리즈)만 main 병합 |

---

## 스마트마인드 경력

| 주장 | 레벨 | 비고 |
|---|---|---|
| ANTLR 문법을 Monaco Editor에 연결한 SQL Editor 개발 | Public | velog 기술 글 + resume |
| JupyterLab Workspace 개발 | Public | velog + resume |
| 비정형 Query Viewer 가상화·페이지네이션·lazy loading 적용 | Public | velog + resume |
| pnpm·Turborepo 모노레포 전환 | Public | velog + resume |
| 빌드 시간 7분 → 1분 단축 | Public | velog + resume (당시 측정 기준) |
| FastAPI PyTorch 모델 서빙 구현 | Public | resume |
| Docker Compose 배포 환경 구성 | Public | resume |
| Frontend Part Leader 역할 | Public | resume |
| Playwright E2E on GitHub Actions | Public | velog |

---

## 주의 필요 주장

| 주장 | 주의 이유 |
|---|---|
| Lighthouse 수치 | 로컬 측정 환경 — 프로덕션 실사용자 측정(RUM)과 다를 수 있음 |
| 일본 액티브 유저 750명대 | Self-attested, 면접에서 "팀 공유 수치 기준"으로 답변 |
| 실제 입금 1억 엔대 | Self-attested, 동일 |
| 빌드 시간 7분→1분 | "당시 측정 기준"으로 환경 명시 필요 |
