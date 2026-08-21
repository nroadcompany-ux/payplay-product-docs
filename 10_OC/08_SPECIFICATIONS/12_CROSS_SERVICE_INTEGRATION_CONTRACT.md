# OC Cross-Service Integration Contract — OSP / Business OS ↔ OC v0.1

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/08_SPECIFICATIONS/12_CROSS_SERVICE_INTEGRATION_CONTRACT.md` |
| Document ID | `PP-OC-SPEC-XSRV-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Logical Cross-Service Contract. Physical API protocol, IAM, Merchant Account, Person Master, Device/Asset ownership are not finalized. |

> **Phase Verdict:** PASS WITH EXTERNAL / INFRA PENDINGS — CROSS-SERVICE LOGICAL CONTRACT COMPLETE

## 1. Purpose

PayPlay OSP / Business OS와 OC 사이의 Source Ownership, Handoff, Projection, Error / Retry / Reconciliation, Idempotency, Permission, Pending Impact를 Logical Contract 수준으로 정규화한다.

기존 Owner Decision을 변경하지 않으며 다음 Physical 구조는 확정하지 않는다.

- Person Master 물리 위치
- Merchant Account 최종 구조
- Shared IAM 물리 Architecture
- Device / Asset Owner

Development Ready / QA Ready를 선언하지 않는다.

## 2. Cross-Service Backbone

```text
OSP
Traffic / Content / Offer / Conversion
→ Lead / Request
→ OC Opportunity / Sales / Quote / Contract
→ Contract / Fulfillment / Installation Outcome
→ OSP Attribution / Conversion Outcome Projection

OC
Product / Commercial Policy
→ Approved Offer / Price / Promotion Projection
→ OSP

OC
Contract / Product / Policy Applied Result
→ Business OS Store Operational Projection

Business OS
Self-Service Request / Support Request
→ OC Case / Work
→ OC Resolution / Status Projection
→ Business OS
```

## 3. Source Ownership

| Object / Meaning | Source Owner | Consumer | Guard |
|---|---|---|---|
| Traffic / Campaign / Landing / Acquisition Context | OSP | OC Attribution Reference | OC가 OSP acquisition source를 재작성하지 않음 |
| Lead Capture / Consent Evidence | OSP | OC | OC Opportunity 생성 Trigger |
| Opportunity / Sales Execution State | OC | OSP outcome consumer | OSP가 Sales State 직접 수정 금지 |
| Quote / Contract / Fulfillment / Case | OC | OSP / Business OS Projection | Consumer direct write 금지 |
| Product / Commercial Policy Master | OC | OSP / Business OS | Approved + Effective Projection만 소비 |
| Store-facing Operational Surface | Business OS | Store user | OC Source State를 복제 Master로 만들지 않음 |
| Self-service Support Request Entry | Business OS | OC | OC Case 생성 Trigger, Case State Owner는 OC |

## 4. OSP → OC Lead Handoff

### Minimum Logical Payload Candidate

- `lead_ref`
- acquisition source / campaign / landing context reference
- request type / interested offer reference
- supplied contact context or contact reference
- consent / evidence reference where applicable
- preferred contact context
- `created_at`
- `correlation_id`
- `idempotency_key`

### Intake

```text
Lead Received
→ Validate Payload
→ Identity Candidate Match
→ Customer Account / Store Context Resolve or Review
→ Opportunity Create or Existing Opportunity Link
→ Assignment / Sales Execution
```

### Guards

- 동일 Lead 재전송 시 Opportunity 중복 생성 금지.
- 기존 가맹점 추가구매는 신규 Customer Account를 자동 생성하지 않는다.
- Person Master 물리 위치가 Pending이므로 contact/person은 logical reference 또는 supplied context로만 처리한다.
- OSP는 Opportunity 이후 Sales State를 소유하지 않는다.

## 5. OC → OSP Approved Offer / Price / Promotion Projection

Candidate:

- `offer_ref`
- product/service reference
- customer-facing title / description
- price / recurring price / install fee candidate
- promotion / benefit representation
- channel / audience context candidate
- effective period
- source policy version reference
- projection version

Guards:

- Draft / WIP / Formula Error / Approval Missing Policy는 Projection 금지.
- OSP가 가격/프로모션 Source를 직접 수정하지 않는다.
- 과거 Quote / Contract Snapshot은 정책변경으로 재작성하지 않는다.

## 6. OSP Quote / Application Boundary

