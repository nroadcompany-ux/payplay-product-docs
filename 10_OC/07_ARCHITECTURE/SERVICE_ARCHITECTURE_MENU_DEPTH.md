# PayPlay OC — Service Architecture / Menu & Depth

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/07_ARCHITECTURE/SERVICE_ARCHITECTURE_MENU_DEPTH.md` |
| Document ID | PP-OC-SVC-ARCH-MENU-001 |
| Version | v1.0 Final Candidate |
| Status | FREEZE READY WITH NON-BLOCKING PENDINGS |
| Source of Truth | NO — Final Candidate. Main PM 승인 전 APPROVED / Source of Truth YES로 승격하지 않는다. |
| Source Basis | Owner Decision + OC Final SOT + CLEAN Flow/Rule + Screen/Navigation + Cross-Service + Legacy Final Audit |
| Owner | PayPlay OC |
| Last Reviewed | 2026-08-21 |
| Development Use | Service boundary / Menu / Depth / Capability placement / Navigation baseline. Physical binding 금지. |
| Notion Source | https://app.notion.com/p/3c353327fb86819391f4d550f3dcdb10 |
| Developer Package | Document #1 / 4 |
| Related Pending | [FINAL_PENDING_REGISTER.md](../09_DECISIONS/FINAL_PENDING_REGISTER.md) |

> 🧭 PayPlay OC Developer Package Document #1. 최신 Owner Direction, CLEAN Flow/Rule, Screen/Navigation, Cross-Service, Legacy Preservation Audit를 반영한 Service Architecture / Menu & Depth 최종 Candidate다. Physical DB/API/Provider/Official Screen ID를 확정하지 않는다.

---

## 1. Architecture Principle

- OC는 고객·영업·견적·계약·이행·설치·AS·재고·공급·재무·보상·People/HR·회사운영·경영 의사결정의 **내부 Operational System**이다.
- 메뉴는 `기능이 존재한다`가 아니라 `직원이 독립적으로 진입해 반복적으로 운영해야 하는 업무영역인가`를 기준으로 노출한다.
- Projection / Self-Service / Communication / Search Utility를 불필요한 1Depth Menu로 승격하지 않는다.
- `Legacy Reality ≠ Target Architecture`. 단 Legacy 기능은 무근거 삭제하지 않고 Target Mapping 또는 명시적 Preservation 분류를 가진다.

---

## 2. Primary Navigation — 1Depth

1. **Today / Work Queue** — 개인/팀 처리대상, Attention, Approval Attention
2. **Customer** — Customer List / Customer 360
3. **Sales** — Lead / Opportunity / Visit·Consultation / Sales Activity / Quote 연결
4. **Contract & Fulfillment** — Contract / Contract Item / Change·Transfer·Termination / Fulfillment / Installation / Work / Verification
5. **Customer Support** — Unified Intake에서 Service/AS로 분기된 Case / Remote / Field / Vendor / Resolution
6. **Product & Commercial Policy** — Product / Commercial Policy / Version / Price·Margin·Rule
7. **Inventory & Supply** — Stock / Reservation / Supply·Purchase / Shipment / Return·Exchange / Asset Reference
8. **Restricted Management** — Finance / Compensation / People·HR / Company Operations / Management Decision

---

## 3. Restricted Management — 2Depth

### Finance

Expense / Settlement / Receivable·Payment Reference / Vendor·Counterparty 관련 Restricted 업무.

### Compensation

Eligibility / Calculation / Approval / Adjustment. 정확 Formula/Rate는 Pending.

### People / HR

Employee·Worker / Organization·Role / Attendance / Leave / Onboarding·Offboarding / Former Employee Service Desk.

### Company Operations

- **차량관리** — Vehicle master, assignment, 운행, 정비, 보험, 검사, 비용 History
- **주차관리** — 정기·임시·방문 주차, 차량/사용자, 기간, 비용, History
- **회사정보 / Company Resource Directory** — 회사·지점 기본정보 + 업무용 Resource Directory
  - 홈페이지 / 공식 채널 / 블로그
  - 외부 서비스 / Admin URL
  - 계정 ID·이메일 Reference
  - 담당자 / Owner Team
  - Vendor 연락처
  - SOP / 매뉴얼 / Notion / GitHub / 관련문서
  - MFA / Recovery 담당 Context
  - Access Permission / Secret Reference
- 광고 실행·블로그 자동화 자체는 Marketing Play/OSP 경계를 유지한다.
- Password / API Key / Token / Recovery Code는 일반 Resource DB/Search에 평문 저장하지 않고 별도 Secret/Vault Reference로 관리한다.

### Management / Decision

Decision → Reason → Expected Result → Execution Handoff → Actual Result → Review.

---

## 4. Common / Collaboration

- **Schedule / Meeting** — 영업방문·설치·AS·회의·행사 등 Time Commitment. Source 업무 State는 각 Domain이 소유.
- **Global Search** — Customer/Contract/Case/Resource 등 권한 범위 검색. Company Resource Directory 포함.
- **Notification** — 업무 변화 Signal. Source State Owner 아님.
- **Team Chat** — Contextual Collaboration.
- **AI Assistant** — 권한 기반 Retrieve/Summarize/Suggest/Prepare. 고위험 Approval/Decision/Commit 자율 금지.
- **Profile / Permission Context** — 사용자·Role·Scope Context.

---

## 5. Conditional Entry

- **Approval Center** — Role/업무상 필요 시 독립 진입. 일반 사용자는 Today > 승인 필요에서도 접근 가능.
- **Admin / Permission** — Authorized Admin 전용. 최종 Sidebar placement 및 Physical IAM은 Pending.

---

## 6. Unified Intake — Multi-Entry / Single OC Intake

고객·가맹점 접수 Entry는 복수일 수 있다.

`OSP / Business OS / Kakao·CS Channel / External Form / Partner Channel → OC Unified Intake → Customer/Store Match → Request Type → Owner Domain Route → Task/Case/Work → Status/Result Projection`

OC Intake 최소 Logical Context:

- Source Channel
- Request Type
- Customer / Store
- Payload / Attachment
- Consent
- Correlation ID

조회·다운로드·FAQ·정상 Self-Service는 실제 내부 처리 Request가 발생하지 않는 한 OC Request를 생성하지 않는다.

---

## 7. Self-Service Boundary

### Contract Document

정상 경로는 Business OS에서 체결 완료 계약서 조회/다운로드. OC `CONTRACT_COPY_REQUEST`는 누락·권한·Legacy 탐색·특수 재발급 등 예외 지원용.

### Sales Data

정상 경로는 Business OS에서 Store/기간/Source 선택 → 조회 → Export/Download/Fax. KOVAN Legacy 자산은 Reuse First. 오류·미수집·특수자료만 OC Assisted Request.

Self-Service 때문에 Contract/Sales Data Source Ownership을 Business OS로 이동하지 않는다.

---

## 8. Shipment / Customer Messaging

### Shipment

Inventory & Supply가 Source를 소유하며 계약/설치 품목과 온라인 주문 배송을 공통 Shipment 의미로 추적한다. 기존 `OC-INV-002` 확장 우선.

### Customer Operational Messaging

Contract / Schedule / Case / Shipment Event를 받아 Kakao/SMS/Fax 등으로 전달하는 Communication Layer. Message 성공 ≠ Source 업무 완료.

광고/프로모션 메시지는 Marketing Play와 분리한다.

---

## 9. Screen Family Impact

기존 Official-normalized Logical ID 52개는 Recovery 기준으로 유지하며 삭제/재번호하지 않는다.

최신 추가 OC-native Family:

1. Vehicle
2. Parking
3. Schedule / Meeting
4. Unified Intake / Request Operations
5. Company Resource Directory / Company Information

Contract Document / Sales Data 정상 Self-Service는 Business OS Surface이고, Customer Messaging은 Embedded/Common Surface다. 따라서 숫자를 단순 합산해 최종 독립 화면 수로 확정하지 않는다.

---

## 10. Legacy TMS Function Mapping Guard

각 Legacy 기능은 Capability/Menu/Screen/Flow/Rule/Request Type/Integration 중 적절한 Target에 Mapping한다.

미연결 시 반드시 다음 중 하나:

- Explicitly Removed
- Legacy Preservation Only
- Planning Gap

현재 주요 분류:

- CCTV → Current OC Target 제외 + Legacy Preservation
- 광고 실행/관리 → Marketing Play/OSP 경계 + Legacy Record Preservation
- 블로그 마케팅 자동화(MJ) → OC Target 제외 + Legacy Preservation
- 프로젝트관리 → Notion Integration First / Native OC Later Review
- 업무게시판 → Legacy Preservation Only until target need confirmed
- 준비중/숨김 기능 → Planning Gap / Review Queue

무근거 삭제 금지.

---

## 11. Permission / Secret Guard

공통 Permission 모델:

`Role + Org/Team + Row Scope + Field Visibility + Action Permission + Approval Authority + Temporary/Delegated Grant + Audit`

Company Resource Directory 추가 Guard:

- Resource Metadata와 Secret을 분리한다.
- Secret은 별도 Vault/Secret Store를 Reference한다.
- Secret 열람은 Resource별/사용자별 권한, 필요 시 재인증, Access Audit을 적용한다.
- Global Search / AI / Chat도 동일 Authorization을 적용하며 Secret 원문 Indexing 금지.
- 퇴사/권한회수 시 Resource Secret Access도 함께 회수되어야 한다.

---

## 12. Explicit Non-Menu / Boundary Decisions

- Contract Document Self-Service → OC 독립 Menu 아님
- Sales Data Self-Service → OC 독립 Menu 아님
- Kakao/SMS/Fax → 독립 업무 원장 Menu 아님
- Unified Intake → 모든 Request를 Case로 만드는 Menu 아님
- CCTV → Current OC Target 제외
- Native Project Management → 현재 Notion 우선
- Marketing Campaign / Blog Automation 실행 → OC Master 아님

---

## 13. Non-Blocking PENDINGS

- Official Screen ID normalization for 신규 Family
- Company Resource Secret/Vault Provider / Physical architecture
- Company Resource exact Permission Matrix / Re-auth policy
- Shared Person / Merchant / IAM / Device·Asset physical implementation
- Billing/Receivable detail
- Settlement exact formula/state
- Compensation formula/rate/approval
- Inventory vs Procurement/Supply physical split
- e-sign / VAN·PG / Carrier / Kakao·SMS·Fax provider exact contract
- SLA / retry / backoff / reconciliation exact values

---

## 14. Gate

- Target Domain / Ownership: **PASS**
- Menu & Depth: **PASS**
- Self-Service / Projection Boundary: **PASS**
- Multi-Entry / Single OC Intake: **PASS**
- Company Resource Directory inclusion: **PASS WITH PERMISSION/VAULT PENDINGS**
- Legacy Loss Regression: **PASS — NO UNGROUNDED LOSS FOUND**
- Physical Architecture: **NOT FINALIZED WHERE PENDING**

**Overall: FREEZE READY WITH NON-BLOCKING PENDINGS.**

---

## 15. Developer Package Navigation

공식 Reading Order는 `#1 Architecture → #2 Flow → #3 Rule → #4 Screen`이다.

