# PayPlay Business OS ↔ PayPlay OC Integration

| 항목 | 내용 |
|---|---|
| File Path | `20_BUSINESS_OS/15_OC_INTEGRATION.md` |
| Document ID | `PP-BOS-OC-INT-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Logical Handoff 기준. Physical API Contract 확정 금지 |

Business OS: 사용자 Entry, 상태 View, Self Service, 최소 Context Handoff.
OC: 계약·설치·AS·재고·Service Request/Case·Product/Commercial Policy·내부 Workflow.

Handoff: `Business OS Request → Context → OC → 상태 → Business OS`.

PENDING: Payload, Store/Person/Request 식별, 상태 동기화, Retry, Physical API, Merchant Account, Shared IAM.