- OSP = 가맹점-facing 요청 / 신청 / 관심 / 기본선택 생성.
- OC = 내부 Quote Revision / Cost / Margin / Exception / Approval / Contract 실행.
- OSP 요청은 Quote 후보 Trigger일 수 있으나 OC 내부 Guard를 우회하지 않는다.
- OSP에 Restricted Cost / Margin / Commission을 Projection하지 않는다.

## 7. OC → OSP Sales Outcome / Attribution Projection

Candidate:

- lead_ref
- opportunity_ref
- outcome type candidate
- contract outcome reference where permitted
- outcome occurred_at
- source version

Candidate outcome examples:
`contacted / qualified / quoted / contracted / lost / hold`

Guards:

- Attribution을 위해 OC Restricted 정보 전체를 보내지 않는다.
- Revenue/financial detail은 필요성과 권한 확정 전 최소화한다.
- OSP outcome projection은 OC Source State를 수정할 수 없다.

## 8. OC → Business OS Store Operational Projection

Candidate:

- customer account reference
- selected store reference
- active contract summary
- applied product/service summary
- applied user-visible policy/benefit summary
- installation / activation status
- open service/case status summary
- expiry / renewal attention candidate
- source version / updated_at

Guards:

- Business OS가 Contract/Product/Policy의 두 번째 Master가 되지 않는다.
- Store 전환 시 다른 Store Context를 혼합하지 않는다.
- internal cost/margin/compensation은 제외한다.

## 9. Business OS → OC Self-Service Request

Minimum logical payload candidate:

- request_ref
- authenticated access context reference
- selected store reference
- request type
- category / product reference candidate
- summary / description
- attachment/evidence reference candidate
- preferred contact context
- created_at
- correlation_id
- idempotency_key

```text
Business OS Request
→ Store Context Verify
→ Permission / Scope Verify
→ Existing Case Duplicate Check
→ OC Case Create or Link
→ Triage / Assign / Work
→ Resolution
→ Result Projection back to Business OS
```

Guards:

- Merchant Account 최종 구조를 전제로 하지 않는다.
- `authenticated_store_access_context`는 Logical Context이며 physical merchant/user/membership table을 의미하지 않는다.
- Business OS request가 OC Case State를 직접 지정/변경하지 않는다.

## 10. OC → Business OS Case / Service Result Projection

Candidate:

- request_ref / case_ref
- user-visible current status
- next action / waiting-on candidate
- appointment / schedule summary where appropriate
- resolution summary
- completed_at / updated_at
- source version

Internal-only triage note, cost, restricted vendor/employee data는 기본 Projection에서 제외한다.

## 11. Customer Account / Store Context Preservation

Cross-service context candidate:

- `customer_account_ref`
- `selected_store_ref`
- source lead / request ref
- legal entity assignment ref when party context is necessary
- actor/access context ref

Guards:

- Customer Account ≠ Legal/Tax/PG/Settlement Party.
- Store ≠ Legal Entity.
- 동일 Customer Account 내 다수 Store 간 Context가 섞이지 않아야 한다.

## 12. Merchant Account / Shared IAM Abstraction

### Merchant Account

최종 구조가 Pending이므로 독립 `merchant_account_id`를 canonical required key로 확정하지 않는다.

### Shared IAM

Physical user/session/membership을 확정하지 않고 logical requirement만 둔다.

- authenticated actor/access context
- selected store scope
- authorization result/context reference
- expiry/revocation behavior
- audit actor reference

## 13. Device / Asset Pending Guard

Device / Asset reference는 설치·AS·Business OS Surface에서 사용할 수 있다.

그러나 이번 Contract에서 Owner Service / Repository / Physical Table은 확정하지 않는다.

## 14. Request / Message Envelope Candidate

```text
message_id / request_id
event_or_command_type
schema_version
occurred_at
producer_service
consumer_service
source_entity_type
source_entity_ref
source_version
correlation_id
causation_id
idempotency_key
customer_account_ref?
selected_store_ref?
actor_or_access_context_ref?
payload
```

## 15. Idempotency

멱등성 필수 후보:

- OSP Lead → OC Opportunity
- OSP Application → OC Intake
- Business OS Support Request → OC Case
- OC Outcome Projection delivery
- provider/webhook callback relay

동일 idempotency key 재처리 시 신규 Source Transaction을 중복 생성하지 않는다.

## 16. Error Contract Candidate

