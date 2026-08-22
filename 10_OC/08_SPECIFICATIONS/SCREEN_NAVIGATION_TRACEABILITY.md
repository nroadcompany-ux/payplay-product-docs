# PayPlay OC — Screen & Navigation / Traceability

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/08_SPECIFICATIONS/SCREEN_NAVIGATION_TRACEABILITY.md` |
| Document ID | PP-OC-SCREEN-NAV-TRACE-001 |
| Version | v1.0 Final Candidate |
| Status | FREEZE READY WITH NON-BLOCKING SCREEN ID / UX / INTEGRATION PENDINGS |
| Final SOT Freeze | COMPLETE — 2026-08-21 16:54 KST · Human Handoff Ready: YES |
| Source of Truth | NO — Final Candidate. Main PM 승인 전 APPROVED / Source of Truth YES로 승격하지 않는다. |
| Source Basis | Owner Decision + Document #1 Final Candidate + CLEAN Flow/Rule + Approved Screen Specs + Request Type Master + Cross-Service + Legacy Final Audit |
| Owner | PayPlay OC |
| Last Reviewed | 2026-08-21 |
| Development Use | Logical Screen Family / Navigation / Entry / Projection / Permission / Traceability baseline. 신규 Family Official Screen ID와 Physical Route binding은 별도 normalization 전 확정 금지. |
| Resync | 2026-08-21 Final SOT Resync (Main PM GO) |
| Notion Source | https://app.notion.com/p/3c353327fb86810a9518dd4fe603be4a |
| Developer Package | Document #4 / 4 |
| Related Document | [SCREEN_SPECIFICATION_TRACEABILITY_SUMMARY.md](./SCREEN_SPECIFICATION_TRACEABILITY_SUMMARY.md) (PP-OC-SPEC-TRACE-001 — Coverage/Gap Summary, 본 문서가 대체하지 않음) |
| Related Pending | [FINAL_PENDING_REGISTER.md](../09_DECISIONS/FINAL_PENDING_REGISTER.md) |

## ✅ FINAL SOT FREEZE — 2026-08-21 16:54 KST

- Human Handoff Ready: **YES**
- Final SOT Freeze: **COMPLETE**
- Final Fix Verification: **PASS**
- Menu↔Screen Trace Break: **0**
- Existing 52 Logical Screen ID Damage: **0**
- Package-wide Scope-Blocking Pending: **0**
- Remaining Pending: **Official new Screen ID / Physical Route / IAM binding / Provider·Config boundaries only**

> 본 문서는 현재 OC Screen & Navigation Logical SOT로 Freeze합니다. 기존 52 Logical ID를 재번호하지 않으며 신규 Official ID/Physical Route를 임의 확정하지 않습니다.

---

> 👀 **이 문서는 언제 보나요?**
> "이 기능을 어느 화면에서 보여주고, 사용자가 어디에서 어디로 이동하는가?"를 확인하는 **화면·네비게이션 설계 문서**입니다.
> 주요 용어: Screen (화면), Navigation (이동 구조), Traceability (기획↔흐름↔규칙↔화면 연결 추적), Screen Family (관련 화면 묶음), Embedded (다른 화면 안에 포함), External Surface (외부 서비스 화면), Route (화면 경로), Visibility (노출 범위).

## 1. 이 문서는 무엇인가

PayPlay OC의 **화면·네비게이션 구현 지도**입니다. "#2 Flow와 #3 Rule을 실제 어느 화면에서 구현하고, 사용자는 어디로 이동하는가"를 보여줍니다. 기존 52개 Logical Screen ID 보존과 신규 Screen Family 분류가 핵심입니다.

## 2. 목적과 문서의 성격

- **왜 존재하는가:** 개발자가 "이 Rule을 어느 화면/Action에 코딩하는가"를 바로 찾을 수 있도록
- **누가 사용하는가:** 개발자(Screen 구현 위치), UX/UI(Navigation 설계), 기획자(Screen 분류·Trace 검수)
- **무엇을 결정하는가:** Logical Screen Family 분류, Navigation 구조, Menu↔Screen Trace, Permission/Visibility Baseline, Request Type↔Target Screen Trace
- **무엇은 결정하지 않는가:** 업무 Flow 순서(→ #2), Rule/Validation 세부(→ #3), Official Screen ID/Physical Route(→ Normalization Pending)

## 3. 핵심 내용

1. **기존 52 Logical Screen ID 전수 보존** (재번호 금지) — §2에 전체 목록
2. **신규 5개 OC-native Family** (Official ID Pending): Vehicle / Parking / Schedule·Meeting / Unified Intake / Company Resource Directory
3. **WSD Supplemental Screen Family:** OC-WSD-*(Internal Operator/Self-Service) + OC-WSD-PUBLIC-*(Public Entry) — §WSD Supplemental
4. **Navigation Baseline:** 1Depth 8개 + Restricted Management 2Depth + Common/Collaboration + Conditional Entry — §5
5. **Screen이 아닌 것:** Business OS Self-Service Surface(Contract/Sales Data), 모든 Request를 Case로 강제 흡수 금지, 52+5=57로 단순 확정 금지
6. **Permission Baseline:** Role + Org/Team + Row Scope + Field Visibility + Action + Approval + Audit — §10
7. **Request Type → Target Screen Trace** 8종 모두 연결됨 — §8
8. **Legacy Regression:** CCTV/광고/블로그 등 전수 Explicitly Removed/Preservation/Planning Gap 분류 — §13

## 4. 언제 / 어떻게 읽는가

- **개발자:** #1(기능 위치) → #2(Flow) → #3(Rule) → **#4(이 문서, Screen 구현 위치)** 마지막 단계
- **UX/UI:** §5 Navigation Baseline을 먼저 보고 신규 Family 설계 시 §3 참조
- **기획자:** §17 Gate 결과 및 §13 Legacy Regression Trace 확인
- **관련 문서:** #1(Architecture), #2(Flow), #3(Rule), Final Pending Register(ID Normalization Pending 경계)

## 5. 현재 상태

- **Human Handoff Ready: YES**
- **Final SOT Freeze: COMPLETE**
- **Package-wide Scope-Blocking Pending: 0**
- **Owner Decision Required: 0**
- **Development Blocker: 0**
- 남은 Pending: 신규 5 Family Official Screen ID / Physical Route / UX Composition / Exact Permission Matrix
- GitHub Final Resync: Main PM VERIFIED 판정 후 main Merge 예정

---

## 6. 기존 본문 (Screen / Navigation 전문)

> 🧭 PayPlay OC Developer Package Document #4. 기존 52 Official-normalized Logical UI Surface를 보존하면서 Pending Reduction 이전 baseline 5개 OC-native Screen Family와 이후 추가된 Workforce Service Desk Supplemental 2개 Family, Embedded/External Surface, Navigation, Permission, Request/Integration, Legacy Regression Trace를 하나의 최종 Candidate로 통합한다. 신규 Official Screen ID 및 Physical Route/API/DB를 임의 확정하지 않는다.

---

## 1. Screen Architecture Principle

- Screen 수보다 `Source Domain / User Intent / Navigation / State Ownership / Permission`을 우선한다.
- List / Detail / Workspace / Modal / Drawer / Tab / Projection을 모두 독립 Screen으로 과대 산정하지 않는다.
- 기존 52 Logical ID는 Recovery/Approved Spec의 정규화된 식별자 집합으로 유지하며 삭제·재번호하지 않는다.
- 최신 신규 Family에는 아직 Official Screen ID를 생성하지 않는다.
- Business OS Self-Service Surface를 OC Screen Inventory에 중복 포함하지 않는다.
- Embedded Communication / Projection을 독립 Source Screen으로 오해하지 않는다.

---

## 2. Existing Normalized Logical IDs — 52 Preserved

### Shell / Cross — 5

`OC-TODAY-001`, `OC-SEARCH-001`, `OC-NOTIFY-001`, `OC-AI-001`, `OC-CHAT-001`

### Customer — 6

`OC-CUST-001~006`

### Sales — 7

`OC-LEAD-001~002`, `OC-MATCH-001`, `OC-OPP-001~003`, `OC-TOUCH-001`

### Quote — 5

`OC-QUOTE-001~005`

### Approval — 2

`OC-APPROVAL-001~002`

### Contract / Fulfillment / Work — 12

`OC-CONTRACT-001~003`, `OC-FULFILL-001~003`, `OC-WORK-001~002`, `OC-MOBILE-001~003`, `OC-VERIFY-001`

### Case / CS / AS — 5

`OC-CASE-001~005`

### Product / Policy / Inventory — 5

`OC-POLICY-001~003`, `OC-INV-001~002`

### Restricted / Admin — 5

`OC-RESTRICTED-001~004`, `OC-ADMIN-001`

**Guard:** 52는 최종 독립 페이지 수가 아니라 기존 정규화 Logical Surface 집합이다.

---

## 3. Latest New OC-native Screen Families — Official ID Pending

### A. Vehicle Management

Candidate surface composition:

- Vehicle List / Status
- Vehicle Detail / History
- Mileage / Operation Log
- Maintenance / Inspection / Insurance
- Fuel / Toll / Cost History
- Assignment / Usage Context

Navigation: `Restricted Management > Company Operations > 차량관리`

### B. Parking Management

Candidate surface composition:

- Parking Overview / Location
- Assignment List
- Assignment Detail/Edit
- Cost / Renewal / Expiry
- Visitor Parking Entry candidate

Navigation: `Restricted Management > Company Operations > 주차관리`

### C. Schedule / Meeting

Candidate surface composition:

- My Schedule
- Team Schedule
- Company Schedule
- Schedule Detail / Create/Edit
- Meeting/Event Detail
- Source-linked Schedule View

Navigation: Common / Collaboration entry. Source workflow deep-link 허용.

### D. Unified Intake / Request Operations

Candidate surface composition:

- Intake Queue / Request List
- Request Detail
- Customer / Store Match context
- Request Type / Owner Domain Routing
- Attachment / Consent / Correlation context
- Status / Handoff / Projection history

Navigation: 독립 Primary 1Depth로 강제하지 않는다. Today / Merchant Support / Domain Queue에서 role-based entry 가능.

### E. Company Resource Directory / Company Information

Candidate surface composition:

- Resource Directory List / Search
- Resource Detail
- Company / Branch Information
- Official Channel / External Service Link
- Owner / 담당자 / Vendor / SOP / Manual / Related Document
- Access Request / Secret Reference context

Navigation: `Restricted Management > Company Operations > 회사정보`

Global Search: `OC-SEARCH-001`에서 권한 범위 내 Resource 검색 가능.

---

## 4. Extension / Embedded / External Surfaces — Do Not Count as New OC Master Screens

### Shipment

- 기존 `OC-INV-002 Shipment/Asset Detail` 확장 우선.
- Order / Contract Item / Customer 360은 Shipment Projection/Deep-link만 소비.

### Contract Document Self-Service

- 정상 경로는 Business OS.
- OC Contract Detail에서는 Source Document / e-sign status / assisted exception action을 제공할 수 있으나 별도 가맹점용 Self-Service Screen을 만들지 않는다.

### Sales Data Self-Service

- 정상 경로는 Business OS.
- OC는 provider/source 상태, assisted exception, error context를 운영 화면에서 처리.

### Customer Operational Messaging

- Contract / Schedule / Case / Shipment 등 Source Detail의 Embedded Action 또는 Communication History.
- Message send success는 Source Business State를 변경하지 않는다.

### Approval

- `OC-APPROVAL-001/002`는 Conditional Entry이며 모든 사용자의 고정 1Depth 메뉴를 의미하지 않는다.

---

## 5. Navigation Baseline

### Primary 1Depth

1. Today / Work Queue
2. Merchant
3. Sales
4. Contract & Fulfillment
5. Merchant Support
6. Product & Commercial Policy
7. Inventory & Supply
8. Restricted Management

### Restricted Management 2Depth

- Finance
- Compensation
- People / HR
  - Workforce Service Desk (재직자 Self-Service / 외부직원·퇴사자·해촉자 Public Entry)
- Company Operations
  - 차량관리
  - 주차관리
  - 회사정보 / Company Resource Directory
- Management / Decision

### Common / Collaboration

- Schedule / Meeting
- Global Search
- Notification
- Team Chat
- AI Assistant
- Profile / Permission Context

### Conditional

- Approval Center
- Admin / Permission

---

## 6. Navigation Rules

- Today는 Source State Owner가 아니며 Source Detail로 Deep-link한다.
- Customer 360은 Projection Hub이며 Sales/Contract/Case/Shipment Source를 중복 소유하지 않는다.
- Schedule은 Time Commitment를 소유/참조하되 Fulfillment/Case/Sales Business State를 복제하지 않는다.
- Unified Intake는 Request Envelope/Route를 관리하며 Domain Business State를 하나의 Generic Case로 통합하지 않는다.
- Company Resource Directory는 외부 서비스의 업무 실행 Owner가 아니라 `찾기/접근/책임/문서/권한` Directory다.

---

## 7. Multi-Entry / Single OC Intake Screen Trace

`OSP / Business OS / Kakao·CS / External Form / Partner Channel → OC Unified Intake → Customer/Store Match → Request Type → Owner Domain → Task/Case/Work → Result/Status Projection`

Minimum visible/traceable context:

- Source Channel
- Request Type
- Customer / Store
- Payload / Attachment
- Consent
- Correlation ID
- Owner Domain / Assignee
- Handoff / Status / Projection History

Normal lookup/download/FAQ/self-resolution은 신규 Request Screen item을 생성하지 않는다.

---

## 8. Request Type → Target Screen Trace

- `SUPPLY_RECEIPT_PAPER` → Unified Intake → Inventory/Supply → `OC-INV-*` / Shipment context
- `SERVICE_AS` → Unified Intake → `OC-CASE-001~005`
- `DOCUMENT_SALES_DATA` → 정상 Self-Service는 Business OS / 예외 시 Unified Intake → assisted data handling
- `CONTRACT_TRANSFER` → Unified Intake → `OC-CONTRACT-001~003` change/amendment context
- `CONTRACT_COPY_REQUEST` → 정상 다운로드는 Business OS / 예외 시 Unified Intake → Contract Document assisted action
- `CONTRACT_TERMINATION` → Unified Intake → Contract Detail / termination action-subflow
- `SALES_PRODUCT_CONSULT` → Unified Intake → Lead/Match/Opportunity (`OC-LEAD-*`, `OC-MATCH-001`, `OC-OPP-*`)
- `REMOTE_SUPPORT` → Unified Intake → Case/Remote Work (`OC-CASE-*`)

---

## 9. Core Flow → Screen Trace

- Lead/Request → Match → Opportunity → `OC-LEAD-* → OC-MATCH-001 → OC-OPP-*`
- Quote → Revision → Approval → Contract → `OC-QUOTE-* → OC-APPROVAL-* → OC-CONTRACT-*`
- Contract Item → Readiness → Schedule → Work → Verification → `OC-CONTRACT-003 → OC-FULFILL-* → Schedule Family / OC-WORK-* → OC-VERIFY-001`
- Case → Triage → Remote/Field/Vendor → Resolution/Reopen → `OC-CASE-001~005`
- Inventory/Supply → Reservation/Supply → Shipment → Return/Exchange → `OC-INV-001/002` + embedded/subview candidates
- Management Decision → Restricted Management / Decision Detail family, 기존 `OC-RESTRICTED-004` entry와 상세 Spec 연결

---

## 10. Permission / Visibility Baseline

공통 모델:

`Role + Org/Team + Row Scope + Field Visibility + Action Permission + Approval Authority + Temporary/Delegated Grant + Audit`

Screen 규칙:

- Navigation이 보인다고 데이터 접근이 허용되는 것이 아니다.
- UI 숨김만으로 권한 구현 금지.
- Assigned technician/external worker/vendor는 Assigned / Explicit Shared 최소범위.
- Finance / Compensation / HR / Executive / Secret 관련 Field는 별도 Field-level guard.
- Search / AI / Chat / Export에도 동일 Authorization 적용.

---

## 11. Company Resource Directory Security Trace

Resource Metadata와 Secret을 분리한다.

Visible metadata candidate:

- Resource / Service Name
- Public/Admin URL
- Account ID/Email reference
- Owner Team / 담당자
- Vendor Contact
- SOP / Manual / Notion / GitHub / Related Document
- MFA / Recovery 담당 Context
- Access status / last verified date

Secret handling:

- Password / API Key / Token / Recovery Code는 일반 DB/Search/AI Index에 평문 저장 금지.
- 별도 Vault/Secret Store Reference 사용.
- Resource별/개인별 열람권한 + 필요 시 재인증 + Access Audit.
- 퇴사/Role 변경 시 Secret access revoke 연계.

---

## 12. Search / AI / Notification Trace

### Global Search — `OC-SEARCH-001`

권한 범위 내 Customer/Store/Contract/Case/Resource 검색. Secret 원문 Index 금지.

### AI Assistant — `OC-AI-001`

Authorized Retrieve만 사용. 권한 없는 Resource/Secret 추론·노출 금지. 고위험 Command 자율 실행 금지.

### Notification — `OC-NOTIFY-001`

업무 변화 Signal. Notification read/ack가 Source Business State를 완료시키지 않는다.

---

## 13. Legacy TMS Function ↔ Screen/Target Regression Trace

- 계약 만료/갱신 → Contract renewal attention / Sales opportunity projection
- POS 청소 → Case/Maintenance Service subflow
- 차량 → Vehicle Family
- 주차 → Parking Family
- 회사정보 → Company Resource Directory / Company Information
- 일정/미팅 → Schedule Family
- 전자계약 개인 UX → Contract/e-sign projection/action
- 제조사 AS → Case/Vendor Handoff
- 배송/택배 → `OC-INV-002` Shipment extension
- 홈페이지 신청함 → Unified Intake
- 매출조회 → Business OS self-service + OC exception/support
- 사용자/보안 → `OC-ADMIN-001` + Shared IAM boundary
- 프로젝트관리 → Notion Integration First
- CCTV → Current Target 제외 + Legacy Preservation
- 광고 실행/블로그 자동화 → OC 실행 Surface 제외, Marketing Play/OSP 경계 + resource link/reference는 Company Resource Directory에서 검색 가능

Unmapped Legacy는 반드시 Explicitly Removed / Legacy Preservation Only / Planning Gap 중 하나로 분류한다.

---

## 14. Screen Count Guard

현재 상태는:

- Existing normalized Logical IDs: **52 preserved**
- New OC-native Screen Families: **5**
- Extension / Embedded / External Surfaces: 별도 존재

따라서 `52 + 5 = 57 final screens`로 선언하지 않는다.

최종 독립 Screen Count는 신규 Family의 List/Detail/Subview/Modal/Drawer/Embedded 분해와 Official Screen ID normalization 후 확정한다.

---

## 15. Non-Blocking PENDINGS

- 신규 5 Family Official Screen ID
- 신규 Family exact route / URL
- Unified Intake exact Screen placement / role-based entry
- Company Resource exact Permission Matrix / Vault provider / re-auth rule
- Schedule visibility / conflict rule
- Vehicle/Parking role matrix 및 Finance relation detail
- Cross-service API / retry / backoff / reconciliation exact values
- e-sign / VAN·PG / carrier / messaging provider binding
- Shared IAM / Person / Merchant / Device-Asset physical implementation

---

## 16. Developer Do-Not-Do

- 신규 Family에 임의 Official Screen ID 생성 금지
- 52를 최종 페이지 수로 해석 금지
- Business OS Self-Service Screen을 OC에 복제 금지
- 모든 Request를 `OC-CASE-*`로 강제 라우팅 금지
- Projection 화면에서 Source State 직접 수정 금지
- Company Resource Directory에 Secret 평문 저장/검색 Indexing 금지
- Today/Notification/AI/Chat가 Source Domain 상태를 직접 소유·완료 처리 금지
- Legacy 기능을 새 메뉴에 안 보인다는 이유만으로 삭제 금지

---

## 17. Gate

- Existing 52 ID Preservation: **PASS**
- New 5 Family Classification: **PASS WITH ID NORMALIZATION PENDING**
- Menu ↔ Screen Navigation: **PASS**
- Flow ↔ Screen: **PASS**
- Rule/Permission Trace: **PASS**
- Request Type ↔ Screen/Owner Domain: **PASS**
- Integration Boundary: **PASS WITH PHYSICAL PENDINGS**
- Legacy Regression Trace: **PASS — NO UNGROUNDED LOSS FOUND**
- Duplicate Source-of-Truth: **0**
- Blocking Screen Conflict: **0**

**Overall: FREEZE READY WITH NON-BLOCKING SCREEN ID / UX / INTEGRATION PENDINGS.**

---

## Developer Package Navigation

공식 Reading Order: `#1 Architecture → #2 Flow → #3 Rule → #4 Screen`

