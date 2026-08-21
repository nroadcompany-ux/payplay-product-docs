# PayPlay OC — Screen & Navigation / Traceability

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/08_SPECIFICATIONS/SCREEN_NAVIGATION_TRACEABILITY.md` |
| Document ID | PP-OC-SCREEN-NAV-TRACE-001 |
| Version | v1.0 Final Candidate |
| Status | FREEZE READY WITH NON-BLOCKING SCREEN ID / UX / INTEGRATION PENDINGS |
| Source of Truth | NO — Final Candidate. Main PM 승인 전 APPROVED / Source of Truth YES로 승격하지 않는다. |
| Source Basis | Owner Decision + Document #1 Final Candidate + CLEAN Flow/Rule + Approved Screen Specs + Request Type Master + Cross-Service + Legacy Final Audit |
| Owner | PayPlay OC |
| Last Reviewed | 2026-08-21 |
| Development Use | Logical Screen Family / Navigation / Entry / Projection / Permission / Traceability baseline. 신규 Family Official Screen ID와 Physical Route binding은 별도 normalization 전 확정 금지. |
| Notion Source | https://app.notion.com/p/3c353327fb86810a9518dd4fe603be4a |
| Developer Package | Document #4 / 4 |
| Related Document | [SCREEN_SPECIFICATION_TRACEABILITY_SUMMARY.md](./SCREEN_SPECIFICATION_TRACEABILITY_SUMMARY.md) (PP-OC-SPEC-TRACE-001 — Coverage/Gap Summary, 본 문서가 대체하지 않음) |
| Related Pending | [FINAL_PENDING_REGISTER.md](../09_DECISIONS/FINAL_PENDING_REGISTER.md) |

> 🧭 PayPlay OC Developer Package Document #4. 기존 52 Official-normalized Logical UI Surface를 보존하면서 최신 5개 OC-native Screen Family, Embedded/External Surface, Navigation, Permission, Request/Integration, Legacy Regression Trace를 하나의 최종 Candidate로 통합한다. 신규 Official Screen ID 및 Physical Route/API/DB를 임의 확정하지 않는다.

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

Navigation: 독립 Primary 1Depth로 강제하지 않는다. Today / Customer Support / Domain Queue에서 role-based entry 가능.

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
- OC Contract Detail에서는 Source Document / e-sign status / assisted exception action을 제공할 수 있으나 별도 고객용 Self-Service Screen을 만들지 않는다.

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
2. Customer
3. Sales
4. Contract & Fulfillment
5. Customer Support
6. Product & Commercial Policy
7. Inventory & Supply
8. Restricted Management

### Restricted Management 2Depth

- Finance
- Compensation
- People / HR
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
- **#2 User & Operations Flows:** [USER_AND_OPERATIONS_FLOWS.md](../04_FLOWS/USER_AND_OPERATIONS_FLOWS.md)
- **#3 Detailed Requirements & Business Policies:** [DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md](../05_REQUIREMENTS_POLICIES/DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md)
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

## Intake Note — 2026-08-21

- 본 문서는 Notion Developer Package Document #4를 GitHub에 신규 입고한 것이다.
- 기존 `SCREEN_SPECIFICATION_TRACEABILITY_SUMMARY.md` (`PP-OC-SPEC-TRACE-001`)는 **Screen Specification Coverage / Gap Delta / Audit Findings 문서**로 본 문서와 Document ID·목적·내용이 다르다. 본 문서는 그 문서를 대체하거나 덮어쓰지 않으며, 두 문서는 병존한다.
- Header Status는 Notion 원문의 `FREEZE READY WITH NON-BLOCKING SCREEN ID / UX / INTEGRATION PENDINGS`를 유지했다. 입고 과정에서 `APPROVED` / `Source of Truth YES`로 승격하지 않았다.
