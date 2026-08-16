# Decision Register (의사결정 등록부)

| 항목 | 내용 |
|------|------|
| Document ID | PP-SA-DR-001 |
| Document Type | Decision Register |
| Status | WORKING (파일 단위) |
| Source of Truth | NO (WORKING 단계) |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |

> ⚠️ **이 문서는 파일 전체를 APPROVED로 승격하지 않는다.**
> 각 Decision은 개별 상태(APPROVED / PROPOSAL / PENDING)를 유지한다.

---

## 1. Architecture 주요 결정

| ID | 결정 | 상태 | 관련 문서 |
|----|------|------|-----------|
| AD-001 | PayPlay 3축 구조 확정 (OSP / OC / Business OS) | APPROVED | SERVICE_BOUNDARIES.md |
| AD-002 | PayPoint Product Owner = Marketing Play / Hosted In = Business OS / Business OS는 Merchant Operating Surface 담당 | APPROVED | PAYPOINT_RELATIONSHIP.md |
| AD-003 | Person Master 물리 위치 | PENDING | 10_OC/09_DECISIONS/PENDING_REGISTER.md |
| AD-004 | Merchant Account 최종 구조 | PENDING | 10_OC/09_DECISIONS/PENDING_REGISTER.md |
| AD-005 | Shared IAM 물리 Architecture | PENDING | 10_OC/09_DECISIONS/PENDING_REGISTER.md |
| AD-006 | Device / Asset Owner | PENDING | ENTITY_OWNERSHIP_MATRIX.md — 근거 확정 전 배정 보류 |
| AD-007 | Product / Commercial Policy Master Owner = OC | APPROVED | 10_OC/06_ENTITY_DATA/SHARED_ENTITY_DECISION_APPLIED.md |
| AD-008 | Lead Source/Creation = OSP, Accepted 이후 Sales Execution = OC (Received ≠ Accepted) | APPROVED | 30_OSP/08_HANDOFF/OSP_OC_HANDOFF.md |
| AD-009 | OSP 공식명 = Online Sales Platform / 온라인 영업 플랫폼 | APPROVED | 30_OSP/README.md |
| AD-010 | PPOS = PayPlay Business OS 내부 공식 약칭 (별도 Product 아님) | APPROVED | OWNER_DECISIONS.md |

---

## 2. PM Gate 판정 결과

| Gate | 판정 |
|------|------|
| Final Documentation Gate | PASS WITH PENDINGS |
| Follow-up Architecture Gate | APPROVED |
| Development Planning / Specification Gate | CONDITIONALLY APPROVED |
| **Development Ready** | ❌ **아직 아님** — 별도 Gate 재검수 필요 |
| **QA Ready** | ❌ **아직 아님** |

---

## 3. APPROVED 공식 기준문서 (Status: APPROVED / Source of Truth: YES)

| 문서 | 경로 |
|------|------|
| OC Traceability & Gap Audit v1.1 | 10_OC/10_AUDIT/OC_TRACEABILITY_GAP_AUDIT_v1.md |
| OC User & Operations Flows | 10_OC/04_FLOWS/user-and-operations-flows.md |
| OC Detailed Requirements & Business Policies | 10_OC/05_REQUIREMENTS_POLICIES/detailed-requirements-and-business-policies.md |
| OC Entity / Data Architecture | 10_OC/06_ENTITY_DATA/ENTITY_DATA_ARCHITECTURE.md |
| OC Shared Entity Decision Applied | 10_OC/06_ENTITY_DATA/SHARED_ENTITY_DECISION_APPLIED.md |
| OC Decision Register | 10_OC/09_DECISIONS/DECISION_REGISTER.md |
| OSP → OC Handoff | 30_OSP/08_HANDOFF/OSP_OC_HANDOFF.md |
| OSP Lead / Person / Store Relationship | 30_OSP/13_ENTITY_RELATIONSHIPS/LEAD_PERSON_STORE_RELATIONSHIP.md |

---

## 4. Gate 판정 이력

| 일자 | Gate | 판정 |
|------|------|------|
| 2026-08-15 | Repository Initial Architecture | PASS WITH PENDINGS |
| 2026-08-15 | Architecture 표현 검수 | REVISION REQUIRED → 반영 완료 |
| 2026-08-15 | Status 정합성 검수 | PASS WITH MINOR REVISION → 반영 완료 |
| 2026-08-15 | Cross-Service Baseline Alignment | **PASS** |
| 2026-08-16 | 4개 세션 정식 입고 (OC / Business OS / OSP / PayPoint, 74건) | **PASS WITH MINOR CLEANUP** |
| 2026-08-16 | PayPoint Documentation State Cleanup | **PASS** |
| 2026-08-16 | Shared Architecture Baseline 재정합성 | 완료 — Main PM 검수 대기 |
| 2026-08-16 | Cross-Service Repository Traceability Audit | **진행 예정** |

---

## 5. 관련 문서

- [SERVICE_BOUNDARIES.md](./SERVICE_BOUNDARIES.md) — 서비스 경계
- [ENTITY_OWNERSHIP_MATRIX.md](./ENTITY_OWNERSHIP_MATRIX.md) — Entity 소유권
- [01_OWNER_INTENT/OWNER_DECISIONS.md](../01_OWNER_INTENT/OWNER_DECISIONS.md) — Owner Decision
- [80_DEVELOPMENT/DEVELOPMENT_GUARDRAILS.md](../80_DEVELOPMENT/DEVELOPMENT_GUARDRAILS.md) — 개발 가드레일