- **#1 Service Architecture / Menu & Depth:** [SERVICE_ARCHITECTURE_MENU_DEPTH.md](../07_ARCHITECTURE/SERVICE_ARCHITECTURE_MENU_DEPTH.md)
- **#2 User & Operations Flows:** [Notion 원문 — v5.2 CLEAN / CROSS-SYNC](https://app.notion.com/p/3bf53327fb868164bb03d968f010ea1f) · GitHub 입고 보류 (아래 Intake Note 참조)
- **#3 Detailed Requirements & Business Policies:** [Notion 원문 — v4.1 CLEAN / AUDITED](https://app.notion.com/p/3bf53327fb8681ba8a9dceb9dd71652c) · GitHub 입고 보류 (아래 Intake Note 참조)
- **#4 현재 문서:** Screen & Navigation / Traceability
- **Package Guide:** [DEVELOPER_PACKAGE_GUIDE.md](../DEVELOPER_PACKAGE_GUIDE.md)

이 문서는 #1~#3에서 정의된 기능·Flow·Rule을 실제 Logical Screen Family와 Navigation에 연결하는 마지막 구현지도다. 신규 Family Official Screen ID 및 Physical Route는 별도 Normalization 전 확정하지 않는다.

---

## Cross-Audit Clarification — Company Resource Account Identifier Visibility

