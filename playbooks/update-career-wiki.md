# Playbook: Career Wiki 갱신

새로운 경력 데이터가 생겼을 때 이 위키를 갱신하는 절차.

## 갱신이 필요한 경우

- 새 직장 입사 또는 퇴사
- 주요 프로젝트 완료 (출시, 마이그레이션 완료 등)
- GitHub 스냅샷 갱신 (PR 집계)
- 새로운 면접 질문에서 이력서 주장의 방어 가능 여부가 바뀐 경우
- 공개된 사업 지표 (뉴스, 블로그, 공식 발표)로 self-attested 값을 승격할 수 있게 된 경우

## 갱신 절차

### 1. 원본 데이터 확인 (소스 우선순위 순서)

1. velog.io/@ss-won — 동시대 기록, 가장 높은 우선순위
2. ss-won/resume git 이력 — HEAD만 보지 말고 커밋 히스토리 확인
3. GitHub 집계 (pilab-sowon 계정, bifrost-platform org)
4. 로컬 CV PDF (raw-github-export/sowon-cv.pdf)

### 2. 공개 가능 여부 확인 (redaction-policy.md)

추가할 내용마다 확인:
- [ ] 비공개 저장소 링크 포함 여부
- [ ] 새로운 사업 지표 — 이미 공개된 이력서에 있는지
- [ ] 파트너·고객 이름 — 이미 공개된 이력서에 있는지
- [ ] 코드 발췌 포함 여부

### 3. 파일 갱신 순서

증거 우선, 파생 문서 나중:

1. `data/profile.json` — 집계 수치, 재직 기간 등
2. `wiki/achievements.md` — 새 업적 추가 또는 기존 업적 보강
3. `wiki/career-themes.md` — 새 테마 또는 기존 테마에 근거 추가
4. `wiki/resume-claims.md` — 새 주장과 증거 레벨 추가
5. `data/themes.json` / `data/claims.json` — JSON 업데이트
6. `wiki/evidence-index.md` — 새 공개 출처 추가
7. `llms.txt` — 새 파일이 생긴 경우 목록 업데이트

### 4. 확인 체크리스트

- [ ] 모든 새 주장에 증거 레벨 표시 (public / redacted-internal / self-attested / derived)
- [ ] self-attested 값은 "면접에서 어떻게 답변할 것인지" interview_note 포함
- [ ] 새 public 출처(velog 글 등)가 있으면 evidence-index.md에 추가
- [ ] 비공개 저장소 링크가 위키 파일에 없는지 grep으로 확인

```bash
grep -r "bifrost-platform" /Users/wish/resume/wiki/ /Users/wish/resume/data/
```

- [ ] 갱신 후 llms.txt의 파일 목록이 실제 파일과 일치하는지 확인

### 5. 커밋

```bash
cd /Users/wish/resume
git add wiki/ data/ playbooks/ prompts/ llms.txt
git commit -m "wiki: <갱신 내용 한 줄 요약>"
git push
```

## 자주 하는 실수

- **내부 PR 링크 실수로 포함**: push 전에 반드시 grep으로 확인
- **self-attested를 public으로 오분류**: 외부에서 검증 가능하지 않으면 self-attested
- **파생 데이터(merge rate 등)를 직접 측정된 것처럼 표현**: derived 레벨로 명시
- **증거 레벨 없이 새 주장 추가**: 모든 주장에 레벨 필수
