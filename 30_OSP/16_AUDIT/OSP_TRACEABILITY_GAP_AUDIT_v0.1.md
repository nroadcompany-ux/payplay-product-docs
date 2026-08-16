# OSP Traceability & Gap Audit v0.1

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/16_AUDIT/OSP_TRACEABILITY_GAP_AUDIT_v0.1.md` |
| Document ID | `PP-OSP-AUDIT-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Gap / Readiness / Traceability 검수용 |

---

## 1. Traceability Chain

```text
Owner Decision
→ OSP Definition / Scope
→ 8 Domain Architecture
→ Capability
→ User / Operations Flow
→ Business Policy
→ Lead / Handoff
→ Outcome / Attribution
→ OSP Admin
→ Development Slice
```

---

## 2. Boundary Trace

### OSP
Traffic → Discovery → Conversion → Lead → Handoff → Attribution → Marketing Decision

### PayPlay OC
Accepted → Assignment → Consultation → Quote → Contract → Installation / Operations

**Boundary Check: PASS**

OSP가 사람 상담·계약 실행 State의 Master로 확장되지 않도록 유지한다.

---

## 3. Product Ownership Trace

POS / 키오스크 / 테이블오더 / 카드단말기는 OSP 하위 Product가 아니다.

**Boundary Check: PASS**

---

## 4. Commercial Policy Trace

Product / Commercial Policy Master = PayPlay OC  
OSP = Approved Offer Presentation

**Boundary Check: PASS**

---

## 5. Major Implementation Gaps

### P0 / Critical
- 민감 Onboarding Document Storage Public-read 위험
- Runtime Code ↔ Managed Schema Drift
- Automated Regression Evidence 부재
- OSP → OC Accepted Physical Interface 미확정
- OC → OSP Contract / Revenue Outcome Interface 미확정

### High
- Advertising Spend Source / API 미확정
- Shared IAM / Role-Permission Physical Model 미확정
- Marketing Performance Admin MOCK 제거 필요

### Working
- Attribution Model / Window
- KPI 공식 명칭·산식
- Experiment / Learning
- Nurture
- AI Recommendation / Execution
- Advanced Smart Ground

---

## 6. Readiness

- Recovery: PASS WITH NOTES
- Logical Architecture: PASS WITH NOTES
- Flow / Policy: PASS WITH NOTES
- Development Planning: CONDITIONALLY AVAILABLE
- Development Ready: NO
- QA Ready: NO

---

## 7. Remaining Main PM Decision

별도 Owner Decision 또는 Common Infrastructure Decision이 필요한 항목:

- Person Master 물리 위치
- Merchant Account 최종 구조
- Shared IAM 물리 Architecture
- Advertising Spend Source / API
- Attribution 세부 Rule / Window
- AI External-impact Execution 권한