Claude PM3 Independent Cross-Audit의 `MINOR-02`를 반영한다.

- `Account ID / Email reference`는 항상 공개 Metadata라는 뜻이 아니다.
- 해당 값은 Resource별 `Visibility Classification`을 가진다: Public / Internal / Restricted / Secret-Adjacent 후보.
- Login에 직접 사용되는 Account ID, 관리자 전용 Email, Recovery Identifier 등은 일반 사용자·Global Search·AI에 자동 노출하지 않는다.
- Secret 자체(Password / API Key / Token / Recovery Code)와 Secret-adjacent Identifier는 분리하며, 필요 시 동일한 Resource-level / User-level Permission, Re-authentication, Access Audit 정책을 적용한다.
- Global Search는 권한이 없는 Account Identifier의 원문을 Index/검색결과에 노출하지 않는다.
- 정확한 Visibility Matrix와 Vault Provider는 Physical/Security Finalization Pending이다.

**Cross-Audit Resolution:** `MINOR-02 CLOSED / NON-BLOCKING / PERMISSION CLARIFIED`

---

## Workforce Service Desk Screen / Navigation Supplemental — 2026-08-21

### New Screen Families — Candidate

기존 52 Logical Screen ID를 변경하거나 renumber하지 않는다. 아래는 Supplemental Family Candidate이며 Official ID Normalization은 별도다.

