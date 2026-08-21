# PayPlay OC — Final Pending Register (Developer Package v1.0)

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/09_DECISIONS/FINAL_PENDING_REGISTER.md` |
| Document ID | PP-OC-FINAL-PENDING-REGISTER-001 |
| Version | v1.0 |
| Status | FINAL GATE CANDIDATE / CONSOLIDATED |
| Final SOT Freeze | COMPLETE — 2026-08-21 16:54 KST · Human Handoff Ready: YES · Final Fix Verification 6/6 PASS |
| Workforce Service Desk Supplemental | MERGED / VERIFIED |
| Source of Truth | NO — Final Gate Index. 기존 Pending 기록을 대체하지 않는다. |
| Owner | PayPlay OC |
| Last Reviewed | 2026-08-21 |
| Development Use | 개발 착수 범위와 Pending-dependent 범위를 분리하는 Gate 기준. Pending 값을 임의 확정하지 않는다. |
| Resync | 2026-08-21 Final SOT Resync (Main PM GO) |
| Notion Source | https://app.notion.com/p/3c353327fb868171acdcf25a6424f3d8 |
| Related Document | [PENDING_REGISTER.md](./PENDING_REGISTER.md) (PP-OC-PENDING-001 — 기존 Pending 원장, 본 문서가 대체하지 않음) |

<details>
<summary>🔐 Final Gate Evidence / Audit Closeout (최종 판정 Evidence — 과거 기록 아님)</summary>

> 본 Toggle은 Final Gate 최종 판정 Evidence다. 현재 §5 `현재 상태` 및 §7 `Final Gate Interpretation`과 내용이 중복되므로 본문에서 분리해 Evidence로 보존한다. **과거 기록이 아니며 삭제 금지.**

### ✅ FINAL PENDING CONTROL — SOT FROZEN — 2026-08-21 16:54 KST

- Human Handoff Ready: **YES**
- Final SOT Freeze: **COMPLETE**
- Final Fix Verification: **6/6 PASS**
- Package-wide Scope-Blocking Pending: **0**
- Owner Decision Required: **0**
- Remaining Pending: **Physical Binding / External Provider / Legal·Finance Reference / Operational·Business Policy Config only**
- Workforce Service Desk Supplemental: **MERGED / VERIFIED**

> 아래 과거 `Human Handoff Ready = NO`, `Merge Required`, `Verification Pending` 표현은 Historical Status입니다. 현재 Pending 판단은 본 섹션과 최신 A~D 분류를 우선합니다.

---

</details>

## 🔄 Pending Reduction Superseding Update — 2026-08-21

> **이 섹션이 아래의 과거 Pending 분류보다 우선합니다.** 기존 항목은 Audit History로 보존하며 삭제하지 않습니다.

### Current Verdict

- **Package-wide Scope-Blocking Pending:** 0
- **Owner Decision Pending (현재 개발 패키지 구조 확정에 필요한 대표 결정):** 0
- **Logical Contract Conflict:** 0
### A. CLOSED — Logical / Product / Operations Structure

다음 항목은 더 이상 큰 범위의 `Pending`으로 표기하지 않습니다. Logical Owner, Interface, State/Rule 또는 운영 원칙이 확정됐고 Physical Binding만 별도 유지합니다.

- Permission Matrix / Field Visibility 기본 구조 및 A/B/C/E 노출등급
- Screen/Route/UX Logical Composition Candidate
- Request Envelope / Cross-Service Logical Contract
- Vehicle / Parking / Schedule Logical Spec
- S1/P1 SLA 핵심 운영원칙 및 Business Hours Carryover
- Legacy Migration Classification + Data Profiling Rule
- Finance Billing / Receivable Logical Boundary
- Compensation Engine / Approval / Snapshot / Adjustment 구조
- HR Employee/Worker ↔ Person ↔ IAM 경계, Offboarding, Former Worker Service
- Company Resource Metadata ↔ Vault Secret 분리
- Shared Person / Merchant / IAM / Device·Asset의 OC Interface Contract
- Inventory / Procurement·Supply / Shipment Logical Boundary
- External Provider Adapter Logical Contract
- Workforce Service Desk Owner = **PayPlay OC**
- Workforce Service Desk Self-Service / Public Entry / Unified Intake Routing 구조
- 퇴사·해촉 시 내부 IAM Access는 Effective End에 회수, 기본 유예기간 없음
- OC 계정 없는 외부직원·퇴사자·해촉자 본인확인 = **One-time Secure Link**
- Secure Link 기본 발송 = **시스템 자동 발송**, 기존 등록 연락처 사용; 직원 수동처리는 예외 Manual Verification에 한정

### B. Development / Common Infrastructure Binding Pending

다음은 기획 미정이 아니라 **실제 구현 Binding**입니다.

- Shared Person: Physical persistence, canonical ID, merge/dedup engine
- Shared Merchant / Store / Merchant Account: Physical table/service, sync strategy; Logical 1:N 가능성 보존 및 1:1 고정 구현 금지
- Shared IAM: Provider, session, row/field/action authorization physical binding, re-auth, break-glass implementation
- Shared Device / Asset: Physical owner/service, telemetry/device binding
- Inventory vs Procurement/Supply: Physical service/deployment split
- Request / Cross-Service: endpoint, auth/token, exact enum code, retry/backoff implementation
- Schedule: Shared IAM permission binding
- Vault: Vault Provider, re-auth physical implementation
- Compensation: Policy Sheet → OC Policy Version physical linkage
- Legacy Migration: production profiling/execution/row selection
- Finance: Physical ledger, bank/payment integration, accounting schema binding
- Workforce Service Desk: Secure Link token implementation, Identity Match, Signed/Secure Download implementation

### C. External Provider Binding Pending

- 전자서명 Provider / Endpoint / Credential / Callback
- Messaging/SMS/Email Provider 실제 Binding
- Carrier/Shipment Provider 실제 Binding
- VAN/PG Provider Endpoint / Credential / Result/Reconciliation Binding
- Parking 등 실제 외부 Provider를 사용하는 경우 Provider Contract
- Provider 성공 후 Source Domain Guard 실패 시 Source State 변경 금지, `MANUAL_INTERVENTION_REQUIRED` 격리 원칙은 Logical CLOSED

### D. Legal / Finance / Operational Config Values — Non-Architecture Pending

다음은 OC 구조 미정이 아니라 실제 운영·법정·회계 **Config/Reference Value**입니다.

- VAT / 원천세 / 계정과목 / 회계분개 기준
- HR 법정 보관·파기기간 및 공식 문서 법정 요건
- Compensation 실제 공식/비율/고정금액/건당단가 등 Policy Value
- S2~S4 세부 SLA Target 및 업무별 Priority/Retry 값
- Secure Link TTL / Retry Count / Lockout 시간
- Signed Document Download Link TTL

이 값들은 구조를 다시 설계하지 않고 Versioned Policy / Security Config / Finance·Legal Reference로 주입합니다.

### Superseded Pending Note

아래 과거 Register에 남아 있는 `본인확인 방식`, `Person/Merchant/IAM/Device 구조 자체`, `Vehicle/Parking/Schedule 구조 자체`, `Finance/HR/Compensation Logical 구조` 등의 광범위 Pending 표현은 본 Update로 **Superseded** 됩니다. Physical / Provider / Legal·Finance / Config 범위만 Pending으로 해석합니다.

> 🛠️ **Historical Working Note — 추가 처리 가능성 재검토 기록 (현재 Pending 판정 아님)**
> 이 Register의 `Pending(미확정)`은 모두 같은 의미가 아닙니다. 현재 항목을 다시 검토한 결과, 상당수는 **지금 기획·설계 단계에서 더 구체화할 수 있으며**, 일부만 대표/운영정책·공통인프라·외부업체 결정이 있어야 최종 확정됩니다.
> **따라서 이 문서는 '기다리는 목록'이 아니라 '남은 일을 누가 닫아야 하는지 관리하는 목록'으로 사용합니다.**

---

> 👀 **이 문서는 무엇인가요?**
> 이 문서는 개발자·기획자가 **"아직 안 정해진 게 무엇이고, 그게 지금 개발을 막는지 아닌지"** 빠르게 확인하는 체크리스트입니다.
> - **Scope-Blocking (범위 차단):** 해결 전에는 핵심 개발을 시작하면 안 되는 항목
> - **Implementation-Dependent (구현 전 확정 필요):** 다른 개발은 가능하지만 해당 기능을 실제 운영 수준으로 완성하기 전에는 반드시 확정해야 하는 항목
> - **Non-Blocking Normalization (비차단 정규화):** 지금 개발을 막지는 않고 Screen ID(화면 식별자), Route(경로), UX(사용자 경험), 운영값 등을 후속 단계에서 정리해도 되는 항목
>
> **현재 결론:** Package-wide Scope-Blocking Pending (패키지 전체를 막는 미확정 항목)은 **0개**입니다. 따라서 개발은 시작할 수 있습니다. 다만 아래 Implementation-Dependent 항목에 직접 걸리는 기능은 값이 확정되기 전 Production Finalization (실운영 수준 최종 확정)을 하면 안 됩니다.

> 📌 PayPlay OC Developer Package Final Gate 직전 통합 Pending Register. 기존 Decision Queue와 각 Specification의 Pending을 삭제하지 않고, 최신 Owner Direction과 GPT↔Claude Cross-Audit 기준으로 중복 제거·재분류한다. 이 문서는 과거 Pending 기록을 덮어쓰지 않으며 현재 구현 영향도를 판정하는 Final Gate용 Index다.

---

## 1. Final Classification Rule (최종 분류 기준)

- **Scope-Blocking:** 해결 전 Developer Package 전체 또는 주요 OC Core Flow 착수를 막는 항목.
- **Implementation-Dependent:** 논리 설계와 unaffected scope 개발은 가능하나 해당 기능의 Production 구현·Physical Binding·정확 동작 확정 전에 해결해야 하는 항목.
- **Non-Blocking Normalization:** 현재 기능 개발 착수를 막지 않으며 ID/Route/UX/운영값/후속 정규화 단계에서 확정 가능한 항목.
- Owner가 방향을 이미 확정한 항목은 다시 `Decision Required`로 되돌리지 않는다.

---

## 2. Scope-Blocking (개발 범위를 막는 항목)

**Package-wide Scope-Blocking Pending (패키지 전체 개발을 막는 미확정 항목): 0**

현재 Developer Package 전체 또는 Major OC Flow 개발 착수를 막는 미해결 Owner Decision은 없다.

단, 아래 Implementation-Dependent 항목에 직접 의존하는 세부 범위는 해당 항목 확정 전 Production Finalization을 금지한다.

---

## 3. Implementation-Dependent PENDINGS (해당 기능 구현 전에 확정해야 하는 항목)

### I-01 Shared Person Physical Implementation (공통 사람정보 실제 구현)

- 방향: **Shared Person Master** 확정.
- Pending: Physical DB / Repository / Schema / API binding.
- 영향: Person identity를 물리 Table로 고정하는 범위.

### I-02 Shared Merchant / Store ↔ Merchant Account Physical Implementation (공통 가맹점·매장 계정 실제 구현)

- 방향: **Shared Merchant Master + Store ↔ Merchant Account 분리** 확정.
- Pending: Physical Entity / Repository / synchronization contract.
- 영향: Merchant/Store 물리 모델과 cross-service write boundary.

### I-03 Shared IAM Physical Architecture (공통 로그인·권한 체계 실제 구조)

- 방향: **Shared IAM** 확정.
- Pending: Auth/session/membership/schema/provider/RLS exact implementation.
- 영향: Production permission enforcement, external worker access, admin binding.

### I-04 Shared Device / Asset Physical Implementation (공통 장비·자산 실제 구현)

- 방향: **Shared Device/Asset Master** 확정.
- Pending: Physical owner/schema/repository/API relationship.
- 영향: Serial/Device/Asset production binding.

### I-05 Finance / Billing / Receivable Detail (재무·청구·미수금 상세)

- Owner 방향 및 주요 Settlement State는 확정.
- Pending: Billing/Receivable 상세 Entity/State, accounting/ledger boundary, payment/bank execution contract.
- 영향: Core finance calculation/posting engine production finalization.

### I-06 Compensation Exact Policy Values (수당·보상 정확 계산값)

- Owner 방향: 계약 + 설치 + 회사 입금 완료 후 Eligibility, 기본 영업팀장 검토→대표 최종승인, 항목별 팀장 단독승인 선택 가능, 취소/환불/미수/해지 환수·익월 차감, 상한 없음.
- Pending: 상품/직군별 계산식·비율 및 항목별 approval configuration.
- 영향: 실제 Compensation calculation engine.

### I-07 External Provider Contracts (외부 연동업체·시스템 상세 계약)

- e-sign / Kakao·SMS·Fax / Carrier / Remote Support / VAN·PG·Bank / Sales Data Provider 등 exact Provider·Endpoint·Callback contract.
- 영향: Provider-dependent production integration만 제한. 내부 logical interface 개발은 가능.

### I-08 Inventory vs Procurement / Supply Physical Split (재고와 구매·공급 실제 시스템 분리)

- Logical 업무영역은 `Inventory & Supply`로 사용 가능.
- Pending: Physical service/table owner split.
- 영향: repository/service decomposition finalization.

### I-09 Company Resource Secret / Vault Architecture (회사 계정 비밀번호·Secret 보관 구조)

- 방향: Resource Metadata와 Secret 분리, Secret 원문 Search/AI Index 금지 확정.
- Pending: Vault/Secret Store provider, secret-reference schema, re-auth integration.
- 영향: Password/API Key/Token/Recovery Code production handling.

### I-10 HR External / Identity / Retention Details (퇴사자·본인확인·보관기간 상세)

- People/HR 및 Former Employee Service Desk 포함은 확정.
- Logical identity method: **One-time Secure Link — CLOSED** (문서 상단 §A 기준). Pending: **Identity Provider Physical Binding, Secure Link Token Implementation, Signed/Secure Download Physical Implementation**, exact HR document template/legal requirement, retention/destruction, physical Person/IAM relation.
- 영향: 퇴사자 서비스와 민감 HR production release.

### I-11 Request / Cross-Service Physical Contract (가맹점요청·서비스간 실제 연동 규격)

- Multi-Entry / Single OC Intake logical contract는 확정.
- Pending: Request Type physical enum/API, source-specific status taxonomy, callback/retry/idempotency/reconciliation exact contract.
- 영향: OSP/BOS/Kakao/External Form/Partner production handoff.

### I-12 Legacy WDI Migration Scope (기존 WDI 데이터 이관 범위)

- 기능 Architecture 통합과 데이터 Migration은 분리.
- Pending: `DQ-OC-WDI-001` 실제 데이터 선별 이관/참조 범위.
- 영향: Migration phase만 제한. Target logical development는 가능.

---

## 4. Non-Blocking Normalization PENDINGS (현재 개발을 막지 않는 후속 정리 항목)

### N-01 Official Screen ID / Route Normalization (공식 화면 ID·경로 정리)

Vehicle / Parking / Schedule / Unified Intake / Company Resource Directory 신규 Family의 Official Screen ID와 exact route.

### N-02 Final Independent Screen Count / UX Composition (최종 화면 수·화면 구성)

List / Detail / Tab / Drawer / Modal / Embedded / Projection 최종 조합. `52 + 5 = 57`로 단순 확정 금지.

### N-03 Admin / Permission Navigation Placement (관리자·권한 메뉴 위치)

`OC-ADMIN-001`의 exact sidebar/entry placement 및 운영 UX.

### N-04 Exact Permission Matrix / Field Visibility (세부 권한표·항목별 노출범위)

공통 `Role + Org/Team + Row Scope + Field Visibility + Action + Approval + Audit` 원칙은 확정. 기능별 exact matrix와 Company Resource Account Identifier visibility/re-auth 세부는 후속 정규화.

### N-05 Schedule / Parking / Vehicle Operational Values (일정·주차·차량 운영 세부값)

Schedule visibility/conflict/double-booking, Parking role/provider/cost 세부, Vehicle finance posting/detail linkage 등 exact 값.

### N-06 SLA / Retry / Backoff / Priority Exact Values (처리시간·재시도·우선순위 세부값)

Request/Case/Provider별 exact SLA, retry count, backoff, priority default 및 escalation timing.

### N-07 Project Native OC Reconsideration (OC 자체 프로젝트관리 기능 재검토)

현재 `Notion Integration First`; Native OC Project Management는 후속 검토. 현재 Developer Package의 차단요소 아님.

---

## 5. Historical Decision Queue Reclassification Guard (과거 미결정 기록 재해석 주의)

- `DQ-OC-CAP-001`의 과거 `OC Customer/Store Master` 제안은 최신 **Shared Merchant Master + Store ↔ Merchant Account 분리** 방향보다 우선하지 않는다. 운영 의미는 보존하되 Physical 구조는 I-02로 관리한다.
- `DQ-OC-CAP-003`은 보안 원칙 자체는 이미 확정 수준이며 exact role/row/field matrix만 I-03/N-04로 유지한다.
- `DQ-OC-CAP-004`는 Eligibility/승인/환수 방향이 Owner Input으로 상당 부분 해소되었고 exact 계산식만 I-06으로 유지한다.
- `DQ-OC-CAP-005`는 Provider 선택 Pending만 I-07로 유지한다.
- `DQ-OC-CAP-002`는 logical split 결정이 아니라 Physical decomposition Pending으로 I-08에 통합한다.
- 과거 Queue/Proposal 문서는 History로 유지하며 삭제하거나 소급 수정하지 않는다.

---

## 6. Cross-Audit Status (GPT ↔ Claude 교차 검수 상태)

Claude Independent Cross-Audit 후 MINOR-01 Customer Messaging Trace 안내와 MINOR-02 Company Resource Account Identifier Visibility를 보정했다.

- GPT ↔ Claude unresolved difference: **0**
- Structural Conflict: **0**
- Document-to-Document Conflict: **0**
- Missing Capability / Flow / Rule: **0**
- Duplicate Source-of-Truth: **0**
- Legacy Unmapped / Loss Risk: **0**
- Development Blocker: **0**

---

## 7. Final Gate Interpretation (최종 통과 판정 해석)

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

<details>
<summary>📋 Historical Pending Reduction / Audit History (과거 Pending 작업 기록 — 현재 상태 아님)</summary>

> 아래는 Pending Reduction 작업 이전 History다. **현재 Pending 판단은 Toggle 밖의 A~D 분류와 §1~§7만 사용한다.** `Human Handoff Ready = NO`, `MERGED / FINAL FIX VERIFICATION PENDING` 등 과거 표현은 현재 상태가 아니며, WSD Merge Status는 **MERGED / VERIFIED**로 확정됐다. 내용은 삭제하지 않고 Evidence로 보존한다.

#### Current Verdict — Historical `Human Handoff Ready` 표기

- **Human Handoff Ready:** NO — #1~#4 / Main Handoff / Single Page 병합과 GPT↔Claude Cross-Audit는 완료. 현재 **Final Fix Verification 후 최종 YES/NO 판정 대기**

#### E. Workforce Service Desk Supplemental Additions — MERGED / FINAL FIX VERIFICATION PENDING *(Historical 제목 표기)*

아래 Supplemental은 #1~#4 원본에 병합 완료되었습니다. 기존 ID는 renumber하지 않았으며, 현재 Final Fix Verification만 남았습니다.

- Flow: `WSD-C-01` 내부직원 Self-Service 조회
- Flow: `WSD-C-02` 외부·퇴사자 Public Entry + Request
- Flow: `WSD-O-01` 담당자 처리
- Screen Family Candidate: `OC-WSD-*` Operator View
- Screen Family Candidate: `OC-WSD-PUBLIC-*` Public Entry Surface
- Unified Intake 추가 Source Channel: `Workforce Service Desk Public Entry`
- Request Envelope 확장: `requester_type`, `identity_verified`, `accessible_scope`
- Request Type Candidate: `PAYSLIP`, `SETTLEMENT_INQUIRY`, `COMMISSION_INQUIRY`, `CERTIFICATE`, `TAX_DOCUMENT`, `CONTRACT_DOCUMENT`, `PERSONAL_INFO_CORRECTION`, `GENERAL_HR`
- 조회 가능 정보는 Request 생성 없이 Self-Service; 담당자 처리가 필요한 경우에만 Request 생성

### Historical Pending Reduction Working Notes — SUPERSEDED / 현재 Pending 판단에 사용 금지

> 아래 A~D 및 후속 기존 Register 내용은 Pending Reduction 이전 작업이력입니다. 현재 Pending 판정은 문서 최상단 `Pending Reduction Superseding Update — 2026-08-21`만 사용합니다.

#### Historical Question — 당시 `지금 더 처리할 수 있는가?` 검토

#### A. 지금 PM/기획에서 바로 더 진행 가능

아래는 신규 Owner Decision 없이 **초안·Logical Spec·개발 준비자료를 더 완성할 수 있는 항목**입니다.

- **N-01 Screen ID / Route:** Official ID를 임의 확정하지는 않되, Screen Family별 **ID 제안안·Route Proposal·Naming Rule**까지 작성 가능.
- **N-02 UX Composition:** List / Detail / Tab / Drawer / Modal / Embedded 구성을 실제 화면 설계 수준까지 분해 가능.
- **N-03 Admin / Permission Navigation:** 권한 메뉴의 진입 위치와 Role별 노출 Proposal 작성 가능.
- **N-04 Permission Matrix:** Role / Team / Row / Field / Action별 **권한 Matrix 초안** 작성 가능. 최종 민감정보 기준만 승인 필요.
- **N-05 Vehicle / Parking / Schedule:** 상태값·필수필드·화면·업무 흐름·예외처리를 더 상세화 가능. 비용·공개범위 같은 정책값만 일부 승인 필요.
- **N-06 SLA / Retry / Priority:** Request Type별 **권장 SLA·Priority·Escalation Candidate** 작성 가능. 실제 운영값은 승인 후 Freeze.
- **I-11 Request / Cross-Service Contract:** Logical Contract는 이미 있으며, API Payload Candidate / Event / Status Mapping / Error Contract 초안까지 진행 가능. 실제 Endpoint·Provider Binding만 후속.
- **I-12 Legacy WDI Migration:** Legacy 데이터 Inventory → Keep / Migrate / Reference-only / Archive Candidate까지 지금 Audit 가능.

#### B. 기획은 더 진행 가능하지만 대표·운영정책 최종확정 필요

- **I-05 Finance / Billing / Receivable:** Entity/Flow/State 초안은 가능. 실제 회계처리·지급·원장 경계는 운영/재무 결정 필요.
- **I-06 Compensation:** 계산엔진 구조와 Formula Slot은 설계 가능. **상품/직군별 실제 비율·금액**은 Owner 결정 필요.
- **I-10 HR Identity / Retention:** Flow/Permission/문서구조는 설계 가능. 본인확인 수준·법정 보관기간·파기정책은 정책/법무 확인 필요.
- **N-05/N-06 일부:** 공개범위, 우선순위, SLA 시간 등 실제 운영값은 Owner/운영 승인 필요.

#### C. 공통인프라/개발 Architecture가 있어야 최종 종료 가능

- **I-01 Shared Person**
- **I-02 Shared Merchant / Store ↔ Merchant Account**
- **I-03 Shared IAM**
- **I-04 Shared Device / Asset**
- **I-08 Inventory vs Procurement / Supply Physical Split**
- **I-09 Vault / Secret Physical Architecture**

위 항목도 Logical Contract·Interface는 계속 정리할 수 있지만, Physical DB / Repository / Provider / RLS 등 실제 구현 구조는 공통인프라와 함께 확정해야 합니다.

#### D. 외부업체·실제 계약정보가 있어야 닫히는 항목

- **I-07 External Provider Contracts:** 전자서명, Kakao/SMS/Fax, Carrier, Remote Support, VAN/PG/Bank, Sales Data Provider의 실제 Endpoint / Credential / Callback / 요금·계약조건.

#### PM 판단

현재 Register를 그대로 '더 이상 못하는 일'로 보면 안 됩니다. **A 그룹은 지금 계속 처리하고, B는 Proposal까지 만든 뒤 Owner에게 결정값만 묻고, C/D만 실제 외부 Dependency로 남기는 방식이 맞습니다.**

</details>


---

## Intake Note — 2026-08-21 (Final SOT Resync)

- 본 문서는 Notion Final Pending Register의 **Final SOT Freeze 판본**을 GitHub에 Resync한 것이다. 직전 입고본(중간 Snapshot)은 커밋 `42e753d`로 보존된다.
- Resync 반영분: `FINAL PENDING CONTROL — SOT FROZEN` 블록(Human Handoff Ready **YES**, Final Fix Verification **6/6 PASS**, Workforce Service Desk Supplemental **MERGED / VERIFIED**) · `Pending Reduction Superseding Update` A~E 분류 · Superseded Pending Note · Historical Working Notes · 독자 안내 callout · 섹션 국문 병기 · **I-10 Logical(One-time Secure Link CLOSED) / Physical(Identity Provider·Token·Signed Download Binding Pending) 분리**.
- **Stale Status 처리:** 원문 `Pending Reduction Superseding Update > Current Verdict`에 `Human Handoff Ready: NO`가 남아 있다. 원문 최상단 블록이 이를 Historical Status로 명시 대체하므로 **삭제하지 않고 원문 그대로 보존**하되, 해당 위치와 `E. ... FINAL FIX VERIFICATION PENDING` 제목 아래에 Intake Note를 부기해 현재 확정 상태가 `YES` / `MERGED / VERIFIED`임을 명시했다. 문서의 Current Status는 최상단 블록이다.
- 기존 `PENDING_REGISTER.md` (`PP-OC-PENDING-001`)는 삭제·덮어쓰기하지 않았다. 두 문서는 계속 병존한다.
- Pending 값은 임의 확정하지 않았다.
