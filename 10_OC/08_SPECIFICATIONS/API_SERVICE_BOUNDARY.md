# API / Service Boundary + Authorization Contract

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/08_SPECIFICATIONS/API_SERVICE_BOUNDARY.md` |
| Document ID | PP-OC-SPEC-API-001 |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Screen/Entity/State/Permission을 Logical Service/API 구조에 연결. REST/RPC/Physical Backend 확정문서 아님. |

## Principle
- 각 Core Entity는 하나의 Primary Service Owner를 가진다.
- Screen/Queue/AI가 Table을 직접 수정하지 않는다.
- 모든 Write는 Authorization + Business Guard + State Guard + Audit을 통과한다.
- Query / Command / Event 의미를 분리한다.
- 외부 Provider 실패가 Source Entity를 잘못된 Success State로 만들지 않는다.

## Logical Service Boundary
Customer, Sales, Contract, Fulfillment, Case, Product&Policy, Inventory&Supply, Approval, Document, Activity&Audit, IAM/Authorization logical dependency, Search/AI Operations.

## Command Pattern
`sendQuote`, `acceptQuote`, `convertQuoteToContract`, `terminateContract`, `scheduleFulfillment`, `verifyInstallation`, `closeCase`, `adjustInventory`, `requestApproval`, `approvePolicyVersion` 등 의미있는 Business Command를 우선한다.

## Write Flow
`Read Current → Authorize → Business Guard → State Guard → Version Guard → Source Update → Activity/Audit → Event/Projection`

## Cross-Domain Rule
- Inventory 배송완료 ≠ Contract 완료
- Approval Approved ≠ Source Commit Success
- AI Confirm ≠ DB Direct Write

## Event Envelope Candidate
`event_id, event_type, version, occurred_at, source_service, source_entity_type/id, correlation_id, causation_id, actor_context/ref, customer_account_ref, store_ref, source_entity_version, payload_schema_version`

## Error Family Candidate
AUTHENTICATION_REQUIRED, FORBIDDEN_ROW_SCOPE, FIELD_RESTRICTED, ACTION_NOT_ALLOWED, APPROVAL_REQUIRED, INVALID_STATE_TRANSITION, PRECONDITION_FAILED, VERSION_CONFLICT, DUPLICATE_REQUEST, EXTERNAL_PROVIDER_PENDING/FAILED, VALIDATION_ERROR.

## Pending
REST/RPC 방식, Shared IAM Physical, Merchant Account Final, Person Master Physical, e-sign/carrier/message/payment provider, Billing/Receivable detail.