- `OC-WSD-*` — Internal Operator / Worker Self-Service Family
- `OC-WSD-PUBLIC-*` — Public Entry / Identity Verification / Secure Result Family

### Internal Surface Candidate

- My Payroll / Payslip
- My Compensation / Commission
- My Settlement / Payment History
- My Documents
- My Requests
- Request Detail / Result
- Operator Queue / Request Detail / Processing History

### Public Surface Candidate

- Public Entry
- Identity Match Input
- Secure Link Sent / Verify
- Verification Failed / Manual Verification Required
- Accessible Scope Home
- Document / Result View
- Request Create / Request Status

### Navigation Rule

- 내부 재직자: 인증된 OC Context에서 Workforce Service Desk로 진입
- OC 계정 없는 외부직원·퇴사자·해촉자: OC Public Entry Surface로 진입
- OSP는 필요 시 링크를 제공할 수 있으나 Surface Owner가 아니다.

### Permission / Security Trace

- `requester_type`, `identity_verified`, `accessible_scope`를 Navigation/Data Authorization에 반영
- Public Entry 사용자는 본인 Scope 밖의 Search/List/Export 기능 금지
- Secure Result는 Public URL이 아니라 인증 Session 또는 만료형 Signed/Secure Link로만 제공
- Identity Match 실패는 일반 Error 종료가 아니라 `MANUAL_VERIFICATION_REQUIRED` Recovery Surface로 연결

