# PayPlay OC — Service Architecture / Menu & Depth

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/07_ARCHITECTURE/SERVICE_ARCHITECTURE_MENU_DEPTH.md` |
| Document ID | PP-OC-SVC-ARCH-MENU-001 |
| Version | v1.0 Final Candidate |
| Status | FREEZE READY WITH NON-BLOCKING PENDINGS |
| Final SOT Freeze | COMPLETE — 2026-08-21 16:54 KST · Human Handoff Ready: YES |
| Source of Truth | NO — Final Candidate. Main PM 승인 전 APPROVED / Source of Truth YES로 승격하지 않는다. |
| Source Basis | Owner Decision + OC Final SOT + CLEAN Flow/Rule + Screen/Navigation + Cross-Service + Legacy Final Audit |
| Owner | PayPlay OC |
| Last Reviewed | 2026-08-21 |
| Development Use | Service boundary / Menu / Depth / Capability placement / Navigation baseline. Physical binding 금지. |
| Resync | 2026-08-21 Final SOT Resync (Main PM GO) |
| Notion Source | https://app.notion.com/p/3c353327fb86819391f4d550f3dcdb10 |
| Developer Package | Document #1 / 4 |
| Related Pending | [FINAL_PENDING_REGISTER.md](../09_DECISIONS/FINAL_PENDING_REGISTER.md) |

## ✅ FINAL SOT FREEZE — 2026-08-21 16:54 KST

- Human Handoff Ready: **YES**
- Final SOT Freeze: **COMPLETE**
- Final Fix Verification: **PASS**
- Structural / Ownership / Menu↔Screen Trace Conflict: **0**
- Existing Logical ID Damage: **0**
- Package-wide Scope-Blocking Pending: **0**
- Remaining Pending: **Physical / Provider / Config boundaries only**

> 본 문서는 현재 OC Architecture/Menu Logical SOT로 Freeze합니다. Physical DB/API/IAM/Provider 값을 임의 확정하지 않습니다.

---

> 👀 **이 문서는 언제 보나요?**
> OC의 메뉴와 기능이 **어느 업무영역에 속하는지** 확인할 때 보는 문서입니다. 개발 전 전체 제품 지도를 잡는 용도입니다.
> 주요 용어: Service Architecture (서비스 구조), Menu & Depth (메뉴 및 단계), Domain (업무영역), Capability (기능 역량), Ownership (담당/소유 책임), Projection (조회·표시용 반영 화면), Self-Service (가맹점 직접 처리).

> 🧭 PayPlay OC Developer Package Document #1. 최신 Owner Direction, CLEAN Flow/Rule, Screen/Navigation, Cross-Service, Legacy Preservation Audit를 반영한 Service Architecture / Menu & Depth 최종 Candidate다. Physical DB/API/Provider/Official Screen ID를 확정하지 않는다.

---

## 1. Architecture Principle

- OC는 가맹점·영업·견적·계약·이행·설치·AS·재고·공급·재무·보상·People/HR·회사운영·경영 의사결정의 **내부 Operational System**이다.
- 메뉴는 `기능이 존재한다`가 아니라 `직원이 독립적으로 진입해 반복적으로 운영해야 하는 업무영역인가`를 기준으로 노출한다.
- Projection / Self-Service / Communication / Search Utility를 불필요한 1Depth Menu로 승격하지 않는다.
- `Legacy Reality ≠ Target Architecture`. 단 Legacy 기능은 무근거 삭제하지 않고 Target Mapping 또는 명시적 Preservation 분류를 가진다.

---

## 2. Primary Navigation (주요 메뉴) — 1Depth

1. **Today / Work Queue (오늘 / 업무대기열)** — 개인/팀 처리대상, Attention (주의필요), Approval Attention (승인필요)
2. **Customer (가맹점)** — Customer List (가맹점목록) / Customer 360 (가맹점 360)
3. **Sales (영업)** — Lead (리드) / Opportunity (영업기회) / Visit·Consultation (방문·상담) / Sales Activity (영업활동) / Quote (견적) 연결
4. **Contract & Fulfillment (계약 및 이행)** — Contract (계약) / Contract Item (계약항목) / Change·Transfer·Termination (변경·양도양수·해지) / Fulfillment (이행) / Installation (설치) / Work (작업) / Verification (검수)
5. **Customer Support (가맹점지원)** — Unified Intake (통합접수)에서 Service/AS (서비스/AS)로 분기된 Case (케이스) / Remote (원격) / Field (현장) / Vendor (협력사) / Resolution (해결)
6. **Product & Commercial Policy (상품 및 영업정책)** — Product (상품) / Commercial Policy (영업정책) / Version (버전) / Price·Margin·Rule (가격·마진·규칙)
7. **Inventory & Supply (재고 및 공급)** — Stock (재고) / Reservation (예약) / Supply·Purchase (공급·구매) / Shipment (배송) / Return·Exchange (반품·교환) / Asset Reference (자산참조)
8. **Restricted Management (제한관리)** — Finance (재무) / Compensation (보상) / People·HR (인사·HR) / Company Operations (회사운영) / Management Decision (경영의사결정)

---

## 3. Restricted Management (제한관리) — 2Depth

### Finance (재무)

Expense (비용) / Settlement (정산) / Receivable·Payment Reference (미수금·지급참조) / Vendor·Counterparty (공급사·거래상대방) 관련 Restricted (제한) 업무.

### Compensation (보상)

Eligibility (지급자격) / Calculation (계산) / Approval (승인) / Adjustment (조정). 정확 Formula/Rate (계산식/비율)는 Pending (미확정).

### People / HR (인사 / HR)

Employee·Worker (직원·근무자) / Organization·Role (조직·역할) / Attendance (근태) / Leave (휴가) / Onboarding·Offboarding (입사·퇴사) / Workforce Service Desk (인력 업무 요청센터: 재직자 Self-Service + 외부직원·퇴사자·해촉자 Public Entry).

### Company Operations (회사운영)

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

### Management / Decision (경영 / 의사결정)

Decision (결정) → Reason (사유) → Expected Result (기대결과) → Execution Handoff (실행인계) → Actual Result (실제결과) → Review (복기).

---

## 4. Common / Collaboration (공통 / 협업)

- **Schedule / Meeting (일정 / 미팅)** — 영업방문·설치·AS·회의·행사 등 Time Commitment (시간약속). Source (원천) 업무 State (상태)는 각 Domain (업무영역)이 소유.
- **Global Search (통합검색)** — Customer (가맹점) / Contract (계약) / Case (케이스) / Resource (자원) 등 권한 범위 검색. Company Resource Directory (회사 자원 디렉터리) 포함.
- **Notification (알림)** — 업무 변화 Signal (신호). Source State Owner (원천상태 소유자) 아님.
- **Team Chat (팀채팅)** — Contextual Collaboration (업무맥락 협업).
- **AI Assistant (AI 도우미)** — 권한 기반 Retrieve (조회) / Summarize (요약) / Suggest (제안) / Prepare (초안준비). 고위험 Approval (승인) / Decision (결정) / Commit (확정반영) 자율 금지.
- **Profile / Permission Context (프로필 / 권한정보)** — 사용자·Role (역할)·Scope (범위) Context (정보).

---

## 5. Conditional Entry (조건부 진입)

- **Approval Center (승인센터)** — Role (역할)/업무상 필요 시 독립 진입. 일반 사용자는 Today (오늘) > Approval Needed (승인필요)에서도 접근 가능.
- **Admin / Permission (관리자 / 권한)** — Authorized Admin (인가된 관리자) 전용. 최종 Sidebar placement (사이드바 배치) 및 Physical IAM (물리 IAM)은 Pending (미확정).

---

## 6. Unified Intake — Multi-Entry / Single OC Intake

가맹점 접수 Entry는 복수일 수 있다.

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

기존 Pending Reduction 이전에 정의된 추가 OC-native Family baseline은 아래 5개다.

1. Vehicle (차량관리)
2. Parking (주차관리)
3. Schedule / Meeting (일정 / 미팅)
4. Unified Intake / Request Operations (통합접수 / 요청운영)
5. Company Resource Directory / Company Information (회사 자원 디렉터리 / 회사정보)

이후 Owner Decision으로 Workforce Service Desk가 추가되었으며, 해당 Surface는 `OC-WSD-*` Internal Operator/Self-Service Family와 `OC-WSD-PUBLIC-*` Public Entry Family의 Supplemental 2개 Family로 관리한다. 따라서 `52 + 5 + 2 = 최종 독립 화면 수`처럼 단순 합산하지 않는다.

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
- **#2 User & Operations Flows:** [USER_AND_OPERATIONS_FLOWS.md](../04_FLOWS/USER_AND_OPERATIONS_FLOWS.md)
- **#3 Detailed Requirements & Business Policies:** [DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md](../05_REQUIREMENTS_POLICIES/DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md)
- **#4 Screen & Navigation / Traceability:** [SCREEN_NAVIGATION_TRACEABILITY.md](../08_SPECIFICATIONS/SCREEN_NAVIGATION_TRACEABILITY.md)
- **Package Guide:** [DEVELOPER_PACKAGE_GUIDE.md](../DEVELOPER_PACKAGE_GUIDE.md)

이 문서에서 기능 위치와 Ownership을 먼저 확인한 뒤 #2에서 업무 목적/상태변화를 읽고, #3에서 Rule/Validation/Permission을 확인한 후 #4에서 실제 Screen/Navigation 구현 위치를 확인한다.

---

## Workforce Service Desk Architecture Supplemental — 2026-08-21

### Ownership / Boundary

- **Owner / Source of Truth:** PayPlay OC
- OSP는 본 기능의 Owner가 아니다. 필요 시 홈페이지·고객센터에서 OC Public Entry로 연결하는 Navigation Link만 제공할 수 있다.
- Internal Processing Owner: HR / Compensation / Finance
- Entry / Request Routing / History Owner: Workforce Service Desk / Unified Intake

### Placement

Workforce Service Desk는 `Restricted Management / People & HR`와 연계되는 **OC 공통 Self-Service Capability**로 정의한다. 내부 재직자는 OC 로그인 후 접근하고, OC 계정이 없는 외부직원·퇴사자·해촉자는 별도 Public Entry Surface를 사용한다.

### Entry Model

- Internal Entry: `OC → Workforce Service Desk → My Payroll / Compensation / Settlement / Documents / Requests`
- Public Entry: `OC Workforce Service Desk Public Entry → Identity Verification → Accessible Scope → Self-Service / Request`
- Public Entry는 독립 OSP Product 기능으로 정의하지 않는다.

### Identity Verification

`Public Entry → 최소정보 입력 → Existing Shared Person/Worker Match → 기존 등록 휴대폰/이메일로 One-time Secure Link 시스템 자동 발송 → 추가정보 Match → Verified Scope`

Manual Verification은 Match 실패·연락처 변경/소실·Legacy 데이터 불완전 등 예외에서만 사용한다.

### Capability

- 본인 급여/명세서 조회
- 본인 수당·Commission/정산 조회
- 확정 지급내역 및 발행문서 조회/다운로드
- 해촉·경력·위촉·세무·계약 관련 문서 요청
- 미정산/오류/이의/개인정보 정정 Request
- Secure Result / Document Delivery

### Request Rule

조회 가능한 확정 정보는 Request/Ticket을 생성하지 않는다. 담당자 판단·발급·수정·정정이 필요한 경우에만 Unified Intake Request를 생성한다.

### Physical Boundary

Secure Link Provider/Token, Identity Provider, Signed Download URL, TTL/Retry/Lockout 값은 Physical / Security Config Pending이며 Architecture Owner/Flow를 다시 열지 않는다.

---

## Intake Note — 2026-08-21 (Final SOT Resync)

- 본 문서는 Notion Developer Package Document #1의 **Final SOT Freeze 판본**을 GitHub에 Resync한 것이다. 직전 입고본(중간 Snapshot)은 커밋 `e252b84`로 보존된다.
- Resync 반영분: `FINAL SOT FREEZE` 블록 · 독자 안내 callout · Primary Navigation / Restricted Management 국문 병기 · People/HR의 `Former Employee Service Desk → Workforce Service Desk` 전환 · §9 `OC-WSD-*` / `OC-WSD-PUBLIC-*` Supplemental 2 Family 및 `52 + 5 + 2` 단순합산 금지 Guard · Workforce Service Desk Architecture Supplemental 신설.
- 기존 52 Logical Screen ID와 기존 5개 OC-native Family baseline은 삭제·재번호하지 않았다.
- Header Status는 Notion 원문의 `FREEZE READY WITH NON-BLOCKING PENDINGS`를 유지했다. 입고 과정에서 `APPROVED` / `Source of Truth YES`로 승격하지 않았다.
- Pending 값은 임의 확정하지 않았다.