- **#1 현재 문서:** Service Architecture / Menu & Depth
- **#2 User & Operations Flows:** [Notion 원문 — v5.2 CLEAN / CROSS-SYNC](https://app.notion.com/p/3bf53327fb868164bb03d968f010ea1f) · GitHub 입고 보류 (아래 Intake Note 참조)
- **#3 Detailed Requirements & Business Policies:** [Notion 원문 — v4.1 CLEAN / AUDITED](https://app.notion.com/p/3bf53327fb8681ba8a9dceb9dd71652c) · GitHub 입고 보류 (아래 Intake Note 참조)
- **#4 Screen & Navigation / Traceability:** [SCREEN_NAVIGATION_TRACEABILITY.md](../08_SPECIFICATIONS/SCREEN_NAVIGATION_TRACEABILITY.md)
- **Package Guide:** [DEVELOPER_PACKAGE_GUIDE.md](../DEVELOPER_PACKAGE_GUIDE.md)

이 문서에서 기능 위치와 Ownership을 먼저 확인한 뒤 #2에서 업무 목적/상태변화를 읽고, #3에서 Rule/Validation/Permission을 확인한 후 #4에서 실제 Screen/Navigation 구현 위치를 확인한다.

---

## Intake Note — 2026-08-21

- 본 문서는 Notion Developer Package Document #1을 GitHub에 신규 입고한 것이다. 동일 목적의 기존 GitHub 파일은 없었다.
- Header Status는 Notion 원문의 `FREEZE READY WITH NON-BLOCKING PENDINGS`를 유지했다. 입고 과정에서 `APPROVED` / `Source of Truth YES`로 승격하지 않았다.
- Developer Package #2 / #3은 기존 GitHub APPROVED / Source of Truth YES 문서(`PP-OC-FLOWS-001`, `PP-OC-REQS-001`)와 Document ID·Status가 달라 입고를 보류하고 Main PM 판단을 요청했다. 상세는 [FINAL_PENDING_REGISTER.md](../09_DECISIONS/FINAL_PENDING_REGISTER.md) 및 [DEVELOPER_PACKAGE_GUIDE.md](../DEVELOPER_PACKAGE_GUIDE.md)의 Intake Status를 참조한다.
