# AAG Changelog
 
## v3.0 — 2026-09-30

### 리뷰어: Antigravity (agy)
### 승인: Chris

### 변경 내용

#### AAG v3.0 (Typesafe Harness, Semantic Ontology & Agentic Loop) 대규모 개정
- **Semantic Ontology (시맨틱 온톨로지 & 지식 그래프) 아키텍처 정립**:
  - 단순 텍스트 청크 RAG를 넘어선 **OPLA (Object-Property-Link-Action)** 온톨로지 모델 도입.
  - 엔티티 간 종속성과 비즈니스 불변식(Invariants)을 그래프로 구조화하여 관계적 환각 원천 방지.
  - 온톨로지 1~2홉 서브그래프 슬라이싱을 통한 경량 모델(SLM)의 Multi-hop 정밀 추론 구현.
  - 온톨로지 기반 객체 수준 보안 및 권한 제어(Object-Level RBAC/ABAC) 표준화.
  - 시맨틱 온톨로지 레이어 아키텍처 Mermaid 다이어그램 추가.
- **Harness Engineering (하네스 엔지니어링) 정립**:
  - 모델에 종속되지 않는 격리된 샌드박스 실행 환경(Sandbox Isolation) 규정.
  - 구문 트리(AST) 및 의존성 그래프 기반의 정밀 컨텍스트 슬라이싱(Context Slicing & Pruning) 표준화.
  - 실행 실패 및 이상 발생 시 Git 기반 체크포인트 즉각 복구(`git reset --hard`) 메커니즘 명문화.
- **Loop Engineering (루프 엔지니어링) 및 FSM 상태 머신 도입**:
  - 무한 루프 방지를 위한 수렴 보장(Halting Guarantee) 및 서킷 브레이커 도입.
  - 턴 한도(최대 5턴) 및 동일 에러 반복 탐지(Cycle Detection) 기반 조기 탈출 프로토콜 수립.
  - Mermaid 기반 루프 엔지니어링 FSM 상태 전이 다이어그램 추가.
- **Typesafe AI & Schema-First Protocol 명문화**:
  - 비정형 자연어 프롬프팅 지양, Pydantic / Zod / JSON Schema / TOON 기반의 강력한 입출력 타입 계약 강제.
  - 타입 불일치 시 LLM 재추론 없이 컴파일러/타입체커 에러 피드백을 통한 즉시 복구(Zero-shot Schema Repair) 체계 구축.
- **경량 모델(SLM / Flash) 최적화 전략 수립**:
  - Frontier LLM 의존도를 낮추고 Gemini Flash / Claude Haiku / 로컬 SLM 중심의 고속·저비용(90% 이상 절감) 아키텍처 제시.
  - 모델 캐스케이딩(Model Cascading): 아키텍처 수립(Frontier) → 구현/변환(SLM) → 검증/판정(결정론적 하네스).
- **Hybrid RAG & 2-Tier Judgment Theory (2단계 판정 이론)**:
  - Dense Vector + Sparse BM25 + AST Code Graph 하이브리드 검색 채택.
  - Tier-1(비용 $0, 100% 결정론적 기계 판정) 통과 시에만 Tier-2(의미론적 LLM-as-a-Judge)를 선별 적용하는 2단계 게이팅 체계 수립.
- **시각화 인프라 강화**:
  - `index.html` Docsify 내 Mermaid v10 렌더링 플러그인 장착.
  - 엔드투엔드 파이프라인, 루프 FSM, 2단계 판정 게이트 3대 Mermaid 플로우차트 공식 문서 삽입.

---

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
