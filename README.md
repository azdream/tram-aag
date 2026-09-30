# Tram AI Agent Governance (AAG)
> **Establishing a Stable Architecture for the Next Generation of AI Agents**

## Overview (개요)
[EN] This repository is the official public record of the **AI Agent Governance (AAG)** framework. We published this to define the operational principles, ethical boundaries, and architectural standards for Tram (트램) and its specialized plugin ecosystem. Our goal is to move beyond simple chat interactions toward a reliable, enterprise-grade multi-agent system.

[KR] 이 저장소는 **AI 에이전트 거버넌스 (AAG)** 프레임워크의 공식 공개 기록입니다. 트램(Tram)과 그 플러그인 생태계의 운영 원칙, 윤리적 경계, 그리고 아키텍처 표준을 정의하기 위해 이 내용을 공표했습니다. 단순한 대화형 AI를 넘어, 신뢰할 수 있는 엔터프라이즈급 멀티 에이전트 시스템으로 나아가는 것이 우리의 목표입니다.

---

## Why We Published This (공표 목적)
1. **Transparency & Trust**: To clearly state the "Constitution" that governs our AI agents, ensuring they remain helpful, harmless, and honest.
2. **Standardization**: To establish the **APEI Protocol** (Analyze-Plan-Execute-Iterate) as a stable design model for complex task handling.
3. **Efficiency**: To optimize **output quality** through compact, structured formats (markdown tables, key-value lists), reducing cognitive load while increasing accuracy.

1. **투명성과 신뢰**: 에이전트를 규제하는 '헌법'을 명시하여, AI가 항상 유익하고 무해하며 정직하게 동작하도록 보장합니다.
2. **표준화**: 복잡한 작업 처리를 위한 안정적인 설계 모델인 **APEI 프로토콜**(Analyze-Plan-Execute-Iterate)을 정립합니다.
3. **효율성**: 마크다운 테이블, key-value 리스트 등 간결하고 구조화된 출력 포맷을 통해 **정보 전달 효율**을 극대화하고, 정확도 향상을 달성합니다.

---

## Core Focus (주요 과제)
- **Semantic Ontology Architecture**: Grounding agent knowledge and actions in a formal Object-Property-Link-Action graph (OPLA) with object-level security policies.
- **Harness & Loop Engineering**: Developing a robust architecture where the Orchestrator (Tram) and specialized Plugins execute within bounded FSM loops with circuit breakers and deterministic rollbacks.
- **Typesafe AI & Schema-First**: Enforcing strict type contracts (Pydantic/Zod/TOON) and System One decision primitives (Noul, Choice, Score) to eliminate runtime hallucinations and enable zero-shot schema repairs.
- **Lightweight Model Optimization**: Maximizing cost-efficiency (>90% savings) and sub-second latency by empowering lightweight models (SLM, Flash/Mini) through typed sandboxes.
- **2-Tier Judgment Theory**: Implementing zero-cost deterministic validation (Tier-1) followed by selective semantic evaluation (Tier-2).
- **Enterprise Trust & Commercialization**: Ensuring B2B readiness with immutable audit trails, Zero-Cost routing for ROI predictability, explainable UI components, and real-time SLA monitoring.

- **시맨틱 온톨로지 아키텍처**: 비정형 텍스트 RAG를 넘어 객체-속성-연결-액션(OPLA) 지식 그래프를 통해 에이전트의 지식 접지와 객체 수준 보안 정책(ABAC/RBAC)을 확립합니다.
- **하네스 및 루프 엔지니어링**: 유한 상태 머신(FSM)과 서킷 브레이커, 결정론적 롤백을 통해 오케스트레이터(트램)와 플러그인이 안전하게 수렴하는 강건한 실행 환경을 구축합니다.
- **타입 세이프 AI & 스키마 우선**: Pydantic/Zod/TOON 및 System One 의사결정 프리미티브(Noul, Choice, Score)를 통해 런타임 환각을 원천 차단하고 즉각적인 스키마 자가 복구를 수행합니다.
- **경량 모델 최적화**: 정밀한 컨텍스트 슬라이싱과 타입 제약을 통해 경량 모델(SLM, Flash/Mini)로도 90% 이상의 비용 절감과 초저지연 고속 자동화를 실현합니다.
- **2단계 판정 체계**: 비용 $0의 기계적·결정론적 판정(Tier-1)과 선별적 의미론적 심사(Tier-2)를 결합하여 안정성과 경제성을 동시에 달성합니다.
- **상용화 및 신뢰 아키텍처**: 불변 감사 로그, 비용 예측 가능한 Zero-Cost 라우팅, 설명 가능한 UI 컴포넌트 및 실시간 SLA 모니터링 체계를 도입하여 기업용 B2B 환경에 대비합니다.

---

## Documents
- [AI Agent Governance & Architecture (v3.0)](./ai-agent-governance.md)
- [Changelog](./CHANGELOG.md)