### Trace

- Flow: `WSD-C-01`, `WSD-C-02`, `WSD-O-01`
- Unified Intake Source: `Workforce Service Desk Public Entry`
- Request Types: `PAYSLIP`, `SETTLEMENT_INQUIRY`, `COMMISSION_INQUIRY`, `CERTIFICATE`, `TAX_DOCUMENT`, `CONTRACT_DOCUMENT`, `PERSONAL_INFO_CORRECTION`, `GENERAL_HR`
- Rule: `HR-WSD-R01~R04`, `COMP-WSD-R01~R02`, `FIN-WSD-R01~R03`

### Pending Boundary

Official Screen ID / Route normalization, Secure Link token UX detail, exact TTL/Retry/Lockout values는 개발·Security Config 단계 Pending이며 Screen Family 필요성 자체는 CLOSED.

---

## Human Handoff Cross-Audit Round 1 — Unified Intake Entry Guard — 2026-08-21

Claude PM3 독립 Cross-Audit GAP-A01 반영.

- Unified Intake는 독립 Primary 1Depth가 아니다.
- `Today / Merchant Support / Domain Queue`는 가능한 Entry Surface이며, 모든 Role이 동일 Entry를 갖는다는 뜻이 아니다.
- 실제 Unified Intake 진입 Role / Org / Team / Row Scope는 Shared IAM + OC Permission Config에서 관리한다.
- 현재 Product Spec은 Role별 Entry Matrix의 Physical/Config 값을 확정하지 않는다.
- 개발자는 `CS 담당은 Merchant Support`, `영업관리자는 Today`처럼 임의의 고정 Role→Entry 매핑을 코드에 하드코딩하지 않는다.
- Permission Config가 없는 상태에서는 권한이 넓어지는 쪽으로 Default하지 않는다.

