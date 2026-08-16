# Decision Queue / Pending

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/15_DECISIONS/DECISION_QUEUE_PENDING.md` |
| Document ID | `PP-OSP-DQ-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Decision / Pending 추적용 |

---

## APPROVED / Closed Decisions

### OSP-DQ-001
Lead 생성 / Handoff / OC 내부 Sales Execution Boundary  
**Status: APPROVED**

### OSP-DQ-004
Lead 생성조건 / Accepted 책임 이전 / 최소 Payload  
**Status: APPROVED**

### OSP-DQ-005
Person / Store Separation  
**Status: APPROVED**

### OSP-DQ-006
Product / Offer / Pricing / Commercial Policy Ownership  
**Status: APPROVED**

---

## WORKING

### Attribution / KPI
- Raw Touch History 보존
- Contract Amount / Recognized Revenue 분리
- Spend Missing ≠ 0
- Real Contract와 Ad Platform Conversion 분리

세부 공식 Attribution Model / Window / KPI 산식은 Working 유지.

### Nurture / Messaging
OSP의 Audience / Trigger / Context와
Shared Notification Infrastructure 간 책임분리는 Working.

### AI Recommendation / Execution
Observe → Detect → Explain → Recommend는 Working Direction.

실제 외부 영향 자동 실행은 별도 승인 전 PENDING.

---

## PENDING — Shared Architecture

다음 3건은 유지한다.

1. Person Master 물리 위치
2. Merchant Account 최종 구조
3. Shared IAM 물리 Architecture

---

## PENDING — Physical Integration

- OSP → OC Physical Handoff API
- OC → OSP Contract / Revenue Outcome Interface
- Advertising Spend Source / API
- Runtime DB / Schema Reconciliation
- Production Storage Security State
