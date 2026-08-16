# Detailed Requirements & Business Policies

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/12_REQUIREMENTS_POLICIES/detailed-requirements-and-business-policies.md` |
| Document ID | `PP-OSP-REQ-POLICY-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Requirement / Policy Working Baseline |

---

## Core Policies

### BP-01
OSP는 Online Sales Platform으로서
온라인 유입·판매경험·Lead·Attribution·Decision Support를 담당한다.

### BP-02
Product / Commercial Policy Master는 현재 PayPlay OC가 소유한다.

### BP-03
OSP는 승인된 Offer만 외부에 표현한다.

### BP-04
Official Lead는 Validation + Required Consent 이후 생성한다.

### BP-05
OSP → OC 책임 이전은 Received가 아니라 Accepted 시점이다.

### BP-06
Retry / Reconciliation 과정에서 동일 Lead가 중복 생성되면 안 된다.

### BP-07
Person / Store / Legal Entity를 임의 자동병합하지 않는다.

### BP-08
OC의 Consultation / Quote / Contract Ledger를
OSP가 이중 원장으로 복제하지 않는다.

### BP-09
Contract Amount와 Recognized Revenue를 분리한다.

### BP-10
Spend Missing을 0으로 처리하지 않는다.

### BP-11
민감 Document는 Public-read를 허용하지 않으며
최소권한 / Signed Access를 적용한다.

### BP-12
주요 변경은 기존 기능 Regression / Side Effect 검증을 통과해야 한다.

---

## Additional Requirements

- E2E Correlation ID
- Consent Version Trace
- Handoff Failure Persistence
- Admin Reconciliation
- Role / Permission Guard
- Audit History
- Source / Campaign / Touch Trace
- Outcome Reversal
- No plaintext secrets
- Shared Infrastructure reuse
