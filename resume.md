# 정소원 (Sowon Jung)
Software Engineer | Product Engineer | Frontend Developer · 010-9349-1709 · swj960515@gmail.com · github.com/ss-won · linkedin.com/in/sowon-jung-573867193 · velog.io/@ss-won

## 프로필

React·TypeScript 기반 제품 화면 구현과 BFF 설계에서 출발해, 현재는 LLM 기반 AI Agent 런타임 개선과 MCP 연동 개발 도구 자동화까지 직접 구축·운영하고 있습니다. 성능 병목을 찾아 측정 가능한 수치로 증명하는 방식을 선호하고, 필요하면 NestJS·FastAPI 같은 프론트엔드 바깥 영역도 스스로 다룹니다. 기술적인 토론과 질문이 자유로운 팀에서 더 좋은 성과를 냅니다.

## 경력

### 파이랩테크놀로지 · Frontend Developer
2024.09 – 현재 (1년 11개월)

블록 탐색기 성능 최적화·WebView 거래 화면 BFF 설계, AI Agent 런타임·MCP 도구 자동화를 맡고 있습니다.

**사용 기술:** TypeScript, React, Next.js(App Router), TailwindCSS, TanStack Query, Jotai, NestJS, wagmi·viem, Chakra UI, Vitest, Playwright, Sentry

- 블록 탐색기 목록 화면 성능 최적화 — 단계적 렌더링·WebSocket 배치 처리로 LCP 평균 ↓45%, TBT 평균 ↓74% 달성 (3개 주요 화면 기준)
- Mobile App·Chrome Extension에서 동일한 WebView 거래 화면 재사용 — BFF 계약 기반 책임 경계 분리, postMessage 프로토콜 설계로 클라이언트별 분기 코드 제거
- 파트너사 모바일 지갑 WebView DApp 출시 — 출시 3개월 만에 일본 액티브 유저 750명대·실제 입금 1억 엔대 달성
- 다수 RPC·사내 API 직접 분기 호출 구조를 BFF 집계 엔드포인트로 재설계 — race condition 원천 차단, 자산 수치 일관성 확보
- 사내 LLM 기반 AI Agent 런타임 개선 — MCP lazy-proxy(on-demand spawn)로 메모리 경합 제거, confidence verifier(임계값 0.8)·CI 품질 게이트 기반 자동 코드 리뷰 workflow 구성, Codex app server 전환 및 3단계 보안 레이어 + workspace sandbox 격리
- Figma Template V2 API + Code Connect CLI로 디자인 시스템 MCP 컨텍스트 자동 생성 — Agent 코드 생성 시 컴포넌트 선택 정확도 향상

### 스마트마인드 · Frontend Developer → Frontend Part Leader
2021.07 – 2024.09 (3년 2개월)

AI 데이터 분석 플랫폼 Workspace의 SQL Editor·Query Viewer 모듈을 개발했으며, pnpm·Turborepo 모노레포 전환과 Microfrontend 설계를 주도했습니다. 후반에는 프론트엔드 파트 리더로 팀 운영을 담당했습니다.

**사용 기술:** TypeScript, React, Next.js, Vite, Monaco Editor, ANTLR, pnpm, Turborepo, Playwright, FastAPI, Docker Compose

- Workspace First Load 최대 40% 단축 — vite rollup manualChunk·tree-shaking·dynamic import·React Suspense 조합 적용
- pnpm·Turborepo 모노레포 전환 및 빌드 캐시 도입으로 앱별 빌드 시간 7분 → 1분 단축 — CI 대기 시간 감소로 팀 전체 배포 리드타임 개선
- SQL Editor 모듈 개발 — ANTLR 문법을 Monaco Editor에 연결해 SQL 구문 강조·자동완성 제공
- Microfrontend 설계·구현 — iframe+postMessage(Lab·Main 간 통신), module federation(Query Manager·File Manager)
- 비정형 데이터 Query Viewer 성능 개선 — 서버 페이지네이션·가상 스크롤·미디어 lazy loading으로 대용량 결과 렌더링 안정화
- FastAPI·Docker Compose로 AI 예측 모델 서빙 인프라 구성 및 데이터 수집·전처리 파이프라인 직접 개발
- 파트 리더로서 프론트엔드 3인 팀 업무 배분·코드 리뷰·기술 의사결정 주도

---

## 주요 성과

### 01 / 프론트엔드 성능 병목 개선

| Route | LCP (before → after) | TBT (before → after) | 개선 |
|---|---|---|---|
| /blocks | 3.7s → 1.9s | 1,010ms → 270ms | LCP ↓49% · TBT ↓73% |
| /txs | 3.7s → 2.2s | 1,330ms → 200ms | LCP ↓41% · TBT ↓85% |
| /tokens | 3.3s → 1.8s | 510ms → 190ms | LCP ↓45% · TBT ↓63% |

- 초기 렌더링 범위 제한·단계적 렌더링·WebSocket 30초 배치 처리 — 목록 화면 첫 페인트 시 불필요한 렌더 트리 축소
- 가스 충전 서비스 1+N 조회 → 지원 토큰 기준 단일 조회로 재설계, SDK 중복 asset fetch 제거
- bridge pair 조회 1+N → 2회 캐시 조회로 축소 — API 호출 수 감소 및 응답 일관성 확보

### 02 / 모바일 WebView 거래 제품 출시

- BFF 계약 기반 책임 경계를 정의해 Mobile App·Chrome Extension 양쪽에서 동일한 WebView 거래 화면을 재사용 — 클라이언트별 분기 코드 제거, 신규 플랫폼 온보딩 비용 최소화
- iOS·Android·Extension 버전별 feature flag를 BFF config v2에 구현 — 클라이언트 재배포 없이 서버에서 기능 노출 제어

**결과:** 파트너사 모바일 지갑 WebView DApp 출시 3개월 — 일본 액티브 유저 750명대·실제 입금 1억 엔대 달성

### 03 / 사내 LLM 기반 AI Agent 런타임 개선

- MCP lazy-proxy 도입 — 매 request마다 서버 전체를 spawn하던 구조를 on-demand spawn으로 전환해 동시 요청 시 메모리 경합 제거
- confidence verifier(임계값 0.8)·CI 품질 게이트로 자동 코드 리뷰 workflow 구성 — 최종 머지는 사람이 확인하는 운영 원칙 유지, 리뷰 편의성만 자동화
- Codex app server 전환 및 3단계 보안 레이어(활성화 검사·bash 안전성·write 승인) 적용, 외부 코드 실행·환경 오염 가능 작업은 workspace sandbox로 완전 격리
- Figma Template V2 API + Code Connect CLI로 디자인 시스템 MCP 컨텍스트 자동 생성 — Agent가 컴포넌트를 직접 조회해 코드 생성 정확도 향상

---

## 학력 및 기타

### 학력
가천대학교 컴퓨터공학과 · GPA 3.98 / 4.5

### 자격증 및 활동
- 정보처리기사 (2019)
- OSSCA — TypeScript Handbook 한글화 (2020), githru-vscode-ext (2023)
- SmileGate Membership AI 1기 (2021)
- AUSG (AWSKRUG University Student Group) 1기 (2019)

### 어학
- 영어 — 기초 비즈니스
- 일본어 — 기초 비즈니스 (JLPT N3)