Verdict: GAP-A01 CLOSED AT LOGICAL/HUMAN-HANDOFF LEVEL. Exact Role Matrix = IAM/Permission Config Pending.

---

<details>
<summary>📋 Historical Duplicate Audit Evidence — Round 1 (원문 중복 수록 — 내용 보존)</summary>

> Notion 원문(`PP-OC-SCREEN-NAV-TRACE-001`)에 `Human Handoff Cross-Audit Round 1 — Unified Intake Entry Guard` 섹션이 동일 제목으로 2회 수록되어 있다. 첫 번째는 본문에 현행 유지하고, 두 번째를 내용 삭제 없이 본 Toggle로 격리한다. 5번째 항목의 표현만 다르며 Verdict는 동일하다.

### Human Handoff Cross-Audit Round 1 — Unified Intake Entry Guard — 2026-08-21

Claude PM3 독립 Cross-Audit GAP-A01 반영.

- Unified Intake는 독립 Primary 1Depth가 아니다.
- `Today / Customer Support / Domain Queue`는 가능한 Entry Surface이며, 모든 Role이 동일 Entry를 갖는다는 뜻이 아니다.
- 실제 Unified Intake 진입 Role / Org / Team / Row Scope는 Shared IAM + OC Permission Config에서 관리한다.
- 현재 Product Spec은 Role별 Entry Matrix의 Physical/Config 값을 확정하지 않는다.
- 개발자는 특정 Role→Entry를 임의 하드코딩하지 않는다.
- Permission Config가 없는 상태에서는 권한이 넓어지는 쪽으로 Default하지 않는다.

