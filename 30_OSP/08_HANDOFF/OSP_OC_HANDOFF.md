# OSP → PayPlay OC Handoff

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/08_HANDOFF/OSP_OC_HANDOFF.md` |
| Document ID | `PP-OSP-OC-HANDOFF-001` |
| Status | APPROVED |
| Source of Truth | YES |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Logical Responsibility Boundary 기준으로 사용 가능 / Physical API는 PENDING |

---

## 1. Responsibility Flow

```text
Validated Intake
→ Required Consent
→ Official Lead Created
→ Handoff Pending
→ Submitted
→ Received / ACK
→ Accepted
→ PayPlay OC Sales Process
```

---

## 2. Owner Decision

**Received ≠ Accepted**

- Received / ACK = 기술적 수신
- Accepted = PayPlay OC가 Lead 업무 책임을 인수
- OSP → OC 책임 이전 기준 = Accepted

---

## 3. OSP → OC Minimum Payload

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

---

## 4. Transport Requirements

- Idempotency
- Retry
- Failure persistence
- Reconciliation
- Audit / Correlation ID
- Reject와 Technical Failed 구분

---

## 5. OC Responsibility After Accepted

- Assignment
- Consultation
- Sales Activity
- Official Quote
- Contract
- Installation / downstream operation

---

## PENDING

- Physical Endpoint
- Transport Protocol
- Sync / Async Architecture
- OC counterpart implementation
