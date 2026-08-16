# Entity Ownership Matrix (엔터티 소유권 매트릭스)

| 항목 | 내용 |
|------|------|
| Document ID | PP-SA-EOM-001 |
| Document Type | Shared Architecture — Entity Ownership |
| Status | WORKING |
| Source of Truth | NO (WORKING 단계) |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | ❌ Physical Schema 확정 근거로 사용 불가. Logical Ownership 참조용. |

> 2026-08-16 — 최신 Shared Entity Decision 기준으로 재정합성.
> **Pending 항목은 임의 확정 금지.** 근거 없이 Owner를 배정하지 않는다.

---

## 1. Entity Ownership

| Entity | Owner | Shared With | Status | 근거 / 비고 |
|--------|-------|-------------|--------|-------------|
| **Customer Account** | OC | OSP, Business OS | APPROVED | 동일 실질 운영관계 고객그룹. 법적 계약·세금·PG·정산 주체 아님 |
| **Store** | OC | OSP, Business OS, PayPoint | APPROVED | 동일 장소·운영 연속성 시 기존 Store ID 유지 후보. 타지역 이전은 신규 Store 우선 |
| **Legal Entity** | OC | — | APPROVED | 단일 고정값 아님. 역할·기간별 Assignment History로 관리 |
| **Person** | **TBD** | 전체 | **PENDING** | Logical Reference 사용 가능 / **물리 위치·Owner 확정 금지** |
| **Product** | OC | OSP(표현), Business OS(소비) | APPROVED | OC = Product / Commercial Policy Master Owner |
| **Offer** | OC | OSP | APPROVED | OSP는 승인된 Offer를 외부에 표현. Master 소유 아님 |
| **Lead** | OSP (Source/Creation) | OC (Accepted 이후) | APPROVED | Received ≠ Accepted. Accepted 시점에 OC로 책임 이전 |
| **Quote** | OC | — | APPROVED | Quote / Quote Revision 분리. 발송본 불변 |
| **Contract** | OC | Business OS(결과 Projection) | APPROVED | Contract Header / Contract Item 분리 |
| **Merchant Account** | **TBD** | — | **PENDING** | Customer Account/Store/User Identity와 동일 Entity 선확정 금지. 독립 Table 선생성 금지 |
| **Role / Permission** | **TBD (Logical: OC)** | 전체 | **PENDING** | Logical Permission 요구사항 사용 가능 / Shared IAM 물리 Architecture 확정 금지 |
| **Device / Asset** | **TBD** | OC, Business OS | **PENDING** | 근거 확정 전 배정 보류 |
| **PayPoint** | **Marketing Play** | Business OS (Hosted In) | APPROVED | Business OS = Merchant Operating Surface 담당 |

---

## 2. 승인 기준 (변경 금지)

| 항목 | 기준 |
|------|------|
| Product / Commercial Policy Master Owner | **OC** |
| Lead Source / Creation | **OSP** |
| Lead Accepted 이후 Sales Execution | **OC** |
| PayPoint Product Owner | **Marketing Play** |
| PayPoint Hosted In | **PayPlay Business OS** |

---

## 3. Structural Pending (P0 — 임의 확정 금지)

| ID | 항목 | 사용 가능 범위 | 확정 금지 범위 |
|----|------|---------------|---------------|
| P-001 | Person Master 물리 위치 | Logical Person / Contact Relationship | Physical DB / Owner |
| P-002 | Merchant Account 최종 구조 | 분리 필요성 인식 | Entity 동일화 / 독립 Table 선생성 |
| P-003 | Shared IAM 물리 Architecture | Logical Permission 요구사항 | User / Auth / Session / Membership Physical Schema |
| P-004 | Device / Asset Owner | — | Owner 배정 (근거 확정 전) |

---

## 4. 변경 이력

| 일자 | 항목 | 변경 내용 |
|------|------|-----------|
| 2026-08-15 | Device | Owner = OSP 삭제. 근거 없음 확인 → PENDING 전환 |
| 2026-08-16 | 전체 | 4개 세션 정식 입고 문서 기준 재정합성. Offer / Lead / Product / Role·Permission / PayPoint Entity 추가 |

---

## 5. 관련 문서

- [10_OC/06_ENTITY_DATA/SHARED_ENTITY_DECISION_APPLIED.md](../10_OC/06_ENTITY_DATA/SHARED_ENTITY_DECISION_APPLIED.md) — Shared Entity Decision 적용 기준 (APPROVED)
- [10_OC/06_ENTITY_DATA/ENTITY_DATA_ARCHITECTURE.md](../10_OC/06_ENTITY_DATA/ENTITY_DATA_ARCHITECTURE.md) — OC Entity / Data Architecture
- [10_OC/09_DECISIONS/PENDING_REGISTER.md](../10_OC/09_DECISIONS/PENDING_REGISTER.md) — OC Pending Register
- [30_OSP/13_ENTITY_RELATIONSHIPS/LEAD_PERSON_STORE_RELATIONSHIP.md](../30_OSP/13_ENTITY_RELATIONSHIPS/LEAD_PERSON_STORE_RELATIONSHIP.md) — Lead / Person / Store 관계