Verdict: GAP-A01 CLOSED AT LOGICAL/HUMAN-HANDOFF LEVEL. Exact Role Matrix = IAM/Permission Config Pending.

</details>

---

## Intake Note — 2026-08-21 (Final SOT Resync)

- 본 문서는 Notion Developer Package Document #4의 **Final SOT Freeze 판본**을 GitHub에 Resync한 것이다. 직전 입고본(중간 Snapshot)은 커밋 `62923ed`로 보존된다.
- Resync 반영분: `FINAL SOT FREEZE` 블록 · 독자 안내 callout · 문서 소개 callout 갱신(baseline 5 + WSD Supplemental 2) · §5 Restricted Management 2Depth의 People/HR 하위 `Workforce Service Desk` 추가 · Workforce Service Desk Screen / Navigation Supplemental(`OC-WSD-*`, `OC-WSD-PUBLIC-*`) 신설 · Unified Intake Entry Guard (GAP-A01) 신설.
- 기존 52 Logical Screen ID는 삭제·재번호하지 않았다. 신규 Family에 임의 Official Screen ID를 생성하지 않았다.
- **중복 격리 (Delta Cleanup 2026-08-21):** 동일 제목 2회 수록 중 **첫 번째는 본문 현행 유지**, **두 번째는 `Historical Duplicate Audit Evidence — Round 1` Toggle로 격리**했다. 내용은 삭제하지 않았고 Verdict·문구 모두 보존된다.
- **원문 참고 1건:** §14 Screen Count Guard는 여전히 `New OC-native Screen Families: 5` / `52 + 5 = 57` 기준으로 서술되어 있고 WSD Supplemental 2 Family가 반영되지 않았다. 문서 #1 §9는 `52 + 5 + 2` 단순합산 금지로 서술한다. 두 서술 모두 "단순 합산 금지"라는 결론은 동일하여 충돌로 분류하지 않았으나, 원문 수정 없이 그대로 보존했다.
- 기존 `PP-OC-SPEC-TRACE-001`(Coverage/Gap Summary)은 본 문서와 목적이 달라 계속 병존한다.
- Header Status는 Notion 원문을 유지했고 `APPROVED` / `Source of Truth YES`로 승격하지 않았다.
