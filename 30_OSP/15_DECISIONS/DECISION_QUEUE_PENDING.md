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

## PENDING — KPI Decision Queue

Source: `PP-OSP-SPEC-SALES-FUNNEL-001`
(`30_OSP/17_SPECIFICATION/SALES_FUNNEL_ATTRIBUTION_CONVERSION_ADMIN_SPEC.md`)

전 항목 **PENDING** 유지. Main PM 승인 전 Decision으로 승격하지 않는다.

| ID | 내용 | Status |
|---|---|---|
| KPI-DQ-01 | 공식 KPI Set | PENDING |
| KPI-DQ-02 | 공식 산식 | PENDING |
| KPI-DQ-03 | Attribution Model | PENDING |
| KPI-DQ-04 | Attribution Window | PENDING |
| KPI-DQ-05 | Spend Source / Import Authority | PENDING |
| KPI-DQ-06 | Contract Amount와 Recognized Revenue 사용 기준 | PENDING |
| KPI-DQ-07 | Cancel / Void / Reversal 반영 기준 | PENDING |
| KPI-DQ-08 | New Customer / Existing Customer / Add-on 분모 분리 기준 | PENDING |

### Guardrail (Source Specification 5항 기준)
- Advertising Platform Conversion을 PayPlay 실제 Contract로 간주하지 않는다.
- Spend Missing을 `0`으로 자동 변환하지 않는다.
- Contract Amount와 Recognized Revenue를 동일 값으로 간주하지 않는다.
- Cancellation / Void / Reversal History를 삭제하지 않는다.

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
