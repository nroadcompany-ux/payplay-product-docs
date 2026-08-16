# PayPlay OSP — Sales Funnel / Attribution / Conversion / Admin Specification

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/17_SPECIFICATION/SALES_FUNNEL_ATTRIBUTION_CONVERSION_ADMIN_SPEC.md` |
| Document ID | `PP-OSP-SPEC-SALES-FUNNEL-001` |
| Product / Service | PayPlay OSP |
| Document Type | Sales Funnel / Attribution / Conversion / Admin Specification |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Logical Funnel·State·Trace·Admin 설계 기준으로 사용 가능 / Attribution 공식 산식·Window·Physical API·DB·IAM 구현 확정 기준으로 사용 금지 |

---

## 1. Purpose

본 문서는 PayPlay OSP의 온라인 영업 Funnel을 Traffic부터 Discovery, Conversion, Lead, PayPlay OC Handoff, OC Outcome Feedback, Attribution, Analytics, Marketing Decision까지 하나의 Logical Specification으로 정리한다.

본 Phase에서는 다음을 임의 확정하지 않는다.

- Attribution 공식 산식
- Attribution Window
- KPI 공식 기준
- Offer 독립 Entity
- Nurture / Messaging 공식 정책
- AI Recommendation / Execution 정책
- Physical API / DB / IAM

**Product / Commercial Policy Master Owner = PayPlay OC** 기준을 유지한다.

---

## 2. Sales Funnel State

```text
Traffic Observed
→ Visit / Session Identified
→ Discovery Started
→ Product / Service Engaged
→ Conversion Intent
→ Form Started
→ Validation Passed
→ Required Consent Captured
→ Official Lead Created
→ Handoff Submitted
→ OC Received / ACK
→ OC Accepted
→ OC Outcome Pending
→ Outcome Updated
→ Attribution / Marketing Decision
```

### State Principle
- Traffic와 Lead는 동일 State가 아니다.
- Form Submit 시도 자체를 Official Lead로 계산하지 않는다.
- Official Lead는 Required Validation과 필요한 Consent가 충족된 이후 생성한다.
- `Received / ACK`는 기술적 수신이다.
- `Accepted`는 PayPlay OC가 업무 책임을 인수한 상태다.
- **Received ≠ Accepted**
- OSP → OC 책임 이전은 `Accepted`에서 발생한다.
- OC Accepted 이후 사람 상담·공식 Quote·Contract 실행 State의 Master는 PayPlay OC이다.

---

## 3. Lead Conversion State Model

1. `Draft Intent`
2. `Form Started`
3. `Validation Failed`
4. `Consent Pending`
5. `Lead Created`
6. `Handoff Pending`
7. `Submitted`
8. `Received`
9. `Accepted`
10. `Rejected`
11. `Transport Failed`
12. `Retrying`
13. `Outcome Pending`
14. `Outcome Updated`
15. `Closed / Reversed`

### State Rules
- `Validation Failed`는 Official Lead Count에 포함하지 않는다.
- Required Consent가 충족되지 않으면 Official Lead를 생성하지 않는다.
- 동일 Lead ID 재전송은 중복 Lead 생성을 발생시키지 않아야 한다.
- `Rejected`와 `Transport Failed`를 구분한다.
- `Outcome Pending`을 Lost로 처리하지 않는다.
- 취소·무효·Reverse 발생 시 History를 삭제하지 않고 Reversal / Updated Outcome으로 남긴다.

---

## 4. Source / Channel / Campaign / Creative / Landing Relationship

```text
Source
└─ Channel
   └─ Campaign
      ├─ Ad
      │  └─ Creative
      └─ Landing
          └─ Session / Touch
              └─ Lead
                  └─ OC Outcome Projection
