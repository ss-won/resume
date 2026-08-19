# Cross-Cutting Engineering Themes — 정소원 (Sowon Jung)

이 문서는 단일 프로젝트가 아닌 여러 제품·회사에 걸쳐 반복 확인된 역량 테마를 정리한다. 각 테마에 근거 레벨을 명시한다.

Evidence levels: **Redacted-internal** = private GitHub 근거, 링크 비공개 · **Public** = 공개 velog/resume 근거

---

## 1. 권한 위임 경계 설계 (postMessage)

**Evidence:** Public (resume) + Redacted-internal · 두 회사에서 반복

| 시기 | 제품 | 위임 대상 |
|---|---|---|
| 2021–2024 · ThanoSQL | JupyterLab을 iframe으로 제품 안에 통합, 제품 로그인으로 세션 위임 | 인증·세션 |
| 2024– · Pockie WebView | 거래 화면이 직접 서명하지 않고 네이티브 호스트(앱·지갑)에 위임 | 키·서명·RPC |

두 환경 모두 "권한을 가진 쪽은 따로 있고 화면은 경계 너머로 그것을 위임받는다"는 동일한 구조 문제다. 4년 간격으로 두 번 구현했다.

---

## 2. 거래 금액 경계 계산 + 가스 추정 통합

**Evidence:** Redacted-internal · 여러 DeFi 제품에서 반복

여러 DeFi 제품에서 거래 최대/최소 금액을 가스·수수료·정책과 통합 계산해 전송 전 실패·과다 입력·오분기를 구조적으로 제거했다. 관련 제품: Lending(BiFi), Swap, Bridge, BTCFi, BiQuid.

---

## 3. 거래 실패 복구 / 자금·단계 고착 방지

**Evidence:** Redacted-internal · 금융 신뢰성 핵심

서명 거부·중단·재진입 시 사용자가 자금이나 거래 단계에 고립되는 edge case를 다층 복구 로직으로 제거. 사례: Native BTC 입금 실패 시 WebView storage 복구, CREATED orphan process 복구, pending 재개, dialog stale 값 리셋.

---

## 4. 성능·API 호출 최적화 (정량 근거 다수)

**Evidence:** Public (resume LCP/TBT 수치) + Redacted-internal

측정 기반 최적화 사례:
- Explorer 블록/트랜잭션/토큰 화면: 로컬 Lighthouse LCP 43~49%, TBT 63~84%, Speed Index 55~63% 개선
- 앱 홈 API 호출 수: 25~46회 → 17회
- WebView balance refetch interval: 90초 → 30초
- AI agent 메모리 주입량: -72%

**가상화 판단 — 같은 도구에 반대 결론:**
- ThanoSQL Query Viewer: 행 수 많고 행 가벼움 → 가상화 채택
- Bifrost Explorer: 행 하나가 무거움(실시간 데이터·차트·이미지) → 가상화 제거 후 점진 렌더링

같은 사람이 반대 결정을 내리고 둘 다 이유를 설명할 수 있다.

---

## 5. Web3 지갑 연결·전송 계층

**Evidence:** Redacted-internal · 여러 지갑/프로바이더 커버

EIP-6963 커넥터 매칭, WalletConnect QR, 다중 프로바이더 연결 상태·세션·체인 전환을 아우르는 지갑 연결/전송 계층 설계·안정화. WebView RPC routing 경계, transaction controller pendingTx, ERC20 transfer 분기 포함.

---

## 6. 테스트 인프라·E2E 자동화

**Evidence:** Redacted-internal

- Jest → Vitest 전환 (Bifrost Explorer)
- Playwright E2E: page object 모델, 네트워크 mocking, WebSocket 갱신, 레이아웃 시프트 검증
- 61개 파일 규모 WebView E2E 기반 구축
- 플랫폼별(iOS·Android·Extension) feature flag E2E 검증

---

## 7. 관측성 — Sentry·LLM observability

**Evidence:** Redacted-internal

- Sentry 거래 로깅 체계·v2 스키마 (WebView 거래 이벤트 수집, calldata 실패 진단)
- axios interceptor Sentry 연동 (BFF 레이어)
- Langfuse LLM observability: cost·feedback score·rate-limit HUD, token usage 관측

---

## 8. 대규모 마이그레이션

**Evidence:** Redacted-internal (규모만 공개)

- Bifrost Explorer: 983개 파일 Next.js 15 App Router 전환
- BTCFi 파트너: 257개 파일 파트너 플로우 구현
- AI Agent 런타임: 299개 파일 Codex App Server 전환

---

## 9. 플랫폼 전반 보안 위생

**Evidence:** Redacted-internal · 다수 저장소 일괄 적용

SSRF 방지(image 도메인 제한), Next.js/axios/web3/react-query CVE 패치, response security headers, Sentry PII 비활성화, NFT iframe sandbox를 10개 저장소에 걸쳐 일괄 적용.

---

## 10. 필요한 계층을 직접 만드는 패턴

**Evidence:** Public (resume) · 두 회사에서 반복

- 스마트마인드: 예측 모델 조회를 위한 FastAPI 직접 구현 + Docker Compose 배포
- Bifrost: BTCFi 파트너·Swap·Gas Top-up BFF를 NestJS로 직접 구현

프론트엔드에서 멈추지 않고 소비자 입장에서 필요한 서버 계층을 직접 만드는 패턴이 두 회사에서 반복됐다.

---

## 지원 포지션별 강조 테마

| 포지션 | 앞에 둘 테마 |
|---|---|
| 핀테크·거래소·금융 | 2(금액경계) · 3(실패복구) · 9(보안) |
| Web3 인프라·지갑 | 5(지갑연결) · 1(권한위임) · 2(금액경계) |
| 프론트엔드 플랫폼·대규모 웹 | 8(마이그레이션) · 4(성능) · 6(테스트) |
| AI 플랫폼·생산성 | D(AI Agent) · 7(관측성) · 4(성능/비용) |
| 스타트업·풀스택 | 10(계층 직접 구현) · 4(최적화) · 6(테스트) |
| 모바일 WebView | 1(권한위임) · 3(실패복구) · 6(E2E) |
