# PayPlay OC — Final Pending Register (Developer Package v1.0)

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/09_DECISIONS/FINAL_PENDING_REGISTER.md` |
| Document ID | PP-OC-FINAL-PENDING-REGISTER-001 |
| Version | v1.0 |
| Status | FINAL GATE CANDIDATE / CONSOLIDATED |
| Source of Truth | NO — Final Gate Index. 기존 Pending 기록을 대체하지 않는다. |
| Owner | PayPlay OC |
| Last Reviewed | 2026-08-21 |
| Development Use | 개발 착수 범위와 Pending-dependent 범위를 분리하는 Gate 기준. Pending 값을 임의 확정하지 않는다. |
| Notion Source | https://app.notion.com/p/3c353327fb868171acdcf25a6424f3d8 |
| Related Document | [PENDING_REGISTER.md](./PENDING_REGISTER.md) (PP-OC-PENDING-001 — 기존 Pending 원장, 본 문서가 대체하지 않음) |

> 📌 PayPlay OC Developer Package Final Gate 직전 통합 Pending Register. 기존 Decision Queue와 각 Specification의 Pending을 삭제하지 않고, 최신 Owner Direction과 GPT↔Claude Cross-Audit 기준으로 중복 제거·재분류한다. 이 문서는 과거 Pending 기록을 덮어쓰지 않으며 현재 구현 영향도를 판정하는 Final Gate용 Index다.

---

## 1. Final Classification Rule

- **Scope-Blocking:** 해결 전 Developer Package 전체 또는 주요 OC Core Flow 착수를 막는 항목.
- **Implementation-Dependent:** 논리 설계와 unaffected scope 개발은 가능하나 해당 기능의 Production 구현·Physical Binding·정확 동작 확정 전에 해결해야 하는 항목.
- **Non-Blocking Normalization:** 현재 기능 개발 착수를 막지 않으며 ID/Route/UX/운영값/후속 정규화 단계에서 확정 가능한 항목.
- Owner가 방향을 이미 확정한 항목은 다시 `Decision Required`로 되돌리지 않는다.

---

## 2. Scope-Blocking

**Package-wide Scope-Blocking Pending: 0**

현재 Developer Package 전체 또는 Major OC Flow 개발 착수를 막는 미해결 Owner Decision은 없다.

단, 아래 Implementation-Dependent 항목에 직접 의존하는 세부 범위는 해당 항목 확정 전 Production Finalization을 금지한다.

---

## 3. Implementation-Dependent PENDINGS

### I-01 Shared Person Physical Implementation

- 방향: **Shared Person Master** 확정.
- Pending: Physical DB / Repository / Schema / API binding.
- 영향: Person identity를 물리 Table로 고정하는 범위.

### I-02 Shared Merchant / Store ↔ Merchant Account Physical Implementation

- 방향: **Shared Merchant Master + Store ↔ Merchant Account 분리** 확정.
- Pending: Physical Entity / Repository / synchronization contract.
- 영향: Merchant/Store 물리 모델과 cross-service write boundary.

### I-03 Shared IAM Physical Architecture

- 방향: **Shared IAM** 확정.
- Pending: Auth/session/membership/schema/provider/RLS exact implementation.
- 영향: Production permission enforcement, external worker access, admin binding.

### I-04 Shared Device / Asset Physical Implementation

- 방향: **Shared Device/Asset Master** 확정.
- Pending: Physical owner/schema/repository/API relationship.
- 영향: Serial/Device/Asset production binding.

### I-05 Finance / Billing / Receivable Detail

- Owner 방향 및 주요 Settlement State는 확정.
- Pending: Billing/Receivable 상세 Entity/State, accounting/ledger boundary, payment/bank execution contract.
- 영향: Core finance calculation/posting engine production finalization.

### I-06 Compensation Exact Policy Values

- Owner 방향: 계약 + 설치 + 회사 입금 완료 후 Eligibility, 기본 영업팀장 검토→대표 최종승인, 항목별 팀장 단독승인 선택 가능, 취소/환불/미수/해지 환수·익월 차감, 상한 없음.
- Pending: 상품/직군별 계산식·비율 및 항목별 approval configuration.
- 영향: 실제 Compensation calculation engine.

### I-07 External Provider Contracts

- e-sign / Kakao·SMS·Fax / Carrier / Remote Support / VAN·PG·Bank / Sales Data Provider 등 exact Provider·Endpoint·Callback contract.
- 영향: Provider-dependent production integration만 제한. 내부 logical interface 개발은 가능.

### I-08 Inventory vs Procurement / Supply Physical Split

- Logical 업무영역은 `Inventory & Supply`로 사용 가능.
- Pending: Physical service/table owner split.
- 영향: repository/service decomposition finalization.

### I-09 Company Resource Secret / Vault Architecture

- 방향: Resource Metadata와 Secret 분리, Secret 원문 Search/AI Index 금지 확정.
- Pending: Vault/Secret Store provider, secret-reference schema, re-auth integration.
- 영향: Password/API Key/Token/Recovery Code production handling.

### I-10 HR External / Identity / Retention Details

- People/HR 및 Former Employee Service Desk 포함은 확정.
- Pending: 본인확인 방식, exact HR document template/legal requirement, retention/destruction, physical Person/IAM relation.
- 영향: 퇴사자 서비스와 민감 HR production release.

### I-11 Request / Cross-Service Physical Contract

- Multi-Entry / Single OC Intake logical contract는 확정.
- Pending: Request Type physical enum/API, source-specific status taxonomy, callback/retry/idempotency/reconciliation exact contract.
- 영향: OSP/BOS/Kakao/External Form/Partner production handoff.

### I-12 Legacy WDI Migration Scope

- 기능 Architecture 통합과 데이터 Migration은 분리.
- Pending: `DQ-OC-WDI-001` 실제 데이터 선별 이관/참조 범위.
- 영향: Migration phase만 제한. Target logical development는 가능.

---

## 4. Non-Blocking Normalization PENDINGS

### N-01 Official Screen ID / Route Normalization

Vehicle / Parking / Schedule / Unified Intake / Company Resource Directory 신규 Family의 Official Screen ID와 exact route.

### N-02 Final Independent Screen Count / UX Composition

List / Detail / Tab / Drawer / Modal / Embedded / Projection 최종 조합. `52 + 5 = 57`로 단순 확정 금지.

### N-03 Admin / Permission Navigation Placement

`OC-ADMIN-001`의 exact sidebar/entry placement 및 운영 UX.

### N-04 Exact Permission Matrix / Field Visibility

공통 `Role + Org/Team + Row Scope + Field Visibility + Action + Approval + Audit` 원칙은 확정. 기능별 exact matrix와 Company Resource Account Identifier visibility/re-auth 세부는 후속 정규화.

### N-05 Schedule / Parking / Vehicle Operational Values

Schedule visibility/conflict/double-booking, Parking role/provider/cost 세부, Vehicle finance posting/detail linkage 등 exact 값.

### N-06 SLA / Retry / Backoff / Priority Exact Values

Request/Case/Provider별 exact SLA, retry count, backoff, priority default 및 escalation timing.

### N-07 Project Native OC Reconsideration

현재 `Notion Integration First`; Native OC Project Management는 후속 검토. 현재 Developer Package의 차단요소 아님.

---

## 5. Historical Decision Queue Reclassification Guard

- `DQ-OC-CAP-001`의 과거 `OC Customer/Store Master` 제안은 최신 **Shared Merchant Master + Store ↔ Merchant Account 분리** 방향보다 우선하지 않는다. 운영 의미는 보존하되 Physical 구조는 I-02로 관리한다.
- `DQ-OC-CAP-003`은 보안 원칙 자체는 이미 확정 수준이며 exact role/row/field matrix만 I-03/N-04로 유지한다.
- `DQ-OC-CAP-004`는 Eligibility/승인/환수 방향이 Owner Input으로 상당 부분 해소되었고 exact 계산식만 I-06으로 유지한다.
- `DQ-OC-CAP-005`는 Provider 선택 Pending만 I-07로 유지한다.
- `DQ-OC-CAP-002`는 logical split 결정이 아니라 Physical decomposition Pending으로 I-08에 통합한다.
- 과거 Queue/Proposal 문서는 History로 유지하며 삭제하거나 소급 수정하지 않는다.

---

## 6. Cross-Audit Status

Claude Independent Cross-Audit 후 MINOR-01 Customer Messaging Trace 안내와 MINOR-02 Company Resource Account Identifier Visibility를 보정했다.

- GPT ↔ Claude unresolved difference: **0**
- Structural Conflict: **0**
- Document-to-Document Conflict: **0**
- Missing Capability / Flow / Rule: **0**
- Duplicate Source-of-Truth: **0**
- Legacy Unmapped / Loss Risk: **0**
- Development Blocker: **0**

---

## 7. Final Gate Interpretation

- Developer Readable: **YES**
- Development Startable: **YES**
- Major OC Flow Implementable: **YES**
- Pending-dependent Production Finalization: **NO — 해당 항목 해소 전**
- QA Ready: **NOT YET**
- New Owner Decision Required for Developer Package Finalization: **NONE**

**Register Verdict: PASS — NO PACKAGE-WIDE SCOPE-BLOCKING PENDING; IMPLEMENTATION-DEPENDENT AND NON-BLOCKING PENDINGS ARE EXPLICITLY ISOLATED.**

---

## 8. Pending Guard Trace — GitHub 연결

Developer Package 문서에서 본 Register를 추적할 수 있도록 다음 문서가 상호 연결되어 있다.

| 문서 | GitHub Path | 연결 |
|---|---|---|
| Document #1 Service Architecture / Menu & Depth | `10_OC/07_ARCHITECTURE/SERVICE_ARCHITECTURE_MENU_DEPTH.md` | Related Pending |
| Document #4 Screen & Navigation / Traceability | `10_OC/08_SPECIFICATIONS/SCREEN_NAVIGATION_TRACEABILITY.md` | Related Pending |
| Developer Package Guide | `10_OC/DEVELOPER_PACKAGE_GUIDE.md` | Final Pending Register |
| 기존 OC Pending 원장 | `10_OC/09_DECISIONS/PENDING_REGISTER.md` | 병존 — 대체하지 않음 |

---

## Intake Note — 2026-08-21

- 본 문서는 Notion Final Pending Register를 GitHub에 신규 입고한 것이다.
- 기존 `PENDING_REGISTER.md` (`PP-OC-PENDING-001`)는 삭제·덮어쓰기하지 않았다. 본 문서 원문이 스스로 "과거 Pending 기록을 덮어쓰지 않는 Final Gate용 Index"임을 선언하므로 두 문서는 병존한다.
- Pending 값은 임의 확정하지 않았다.