```

### Trace Candidate
- source
- channel
- campaign_ref
- ad_ref
- creative_ref
- landing_ref
- referrer
- utm_*
- click_id
- session_ref
- captured_at

Raw Touch History를 보존한다. Attribution Model이 변경되더라도 원천 Touch Event를 삭제·덮어쓰지 않는다.

---

## 5. Attribution Candidate Model

**Status: WORKING / PENDING**

Candidate:
- First Touch
- Last Touch
- Assisted / Multi-touch
- Direct / Unknown Handling

```text
Raw Touch / Event History
≠
Attribution Result
```

### Guardrails
- Advertising Platform Conversion을 PayPlay 실제 Contract로 간주하지 않는다.
- Spend Missing을 `0`으로 자동 변환하지 않는다.
- Contract Amount와 Recognized Revenue를 동일 값으로 간주하지 않는다.
- Cancellation / Void / Reversal History를 삭제하지 않는다.

### PENDING
- 공식 Attribution Model
- Attribution Window
- Multi-touch Weight
- Cross-device 처리
- Offline Conversion 처리
- 공식 KPI 산식
- Spend Source
- Revenue Recognition 기준

---

## 6. Website / Landing Conversion Components

### Discovery Components
- Product / Service Card
- Category / Filter
- Detail Page
- Comparison
- Bundle
- Approved Offer Presentation
- Basic Recommendation — WORKING

### Trust / Sales Content Components
- Benefit / Feature
- Pricing Presentation
- Case / Review / Proof
- FAQ
- Guide / Insight
- Campaign Message

### Conversion Components
- CTA
- Consultation Entry
- Quote Request Entry
- Application Entry
- Contact / Inquiry
- Form
- Consent
- Submit
- Submission Complete
- Handoff Status Projection

### Offer Guardrail
OSP는 승인되지 않은 Product / Price / Package / Promotion을 생성하지 않는다.
**Product / Commercial Policy Master Owner = PayPlay OC**
OSP는 승인된 Offer를 Website / Landing / Comparison / Recommendation / Conversion UI에서 표현한다.

---

## 7. Lead Capture Specification

```text
Form / Request
→ Validation
→ Required Consent
→ Official Lead Created
```

### Minimum Logical Data Candidate
- Lead ID
- Lead Type
- Prospect / Person Context
- Contact
- Store Context Reference — optional
- Interest Product / Service
- Source / Channel
- Campaign / Ad / Creative / Landing Reference
- UTM / Click ID
- Consent Snapshot
- Consent Version
- Consent Timestamp
- Request Context
- Quality Signal — optional
- Created At

### Rules
- Support Ticket을 자동으로 Sales Lead로 전환하지 않는다.
- Person / Store / Legal Entity를 자동 병합하지 않는다.
- 재신청은 기존 Intent를 덮어쓰지 않고 새 Intent/Event로 남길 수 있다.
- 동일 Handoff Retry로 동일 OC Lead가 중복 생성되지 않아야 한다.

---

## 8. OSP → PayPlay OC Handoff Detailed Trace

```text
Lead Created
→ Handoff Pending
→ Submitted
→ Received / ACK
→ Accepted
→ OC Assignment
→ OC Consultation
→ OC Quote
→ OC Contract
```

### OSP Responsibility
- Lead 생성
- Payload 준비
- Handoff Submit
- Delivery Trace
- Received / ACK Trace
- Accepted Trace
- Retry / Failure
- Reconciliation
- Correlation

### OC Responsibility
Accepted 이후:
- Assignment
- Consultation
- Sales Activity
- Official Quote
- Contract
- Installation / downstream operation

### Minimum Handoff Candidate
- Lead ID
- Lead Type
- Prospect identity / contact
- Interest Product / Service
- Source / Channel
- Campaign / Ad / Creative / Landing Ref
- UTM / Click ID
- Consent + Version + Timestamp
- Context
- Created At
- Handoff At
- Quality Signal if any
- Attachment Reference if allowed

### Physical Integration
**PENDING**
- Endpoint
- Transport
- Authentication
- Sync / Async
- Retry implementation
- DB Schema
- Event Infrastructure

---

## 9. OC Outcome Feedback Loop

```text
OC Accepted
→ Consultation Outcome
→ Quote Outcome
→ Contract Outcome
→ Contract Amount
→ Recognized Revenue
→ Lost / Cancel / Reverse
→ OSP Outcome Projection
```

### Candidate Feedback Fields
- Lead ID
- Consultation Started / Completed
- Quote Created
- Contract Status
- Contract ID Reference
- Contract Date
- Product / Service Result
- Approved Contract Amount
- Recognized Revenue — if available and approved
- Lost Reason
- Updated At

상담·견적·계약 원장은 PayPlay OC가 소유한다.
OSP는 Attribution / Analytics에 필요한 Outcome Snapshot / Reference만 유지한다.

---

## 10. OSP Admin Operating Flow

```text
Data Health
→ Traffic
→ Lead / Handoff
→ OC Outcome
→ Funnel
→ Attribution
→ Comparison / Drill-down
→ Marketing Decision
→ Next Execution
```

### Admin Candidate Areas
1. Marketing Performance Dashboard
2. Campaign / Channel Performance
3. Landing / Content Operations
4. Product / Offer Presentation
5. Lead / Handoff Monitor
6. Lead Detail / Attribution Trace
7. Funnel / Attribution Analytics
8. Experiment / Learning — WORKING
9. Marketing Decision Center
10. Integration / Reconciliation / Audit

### Data State Rule
- `0`
- `Unknown`
- `Not Connected`
- `Delayed`
- `Partial`
- `N/A`

Missing Data를 0으로 위장하지 않는다.

---

## 11. Analytics / Marketing Decision Support

```text
Spend / Traffic
→ Discovery
→ Conversion
→ Valid Lead
→ OC Accepted
→ Contract / Revenue Outcome
→ Attribution
→ KPI / Funnel Analysis
→ Marketing Decision
→ Next Campaign / Landing / Creative Action
```

### Decision Support Candidate
- Period Comparison
- Channel Comparison
- Campaign Comparison
- Creative Comparison
- Landing Comparison
- Conversion Component Comparison
- Funnel Drop-off
- Lead Quality Signal
- Contract / Revenue Outcome
- Data Quality / Missing Source Warning

AI Recommendation / Execution 정책은 본 Phase에서 확정하지 않는다.

---

## 12. KPI Decision Queue

### Working KPI Candidates
- Impression
- Click
- CTR
- CPC
- Session
- Valid Lead
- Lead Conversion Rate
- CPL
- Accepted Lead
- Accepted Lead Cost
- Contract
- Contract Conversion Rate
- Contract Acquisition Cost
- CAC
- Contract Amount
- Recognized Revenue
- ROAS

### PENDING Decisions
- KPI-DQ-01 공식 KPI Set
- KPI-DQ-02 공식 산식
- KPI-DQ-03 Attribution Model
- KPI-DQ-04 Attribution Window
- KPI-DQ-05 Spend Source / Import Authority
- KPI-DQ-06 Contract Amount와 Recognized Revenue 사용 기준
- KPI-DQ-07 Cancel / Void / Reversal 반영 기준
- KPI-DQ-08 New Customer / Existing Customer / Add-on 분모 분리 기준

본 Decision Queue는 기존 Owner Decision을 변경하지 않으며 Main PM 승인 전 Decision으로 승격하지 않는다.

---

## 13. Explicit Non-Decisions

본 Specification은 다음을 Decision으로 확정하지 않는다.

- Attribution 공식 산식
- Attribution Window
- KPI 공식 기준
- Offer 독립 Entity
- Nurture / Messaging 공식 정책
- AI Recommendation / Execution 정책
- Physical API
- Physical DB
- Shared IAM

---

## 14. Existing Shared Pending

다음 3건은 기존 Pending을 유지한다.

1. Person Master 물리 위치
2. Merchant Account 최종 구조
3. Shared IAM 물리 Architecture

---

## 15. Phase Assessment

- Traffic → Lead Funnel State: WORKING BASELINE
- Lead Conversion State Model: WORKING BASELINE
- Source / Campaign Relationship: WORKING
- Attribution Candidate Model: WORKING / PENDING
- Conversion Components: WORKING
- Lead Capture Logical Specification: WORKING
- OSP → OC Logical Handoff Trace: APPROVED Decision 반영
- OC Outcome Feedback Loop: WORKING
- OSP Admin Operating Flow: WORKING
- KPI Official Standard: PENDING
- Physical API / DB / IAM: PENDING

### Gate
- Phase Specification: **PASS WITH NOTES**
- Development Ready: **NO**
- QA Ready: **NO**

---

## 16. Next Specification

```text
Sales Funnel Screen / Event / Data Traceability Matrix
→ Conversion Component Acceptance Criteria
→ Admin Drill-down / Reconciliation Specification
```
