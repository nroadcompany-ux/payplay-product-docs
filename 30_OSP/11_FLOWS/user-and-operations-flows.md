# User & Operations Flows

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/11_FLOWS/user-and-operations-flows.md` |
| Document ID | `PP-OSP-FLOW-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | UX / Operations Flow Working Baseline |

---

## 1. Customer Flow

```text
Search / Ad / Content / Referral
→ PayPlay Website
→ Product / Service Discovery
→ Approved Offer / Compare / Recommendation
→ Consultation / Quote / Application
→ Validation
→ Required Consent
→ Official Lead Created
→ OSP → OC Handoff
→ Submission / Status Projection
```

---

## 2. OSP Operator Flow

```text
Campaign / Content 확인
→ Traffic / Lead 확인
→ Handoff 상태 확인
→ OC Outcome 수신
→ Funnel / Attribution 확인
→ Marketing Decision
→ 다음 Landing / Campaign / Content 실행
```

---

## 3. PayPlay OC Flow After Accepted

```text
Accepted Lead
→ Assignment
→ Consultation
→ Sales Activity
→ Official Quote
→ Contract
→ Installation / downstream operation
```

OSP는 위 OC 내부 업무 Flow를 자신의 Master Ledger로 복제하지 않는다.

---

## 4. Failure Flow

### Handoff Failure
Submitted → Failed → Retry → Reconciliation

### Outcome Delay
Accepted → Outcome Pending → Updated Outcome

### Data Missing
Spend / Outcome / Tracking 데이터가 없으면 0으로 간주하지 않고
Unknown / Not Connected / Delayed / Partial 상태를 사용한다.
