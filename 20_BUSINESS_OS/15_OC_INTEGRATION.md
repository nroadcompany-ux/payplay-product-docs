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


---

## Related Official Logical Contract — Reference

| 항목 | 내용 |
|---|---|
| Document ID | `PP-OC-SPEC-XSRV-001` |
| 문서 | [10_OC/08_SPECIFICATIONS/12_CROSS_SERVICE_INTEGRATION_CONTRACT.md](../10_OC/08_SPECIFICATIONS/12_CROSS_SERVICE_INTEGRATION_CONTRACT.md) |
| Status | WORKING |
| Source of Truth | NO |

Business OS ↔ OC Logical Handoff 구조는 위 Cross-Service Integration Contract에서
Source Ownership / Payload Candidate / Projection / Idempotency / Error / Retry / Reconciliation 관점으로 정규화되어 있다.

> ⚠️ **본 참조는 Reference / Cross-link이며 아래를 의미하지 않는다.**
> - Physical API 확정 근거 아님
> - Business OS 기존 Owner Decision 변경 아님
> - 기존 PENDING 해소 아님
> - 신규 Interface Decision 생성 아님
>
> 상기 문서의 PENDING(Payload, Store/Person/Request 식별, 상태 동기화, Retry, Physical API, Merchant Account, Shared IAM)은 그대로 유지된다.
