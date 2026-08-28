# AAG Changelog

## v2.2 — 2026-08-28

### 리뷰어: Antigravity (agy)
### 승인: Chris

### 변경 내용

#### AAG v2.0 (Harness Architecture) 보완 개정
- **Contract-First & Deterministic Verification 명문화**: APEI 각 단계에 입력/출력 스키마 명세 및 단일 검증 명령어(`verification_command`) 강제.
- **수정 범위 격리 (Scope Boundaries)**: AI가 임의로 전역 설정/프로젝트 환경을 수정하지 못하도록 `Allowed Scope`와 `Forbidden Scope` 규칙 규정.
- **APEI-H Protocol 구체화**:
  - `Analyze`: 추측 기반 코딩 금지, 모호한 요구사항 질의 명확화.
  - `Plan`: 하위 태스크(DAG) 분해 기준 수립.
  - `Execute`: 컨텍스트 세션 분리(Isolation), 원자적 변경(Atomic Changes - 단일 작업당 최대 5개 파일), `Forbidden Scope` 명시.
  - `Iterate`: 사람의 육안 검수 대신 Exit Code 0 기반 3단계 검증 및 자가 치유(최대 3회), 초과 시 Git 자동 롤백.
- **Hook Lifecycle 강화**: `UserPromptSubmit`, `PreExecution`, `PostToolUse`, `WorkerVerify`, `Stop` 5대 훅의 책임, 트리거, 실패 시 트리거 동작 명시.
- **자원 한도 (Resource Limits) & Human Escalation Triggers**:
  - 서브태스크 당 최대 5턴, 3회 자가치유 리트라이 한도 규정.
  - 아키텍처 코어 변경, 보안/권한, 비용/배포, 치유 실패 시 인간 승인 위임 트리거 설정.

---

## v2.1 — 2026-07-16

### 리뷰어: Antigravity (agy)
### 승인: Chris

### 변경 내용

#### Section 0: Identity → Operating Context
- **이전:** "You are Tram" — 단일 모델 persona 선언
- **이후:** 멀티모델 호환 프레임 — Codex/Claude/agy/Gemini/Hermes 모두 Tram Conductor 역할로 동작
- **이유:** 각 모델의 내장 identity와 충돌 방지. 도구 중립적 지침으로 전환.

#### Operational Principles: TOON → Compact Output Format
- **이전:** TOON(Token-Oriented Object Notation) — 비공식 표준, 모델 혼란 유발
- **이후:** 마크다운 테이블, key-value 리스트, 최소 JSON 중심으로 구체화
- **이유:** TOON은 공식 명세 없음. 실제 모델이 따를 수 있는 구체적 가이드로 교체.

#### Context Engineering 확장
- **이전:** RAG 검색에 한정된 컨텍스트 엔지니어링
- **이후:** file read, web search, MCP tool call, RAG, session memory 전반으로 확장
- **이유:** 현재 모델들의 컨텍스트 수집 방식이 RAG 이상으로 다양해짐.

#### Execute 병렬 실행 표현 현실화
- **이전:** "독립된 작업은 병렬로 동시 실행" — 단일 에이전트에서 불가능
- **이후:** 개념적 분해 후 순차 실행, multi-agent 가용 시 위임 명시
- **이유:** 단일 turn 모델에서 실질적 병렬 실행은 불가. 현실적 표현으로 수정.

#### Tram Central Model: Decision Rules 추가
- 간단/복잡/고위험 작업에 따른 판단 기준 명시

#### Recent Updates (Blog) 제거
- 실행 지침 문서와 블로그 형식 혼재 제거
- 변경 이력은 이 CHANGELOG.md로 분리

#### ~/AGENTS.md 전역 심볼릭 링크 설정
- `~/AGENTS.md` → `~/.codex/AGENTS.md` 심볼릭 링크 생성
- agy, Claude, Gemini 등 모든 도구가 동일한 Tram AAG v2.1을 전역으로 참조

---

## v2.0 — 2026-02-23

- Tram AAG 초기 문서화
- APEI Protocol 정의
- Plugin Ecosystem (Sales, PM, Dev, Legal) 정의
- Tram Constitution 4원칙 수립
- TOON 포맷 도입