- `VALIDATION_ERROR`
- `AUTHENTICATION_REQUIRED`
- `AUTHORIZATION_DENIED`
- `STORE_CONTEXT_REQUIRED`
- `SOURCE_NOT_FOUND`
- `SOURCE_NOT_READY`
- `VERSION_CONFLICT`
- `DUPLICATE_REQUEST`
- `DEPENDENCY_UNAVAILABLE`
- `CONTRACT_VERSION_UNSUPPORTED`
- `RECONCILIATION_REQUIRED`

정확한 HTTP status / protocol은 Physical Integration 단계에서 확정한다.

## 17. Retry Candidate

Retryable:
- timeout / transient network
- dependency unavailable
- 5xx candidate
- projection delivery failure
- version conflict after re-read candidate

Non-retryable until correction:
- invalid payload
- authorization denied
- store context mismatch
- unsupported schema version
- invalid business transition

Retry count / backoff은 Pending.

## 18. Reconciliation Candidate

Candidate fields:

- producer / consumer
- source ref / consumer ref
- expected version / observed version
- mismatch type
- correlation id
- retry history
- detected_at
- owner/team
- resolution / resolved_at

Examples:

- OSP Lead sent but OC Opportunity missing
- OC Contract outcome exists but OSP attribution stale
- Business OS request sent but OC Case missing
- OC Case resolved but Business OS status stale

## 19. Versioning / Backward Compatibility

- message / payload에 schema version을 둔다.
- breaking version을 조용히 수용하지 않는다.
- optional field addition과 semantic breaking change를 구분한다.
- source version을 전달한다.

Compatibility window / deployment policy는 Pending.

## 20. Permission / Security

- Producer 전달권한과 Consumer 접근권한을 분리한다.
- Business OS 사용자는 허용된 Store Context만 요청 가능.
- OSP public/anonymous entry는 consent/evidence policy를 따른다.
- Restricted Cost/Margin/Finance/HR/Executive Field는 기본 payload에서 제외.
- Search / AI / Chat가 Cross-Service authorization을 우회하지 않는다.
- Secret / Credential을 payload에 직접 포함하지 않는다.

## 21. AI Guard

AI는 Cross-Service Contract를 우회하는 integration path를 갖지 않는다.

`Authorized Retrieve → Suggest / Prepare → Human Confirm when required → Authorized Service Command → Audit`

AI가 OSP Lead를 임의로 Contract 처리하거나 Business OS request를 직접 Closed 처리하거나 타 Service DB를 직접 수정하지 않는다.

## 22. Test Scenario Candidates

- 동일 OSP Lead 중복 전송 → Opportunity 1건
- Draft/WIP Policy OSP 노출 차단
- OSP 내부 Margin 조회 → 비노출
- Existing Customer 추가요청 → Customer 중복 생성 금지
- BOS Store A에서 Store B 요청 생성 → 거부
- Merchant Account physical 구조 없이 Store Context 계약 동작
- BOS request 중복 submit → Case 중복 방지
- OC Case Resolved / BOS delivery failure → Reconciliation
- stale source version → conflict/re-read
- unsupported schema version → explicit failure
- Contract outcome → OSP attribution projection
- BOS가 OC Contract State direct write → 거부
- Device/Asset Owner 자동추론 금지
- AI Cross-Service direct DB write → 거부

## 23. Pending Impact

### Structural Pending

- Person Master 물리 위치
- Merchant Account 최종 구조
- Shared IAM 물리 Architecture
- Device / Asset Owner

### Cross-Service Policy / Infra Pending

- exact auth token/session transport
- exact API protocol / endpoint / queue technology
- schema compatibility window
- retry count / backoff
- OSP outcome/revenue projection 세부범위
- Business OS user-visible Case status taxonomy
- e-sign / message / carrier / remote support / payment provider
- Legal Entity role-period context가 필수인 contract 상세 rule

## 24. Traceability

```text
OSP Traffic / Offer / Lead
→ OC-FLOW-001
→ Opportunity / Quote / Contract
→ Fulfillment Outcome
→ OSP Attribution Projection

OC Product / Commercial Policy
→ Approved Projection
→ OSP Offer Surface

Business OS Self-Service
→ OC-FLOW-005
→ Case / Work / Resolution
→ Business OS Result Projection
```

## 25. PM Judgment

**PASS WITH EXTERNAL / INFRA PENDINGS — CROSS-SERVICE LOGICAL CONTRACT COMPLETE**

기존 `INTERFACE DRAFT ONLY` 상태였던 OSP / Business OS ↔ OC 경계를 Logical Contract 수준까지 정규화했다.

Physical 구현, Development Ready, QA Ready는 아직 승인하지 않는다.
