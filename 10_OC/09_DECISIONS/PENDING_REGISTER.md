# PayPlay OC Pending Register

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/09_DECISIONS/PENDING_REGISTER.md` |
| Document ID | PP-OC-PENDING-001 |
| Status | PENDING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | 미확정 구조·정책의 임의 구현 방지. Pending 해소는 별도 Main PM/Owner Decision 필요. |

## P0 Structural Pending
1. **Person Master 물리 위치** — Logical Relation 사용 가능, Physical DB/Owner 확정 금지.
2. **Merchant Account 최종 구조** — Customer Account/Store/User Identity와 동일 Entity 선확정 금지, 독립 Table 선생성 금지.
3. **Shared IAM 물리 Architecture** — Logical Permission 요구 사용 가능, User/Auth/Session/Membership Physical Schema 확정 금지.

## Additional Pending
Inventory/Supply physical split, Billing/Receivable entity/state/allocation, Settlement detail, Compensation formula/rate/approval, Payment/Bank Provider, e-sign, Quote/Message Provider, Carrier/Logen Adapter, Remote Support/Vendor Integration, HR 본인확인/문서법적요건/Retention/SLA, Official Screen ID, Decision Detail UX, Legacy WDI Migration scope, Credential Key classification, Approval threshold.

## Guard
Pending은 Source Code 편의를 이유로 Decision으로 간주하지 않는다.
