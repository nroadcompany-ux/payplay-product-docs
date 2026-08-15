# Decision Register (의사결정 등록부)

| 항목 | 내용 |
|------|------|
| Document ID | PP-SA-DR-001 |
| Document Type | Decision Register |
| Status | WORKING (파일 단위) |
| Source of Truth | NO (WORKING 단계) |
| Last Reviewed | 2026-08-15 |

> ⚠️ **이 문서는 파일 전체를 APPROVED로 승격하지 않는다.**
> 각 Decision은 개별 상태(APPROVED / PROPOSAL / PENDING)를 유지한다.

---

## Architecture 주요 결정

| ID | 결정 | 상태 | 관련 문서 |
|----|------|------|-----------|
| AD-001 | PayPlay 3축 구조 확정 (OSP / OC / Business OS) | APPROVED | SERVICE_BOUNDARIES.md |
| AD-002 | PayPoint는 Business OS에 Hosted, Owner는 Marketing Play, Business OS가 매장 운영 Surface 담당 | APPROVED | PAYPOINT_RELATIONSHIP.md |
| AD-003 | Person Master 물리 위치 | PENDING | — |
| AD-004 | Merchant Account 최종 구조 | PENDING | — |
| AD-005 | Shared IAM 물리 Architecture | PENDING | — |
| AD-006 | Device(단말기/장비) Owner | PENDING | ENTITY_OWNERSHIP_MATRIX.md — 근거 확정 전 배정 보류 |

---

## PM Gate 판정 결과

| Gate | 판정 |
|------|------|
| Final Documentation Gate | PASS WITH PENDINGS |
| Follow-up Architecture Gate | APPROVED |
| Development Planning / Specification Gate | CONDITIONALLY APPROVED |
| Development Ready | ❌ 아직 아님 — 별도 Gate 재검수 필요 |
| QA Ready | ❌ 아직 아님 |

---

## APPROVED 공식 기준문서 (Status: APPROVED / Source of Truth: YES)

| 문서 | 경로 |
|------|------|
| OC Traceability & Gap Audit v1.0 | 10_OC/10_AUDIT/OC_TRACEABILITY_GAP_AUDIT_v1.md |
| User & Operations Flows | 10_OC/04_FLOWS/user-and-operations-flows.md |
| Detailed Requirements & Business Policies | 10_OC/05_REQUIREMENTS_POLICIES/detailed-requirements-and-business-policies.md |

---

## Gate 판정 이력

| 일자 | Gate | 판정 |
|------|------|------|
| 2026-08-15 | Repository Initial Architecture | PASS WITH PENDINGS |
| 2026-08-15 | Architecture 표현 검수 | REVISION REQUIRED → 반영 완료 |
| 2026-08-15 | Status 정합성 검수 | PASS WITH MINOR REVISION → 반영 완료 |
| 2026-08-15 | Repository Initial Baseline v1.0 | 최종 PASS 대기 |
