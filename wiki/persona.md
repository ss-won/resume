# Working Style and Persona — 정소원 (Sowon Jung)

엔지니어 본인이 직접 기술한 성향과 작업 방식.

## 자기 기술

- 서비스의 초기 설계부터 최적화 지점을 찾아가는 것을 좋아한다.
- 병목을 찾아 개선하는 과정을 즐긴다.
- 필요하면 BFF·FastAPI처럼 프론트엔드 바깥 영역도 직접 다룬다.
- 기술적인 토론을 즐기고, 팀원들과 기술적 문제를 함께 정의하고 해결하는 환경에서 강점을 발휘한다.
- 모르는 것을 편하게 물어볼 수 있는 분위기에서 가장 잘 일한다.
- 프론트·백엔드 도메인을 가리지 않고 기술을 써보는 것을 좋아한다.

## 포지셔닝 우선순위

1. **WebView / mobile-web product engineering** — 앱–WebView–지갑–BFF 경계
2. **Frontend and product engineering** — 대규모 마이그레이션, 성능, 테스트
3. **Web3 wallet, DeFi, transaction UX** — 거래 안정성, 금액 경계
4. **Full-stack product ownership** — BFF, 테스트, CI, AI agent runtime

## 관심 영역

- AI Agent 설계 및 런타임 개선 (MCP, tool permission, observability)
- Frontend Development Engineer (FDE) / Developer Tooling
- 풀스택 인턴십 (frontend-heavy)

## 작업 방식 특징

- 측정 없이 최적화하지 않는다. Lighthouse·API 호출 수·토큰 비용을 먼저 측정하고 개선한다.
- 경계를 명확히 하는 설계를 선호한다 (BFF 계약, WebView RPC routing, tool permission gate).
- 단위 테스트로는 잡히지 않는 통합 버그를 E2E로 잡는 것을 중요하게 생각한다.
- 팀원이 "왜 이렇게 결정했는지"를 나중에 이해할 수 있도록 PR에 맥락을 남긴다.
