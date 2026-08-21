# PayPlay OC — Detailed Requirements & Business Policies

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/05_REQUIREMENTS_POLICIES/DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md` |
| Document ID | PP-OC-REQ-BIZ-POLICY-001 |
| Version | v4.1 CLEAN / AUDITED |
| Status | FREEZE READY / CLEAN / AUDITED / LATEST SOT SYNCHRONIZED |
| Final SOT Freeze | COMPLETE — 2026-08-21 16:54 KST · Human Handoff Ready: YES |
| Source of Truth | NO — Main PM 승인 전 APPROVED / Source of Truth YES로 승격하지 않는다. |
| Source Basis | Owner Decision + OC Final SOT + Candidate 1~5 Frozen + User & Operations Flows + Approved Screen Specification + Cross-Service + latest supplemental Target specs |
| Owner | PayPlay OC |
| Last Reviewed | 2026-08-21 |
| Development Use | Observable Requirement / Business Rule / State / Permission / Validation / Exception / Integration guard baseline. Pending Physical API/DB/Provider values 임의 확정 금지. |
| Resync | 2026-08-21 Final SOT Resync (Main PM GO) |
| Notion Source | https://app.notion.com/p/3bf53327fb8681ba8a9dceb9dd71652c |
| Developer Package | Document #3 / 4 |
| Supersedes | `PP-OC-REQS-001` — [detailed-requirements-and-business-policies.md](./detailed-requirements-and-business-policies.md) (2026-08-21, Claude PM3 지시) |
| Related Pending | [FINAL_PENDING_REGISTER.md](../09_DECISIONS/FINAL_PENDING_REGISTER.md) |

## ✅ FINAL SOT FREEZE — 2026-08-21 16:54 KST

- Human Handoff Ready: **YES**
- Final SOT Freeze: **COMPLETE**
- Final Fix Verification: **PASS**
- Flow↔Rule Trace Break: **0**
- Owner Decision Required: **0**
- Development Blocker: **0**
- Package-wide Scope-Blocking Pending: **0**
- Remaining Pending: **Physical / Provider / Legal·Finance Reference / Operational·Business Policy Config only**

> 본 문서는 현재 OC Detailed Requirements & Business Policies Logical SOT로 Freeze합니다. Config/Reference 값과 Physical Binding을 개발자가 임의 하드코딩하지 않습니다.

---

> 👀 **이 문서는 언제 보나요?**
> 업무 흐름을 실제 기능으로 만들 때 **어떤 조건·권한·검증·상태·예외 규칙을 지켜야 하는지** 확인하는 개발 규칙 문서입니다.
> 주요 용어: Detailed Requirements (상세 요구사항), Business Policies (업무 정책), Validation (입력·조건 검증), Permission (권한), State (상태), Rule (업무 규칙), Exception (예외), Integration (외부/시스템 연동), Acceptance Criteria (완료·검수 기준).

---

> 📘 정우용 개발자님 제공 `상세 요구사항 및 비즈니스 정책` 템플릿 기준으로 PayPlay OC 요구사항을 재정렬한 Clean Version이다. `[OC] User & Operations Flows — Developer Template v5 CLEAN`의 C/O/S/P 29개 Flow와 추적성을 유지한다. 기존 OC Target Architecture와 Owner Decision을 변경하지 않는다.

**Related Document:** [USER_AND_OPERATIONS_FLOWS.md](../04_FLOWS/USER_AND_OPERATIONS_FLOWS.md) (PP-OC-USER-OPS-FLOW-001), Approved Screen Specification, OC Final SOT

**Template Basis:** 상세 요구사항 및 비즈니스 정책 / 사용자 및 운영 흐름

---

## 1. 문서 목적

OC의 업무 의미와 정책을 구현 방식이 아니라 **관찰 가능한 조건·상태·권한·입력·검증·결과** 기준으로 정의한다.

### 1.1 포함 범위

- Customer/Store 식별 및 Customer 360
- Lead/Opportunity/Assignment/상담·방문
- Quote Revision/Approval/발송·수락
- Contract/Contract Item/서명
- Fulfillment/설치/검증/Revisit
- Inventory/발주/배송/Asset 참조
- CS/AS/Case/Escalation
- 비용·정산
- 수당 Eligibility/승인/Adjustment
- 경영 Decision/실행/복기
- Commercial Policy Version/Snapshot
- Queue/Notification/AI 보조
- People / HR — Employee·Worker, Onboarding·Offboarding, Workforce Service Desk 처리 Rule
- Company Operations — Vehicle, Parking, Company Resource Directory, Schedule/Meeting 연계 Rule
- Workforce Service Desk — 재직자 Self-Service + 외부직원·퇴사자·해촉자 Public Entry, One-time Secure Link, HR/Compensation/Finance Routing

### 1.2 제외·미확정 범위

- Shared Person/Merchant/IAM/Device·Asset의 Physical DB/Provider/Repository
- FLOW-007 상품·직군별 계산식·비율·항목별 팀장 단독승인 적용값 — 계산/승인 구조는 확정되어 있으며 실제 Business Policy Config 값만 추후 입력
- 미선정 외부 Provider의 실제 Endpoint/Physical Schema
- Product별 exact Evidence Template

### 1.3 요구사항 해석 원칙

1. 성재님 Owner Decision과 Pending을 분리한다.
2. Business Rule은 조건과 결과가 테스트 가능해야 한다.
3. `Legacy Reality ≠ OC Target Architecture`; 기존 TMS는 Reference다.
4. 외부 연동 실패·timeout·unknown 상태에서 성공 State를 선반영하지 않는다.
5. Physical API/DB/IAM/Provider는 Common Infrastructure/Architecture 결정 전 임의 확정하지 않는다.
6. User Flow 문서와 Requirements 문서가 충돌하면 최신 Owner Decision과 Final SOT를 우선한다.

---

## 2. 용어와 식별자

| 용어 | 정의 | 구분 |
|---|---|---|
| Customer Account | 동일 실질 운영관계로 관리하는 가맹점그룹 | Legal Entity와 다름 |
| Store | 설치·운영·AS가 발생하는 사업장 단위 | Merchant Account와 다름 |
| Merchant Account | Shared Merchant Master의 가맹점 식별 구조 | Store와 별도 Entity |
| Person | Shared Person Master의 개인 식별 대상 | OC는 참조/편집 UI 제공 가능 |
| Quote Revision | 견적의 불변 버전 | Sent 이후 직접 덮어쓰기 금지 |
| Contract Item | 계약 내 개별 상품·서비스 이행 단위 | Contract Header와 분리 |
| Work Item | 설치/AS 등 실제 수행 단위 | Requirement/Case와 연결 |
| Case | 추적이 필요한 가맹점 요청·장애 | 단순 Activity와 구분 |
| Policy Snapshot | 당시 적용된 Rule/Value 불변 기록 | 이후 Policy 변경과 분리 |

**식별자 규칙**

- Context: `CUSTOMER`, `SALES`, `QUOTE`, `CONTRACT`, `FULFILLMENT`, `INVENTORY`, `CASE`, `FINANCE`, `COMP`, `MGMT`, `POLICY`, `COMMON`, `AI`
- Business Rule: `[CONTEXT]-R[일련번호]`
- Flow Trace: User Flow 문서의 `C/O/S/P-[NN]`
- Decision: `DECISION-[NN]`

---

## 3. 바운디드 컨텍스트

| Context | 책임 | 주요 사용자 | 핵심 데이터 | 외부 의존성 |
|---|---|---|---|---|
| CUSTOMER | Customer/Store 관계, Match, Customer 360 Projection | 영업·CS·운영 | Customer Account, Store, Person Ref | Shared Person/Merchant |
| SALES | Lead, Opportunity, Assignment, Touch | 영업 | Lead, Opportunity, Activity | OSP |
| QUOTE | Quote Revision, Approval, Send/Accept | 영업·승인자 | Quote, Revision, Approval | Message Provider |
| CONTRACT | 계약, Contract Item, 서명 | 계약관리 | Contract, Contract Item | e-sign Provider |
| FULFILLMENT | Readiness, Schedule, Work, Verification | 설치팀·기사 | Requirement, Work Item, Evidence | Inventory/Asset |
| INVENTORY | 재고, 예약, 발주, 배송 | 재고·구매 | Inventory Tx, Shipment, Asset Ref | Vendor |
| CASE | CS/AS, Resolution, Escalation | CS·AS | Case, Work Item | Vendor/Provider |
| FINANCE | 비용, 승인, 지급, 정산 | 재무·승인자 | Expense, Settlement | 증빙/회계 Integration |
| COMP | 수당 Eligibility, 계산, 승인, Adjustment | 영업·재무 | Compensation Record | Policy |
| MGMT | 경영 Decision, 실행, 결과검토 | 대표·위임권자·팀장 | Decision, Revision | 없음 |
| POLICY | Commercial Policy Version/Snapshot | Policy Manager | Policy Version, Snapshot | 없음 |
| COMMON | Queue, Notification, Audit, Permission Guard | 전 사용자 | Queue, Notification, Audit | Shared IAM |
| AI | Context 기반 제안·초안 | 내부 사용자 | AI Context, Audit | AI Provider Pending |

### 3.0A Latest Supplemental Capability Areas — Human Handoff Guard

아래 영역은 기존 Bounded Context 식별자 표를 재번호하지 않고 최신 Supplemental Rule/Trace로 포함한다.

- **People / HR** — 고용·위촉 관계, Onboarding/Offboarding, 퇴사·해촉 후 Self-Service 및 문서 요청
- **Company Operations** — Vehicle / Parking / Company Resource Directory / Schedule·Meeting 연계
- **Workforce Service Desk** — Internal Self-Service / Public Entry / Identity Verification / Unified Intake Handoff

이 항목들은 후속 아이디어가 아니라 현재 OC Target Scope다. Physical IAM/Provider/Official Screen ID 등 구현 Binding만 Pending으로 유지한다.

### 3.1 Context Handoff

- `SALES → QUOTE`: Quote Ready Opportunity 전달. 실패 시 Sales 원 상태 유지.
- `QUOTE → CONTRACT`: Accepted Revision + Policy Snapshot 전달. Contract 생성 실패 시 Accepted Revision 유지.
- `CONTRACT → FULFILLMENT`: Signed Contract Item 전달. Fulfillment 상태가 Contract Signed를 되돌리지 않는다.
- `FULFILLMENT ↔ INVENTORY`: Material Requirement/Reservation/Allocation 전달.
- `FULFILLMENT → CASE`: 설치 Failure/Issue 발생 시 Case 생성 가능. 원 Work 이력 유지.
- `CASE → SALES`: 추가구매/교체 필요 시 Opportunity Candidate 전달.
- `POLICY → QUOTE/CONTRACT/COMP`: Approved + Effective Version/Snapshot 제공.

---

## 4. 공통 권한·데이터 규칙

- `COMMON-R01` 모든 중요 Command는 Shared IAM Role/Scope/Permission Guard를 통과해야 한다.
- `COMMON-R02` 사용자는 Assigned/Team/Organization Scope를 벗어난 Restricted Data를 임의 열람·변경할 수 없다.
- `COMMON-R03` 승인권한과 작성권한을 동일 개념으로 취급하지 않는다.
- `COMMON-R04` AI는 Permission을 우회하거나 승인·확정·중요 Commit을 독자 수행할 수 없다.
- `COMMON-R05` 중요 상태변경은 Actor, Before/After, Source, Timestamp를 Audit한다.
- `COMMON-R06` Projection(Customer 360/Today/Queue/Dashboard)은 Source of Truth가 아니다.
- `COMMON-R07` Notification 실패는 이미 성공한 Business Transaction을 Rollback하지 않는다.
- `COMMON-R08` 중복 Command/Callback은 Idempotency Guard를 적용한다.

---

## 5. 입력·검증 공통 규칙

- `VALID-R01` Required/Optional/Conditional Field를 구분한다.
- `VALID-R02` Required 누락 시 해당 Submit/Confirm Command를 차단하고 누락 항목을 표시한다.
- `VALID-R03` Conditional Field는 조건 충족 시에만 Required가 된다.
- `VALID-R04` 외부 Provider 결과가 `timeout/unknown`이면 성공 완료 상태로 전환하지 않는다.
- `VALID-R05` 완료 후 이력 보존이 필요한 Entity는 직접 덮어쓰기보다 Revision/Correction/Adjustment를 사용한다.

---

## 6. Context별 Business Rules

### 6.1 CUSTOMER

- `CUSTOMER-R01` 복수·애매 Match 후보는 자동 Merge하지 않고 Human Review로 보낸다.
- `CUSTOMER-R02` Customer Account와 Store는 논리적으로 구분한다.
- `CUSTOMER-R03` Store와 Merchant Account는 별도 Entity로 연결한다.
- `CUSTOMER-R04` 한 Person은 복수 전화번호를 가질 수 있다.
- `CUSTOMER-R05` 가맹점관계 대표 Person 기본값은 최초/원계약 관계자를 우선하되 법적/PG/정산 명의와 분리한다.
- `CUSTOMER-R06` Shared Person/Merchant의 Physical Owner는 Common Infrastructure이며 OC는 참조/Projection/허용된 편집 UI를 제공한다.

**입력/검증:** 이름, 상호, 전화, 주소, 사업자정보 등 Match 가능한 값. Exact Match Threshold는 Configuration Pending.

**AC 예시:** Given 복수 후보, When Match 실행, Then 자동 Merge 없이 Review Pending이어야 한다.

### 6.2 SALES

- `SALES-R01` Lead/Request는 Source와 최초 접수 이력을 보존한다.
- `SALES-R02` Opportunity는 Customer/Store Context와 연결되어야 한다.
- `SALES-R03` 담당자 배정 시 활성 사용자·Role·Scope를 검증한다.
- `SALES-R04` 담당자 미확정 시 Team Queue에 둘 수 있으며 강제 가짜 Assignee를 만들지 않는다.
- `SALES-R05` 상담/방문/Follow-up은 Activity/Touch 이력을 남긴다.
- `SALES-R06` 기존 가맹점 추가구매도 기존 Customer/Store Context에서 새 Opportunity로 처리한다.

### 6.3 QUOTE

- `QUOTE-R01` Sent/Accepted Quote Revision은 직접 덮어쓰지 않고 New Revision을 생성한다.
- `QUOTE-R02` Quote에는 당시 적용된 Policy Version/Snapshot이 연결되어야 한다.
- `QUOTE-R03` Policy 범위를 벗어나면 Approval이 완료되기 전 Send를 허용하지 않는다.
- `QUOTE-R04` Provider Send 실패/Unknown은 `Sent`로 확정하지 않는다.
- `QUOTE-R05` Accepted 대상은 특정 Quote Revision이며 Quote Header 전체를 추상적으로 수락 처리하지 않는다.

**입력:** 상품/서비스, 수량, 단가/할인, 적용 Policy, 가맹점/Store, 유효기간, 메모/조건.

**AC 예시:** Given Approval Pending Revision, When Send, Then 차단되고 상태는 Approval Pending을 유지한다.

### 6.4 CONTRACT

- `CONTRACT-R01` Contract 생성 Source는 Accepted Quote Revision이어야 한다.
- `CONTRACT-R02` 중복 Conversion은 Idempotency로 차단한다.
- `CONTRACT-R03` 서명 실패/Unknown 상태는 Signed로 전환하지 않는다.
- `CONTRACT-R04` 계약 변경은 원 계약 덮어쓰기보다 Amendment/Revision으로 이력을 보존한다.
- `CONTRACT-R05` Contract Header 상태와 Contract Item Fulfillment 상태는 분리한다.

### 6.5 FULFILLMENT

- `FULFILL-R01` Contract Item별 Requirement/Work를 독립적으로 생성·추적한다.
- `FULFILL-R02` Readiness가 충족되지 않으면 Schedule/Complete를 차단한다.
- `FULFILL-R03` 필수 Evidence가 필요한 Work는 Evidence 누락 시 Verified Complete를 차단한다.
- `FULFILL-R04` Partial/Failure는 원 Work Context를 유지하고 Revisit 또는 Case로 복구한다.
- `FULFILL-R05` 복수 Contract Item은 독립 상태를 가진다.
- `FULFILL-R06` Required/Core Item 완료 시 비핵심 Item이 보류 중이어도 Store Activation을 허용할 수 있다.
- `FULFILL-R07` Contract는 체결완료 상태를 유지하고 Fulfillment는 진행중/부분완료/완료/보류/취소로 별도 관리한다.
- `FULFILL-R08` Item 완료 판정은 계약 문서 + 설치 완료 조건을 기준으로 한다.

### 6.6 INVENTORY

- `INV-R01` 수량 재고와 개별 Installed Asset/Serial은 논리적으로 분리한다.
- `INV-R02` Serial 중요 장비는 입고 시점부터 Asset으로 관리할 수 있다.
- `INV-R03` 복수 Product가 동일 Asset ID를 참조할 수 있다.
- `INV-R04` 재고 부족 시 PO Candidate/외부조달 Flow로 분기한다.
- `INV-R05` Vendor 직배송은 창고 입고 없이 Shipment로 추적할 수 있다.
- `INV-R06` 중복 Inventory Transaction은 Idempotency로 방지한다.
- `INV-R07` Device/Asset Physical Repository는 Common Infrastructure Pending이다.

### 6.7 CASE / CS / AS

- `CASE-R01` 단순 문의와 추적이 필요한 Case를 구분한다.
- `CASE-R02` Case Close와 Work Complete는 별도 Guard를 가진다.
- `CASE-R03` Close 조건 미충족 시 Case Close를 차단한다.
- `CASE-R04` 재발은 Reopen 또는 Linked Case로 원 이력을 보존한다.
- `CASE-R05` Escalation Trigger: 영업중단, 카드/PG 불가, 핵심 전체불능, 반복장애, 설치 직후 중대장애, 강한 불만/해지위험, 약속시간 초과, 외부협업 필요, 다매장 동시 장애.
- `CASE-R06` Severity는 S1 긴급 / S2 높음 / S3 일반 / S4 낮음.
- `CASE-R07` 반복장애 기준은 동일 Store + 동일/유사 증상 + 30일 이내 2회 이상.
- `CASE-R08` Escalation 시 기존 담당자를 유지하며 AS팀장을 공동담당으로 추가하고 팀장은 재배정할 수 있다.
- `CASE-R09` 처리상태는 `접수(New) → 배정(Assigned) → 처리중(In Progress) → 보류/가맹점대기/외부업체대기 → 해결(Resolved) → 종료(Closed)`를 사용하며 `취소(Cancelled)`는 별도 상태로 관리한다. 사용자 표시는 한글명을 우선하고 코드/논리 상태값은 괄호의 영문 표기를 사용한다.

### 6.8 FINANCE

- `FIN-R01` 1원 이상 모든 금액은 금전 승인 대상으로 본다.
- `FIN-R02` 증빙 유형은 세금계산서/영수증을 지원하고 첨부는 Optional이다.
- `FIN-R03` 증빙 미첨부는 Warning이며 저장/승인을 막지 않는다.
- `FIN-R04` 중복 의심은 Warning 후 운영자 확인을 거쳐 진행 가능하다.
- `FIN-R05` 상태는 작성중→검토대기→보류/승인확정→지급대기→정산완료, 별도 취소를 사용한다.
- `FIN-R06` 정산완료 이후 수정은 원본 삭제 대신 Correction/Adjustment로 남긴다.

### 6.9 COMP

- `COMP-R01` Eligibility는 **계약 완료 + 설치 완료 + 회사 입금 완료** 모두 충족해야 한다.
- `COMP-R02` 기본 승인 흐름은 영업팀장 검토 → 대표/최종 Owner 승인이다.
- `COMP-R03` 일부 항목의 팀장 단독승인은 Configuration 가능하나 대상은 Pending이다.
- `COMP-R04` 취소/환불/미수/해지는 원 이력 삭제 없이 다음 지급분 Adjustment/Clawback으로 반영한다.
- `COMP-R05` 상품/직군별 계산식과 수당 비율은 Pending이며 하드코딩하지 않는다.
- `COMP-R06` 완료된 Contract Item 단위로 보상 계산 근거를 만들 수 있다.

### 6.10 MGMT

- `MGMT-R01` 상태는 기안→검토중→보류/반려/결정완료→실행중→결과검토→종료, 별도 취소를 사용한다.
- `MGMT-R02` Authority Mode는 대표전결 / 위임전결 / 합의·승인 필요를 지원한다.
- `MGMT-R03` 확정 Decision은 직접 덮어쓰지 않고 Revision/Supersede한다.
- `MGMT-R04` Decision 실행은 별도 Work/Action과 연결될 수 있다.
- `MGMT-R05` 결과검토 완료 후 종료하며 결정완료만으로 전체 업무가 종료되지 않는다.

**입력:** 제목, Decision 유형, 배경/문제, 결정 필요사항, 제안안, 근거/첨부, 검토/승인 대상, 실행 담당/기한.

**AC 예시:** Given 결정권한 없음, When 결정완료, Then Command를 차단하고 검토중 상태를 유지한다.

### 6.11 POLICY

- `POLICY-R01` 적용 가능한 Policy는 Approved + Effective 상태여야 한다.
- `POLICY-R02` Quote/Contract/Compensation에 적용된 값과 Version은 Snapshot으로 보존한다.
- `POLICY-R03` 이후 Policy 변경으로 기존 Snapshot을 변경하지 않는다.
- `POLICY-R04` Formula Error 또는 Effective Version 없음 시 적용을 차단한다.

### 6.12 AI

- `AI-R01` AI는 현재 사용자의 허용된 Customer/Store/Quote/Contract/Case Context만 사용한다.
- `AI-R02` AI 제안/초안은 Human Confirm 전 중요 Commit을 수행하지 않는다.
- `AI-R03` Human Confirm 후에도 동일 Domain Permission/Guard를 다시 검증한다.
- `AI-R04` Restricted Field 접근은 차단하고 Audit한다.

---

## 7. 알림·후속처리

- `NOTIFY-R01` Assignment, Approval 요청, 일정변경, Case Escalation, 외부대기 장기화 등 실제 Action이 필요한 Event를 Queue/Notification 후보로 한다.
- `NOTIFY-R02` Notification 실패는 Source Transaction 성공 여부와 분리한다.
- `NOTIFY-R03` 알림 클릭 시 사용자의 Permission Scope 안에서 Source Entity로 이동한다.
- `NOTIFY-R04` Projection 지연 시 Source of Truth를 변경하지 않고 재조회/재계산한다.

---

## 8. 외부 연동 공통 규칙

- `EXT-R01` 외부 요청 전 내부 Source ID/Correlation ID를 유지한다.
- `EXT-R02` 외부 성공 기준을 명시적으로 충족하기 전 내부 최종 성공 State를 확정하지 않는다.
- `EXT-R03` Timeout/Unknown은 재조회·재시도·Human Confirm 경로를 제공한다.
- `EXT-R04` Callback 중복/순서역전은 Idempotency와 최종 Business Guard로 처리한다.
- `EXT-R05` 외부 Provider의 Physical Endpoint/Schema는 Provider 선정 전 임의 확정하지 않는다.

---

## 9. User Flow ↔ Rule Traceability

| User Flow | Context | 주요 Rule | 구현/검수 포인트 |
|---|---|---|---|
| C-01 상담·영업 요청 | SALES/CUSTOMER | SALES-R01, CUSTOMER-R01~R03 | 필수값, Handoff, Match, 중복 |
| C-02 견적 확인·수정·수락 | QUOTE | QUOTE-R01~R05 | Revision 불변, 수락 대상, 재발송 |
| C-03 계약 확인·서명 | CONTRACT | CONTRACT-R01~R04, EXT-R01~R04 | 서명 성공/Unknown, 중복 |
| C-04 설치 일정·결과 확인 | FULFILLMENT | FULFILL-R01~R08 | 일정, Partial, Evidence, Activation |
| C-05 CS·AS 요청 | CASE | CASE-R01, CASE-R05~R09 | Case 생성, Severity, Escalation |
| C-06 AS 결과 확인·재요청 | CASE | CASE-R02~R04 | Close Guard, Reopen/Linked |
| C-07 추가구매·변경 요청 | SALES/CUSTOMER | SALES-R06, CUSTOMER-R01 | 기존 Context 재사용 |
| O-01 Match/Opportunity 생성 | CUSTOMER/SALES | CUSTOMER-R01~R06, SALES-R01~R02 | Human Review, Opportunity Link |
| O-02 담당자 배정 | SALES/COMMON | SALES-R03~R04, COMMON-R01~R03 | Role/Scope/활성 사용자 |
| O-03 상담·방문 | SALES | SALES-R05 | Activity, Follow-up |
| O-04 견적 작성·승인·발송 | QUOTE/POLICY | QUOTE-R01~R05, POLICY-R01~R04 | Approval, Snapshot, Send |
| O-05 계약 체결 | CONTRACT | CONTRACT-R01~R05 | Conversion, e-sign, Items |
| O-06 이행 준비·설치 배정 | FULFILLMENT/INVENTORY | FULFILL-R01~R02, INV-R01~R05 | Readiness, 자재, Assignee |
| O-07 현장 설치·검증 | FULFILLMENT | FULFILL-R03~R08 | Evidence, Partial, Failure |
| O-08 재고·발주·배송 | INVENTORY | INV-R01~R07 | Quantity/Asset 분리, Shipment |
| O-09 CS·AS 해결 | CASE | CASE-R01~R09 | Work/Case 상태 분리 |
| O-10 비용·정산 | FINANCE | FIN-R01~R06 | 증빙 Optional, 승인, Adjustment |
| O-11 수당·인센티브 | COMP/POLICY | COMP-R01~R06, POLICY-R01~R04 | Eligibility, Pending Formula |
| O-12 경영 의사결정 | MGMT | MGMT-R01~R05, COMMON-R01~R05 | 입력, 권한, Revision, 결과검토 |
| O-13 기존가맹점 추가구매 | SALES/CUSTOMER | SALES-R06, CUSTOMER-R01~R03 | 기존 Store Context |
| O-14 복수 Item 이행 | FULFILLMENT | FULFILL-R05~R08 | Item 독립상태, Activation |
| O-15 AS Escalation | CASE | CASE-R05~R09, NOTIFY-R01 | Trigger, Severity, 공동담당 |
| S-01 Match 자동보조 | CUSTOMER | CUSTOMER-R01, VALID-R04 | Auto Merge 금지 |
| S-02 Policy Snapshot | POLICY | POLICY-R01~R04 | Version/Resolved Value 보존 |
| S-03 AI 보조 | AI/COMMON | AI-R01~R04, COMMON-R01~R05 | Human Confirm, Permission |
| S-04 Queue/Notification | COMMON | NOTIFY-R01~R04, COMMON-R06~R07 | Source/Projection 분리 |
| P-01 외부 기사 작업 | FULFILLMENT/CASE | FULFILL-R03~R04, EXT-R01~R04 | 결과검증, Partial/Failure |
| P-02 Vendor/배송/외부 AS | INVENTORY/CASE | INV-R04~R06, CASE-R09, EXT-R01~R05 | Waiting External, Shipment |
| P-03 외부 Provider 요청/Callback | COMMON | EXT-R01~R05, COMMON-R08 | Timeout, Callback, Idempotency |

---

## 10. 상태전이 핵심표

| 대상 | 허용 핵심 상태 |
|---|---|
| Quote Revision | Draft → Approval Pending → Approved/Ready → Sent → Accepted/Negotiating/Rejected |
| Contract | Draft/Ready → Signed; 변경은 Amendment/Revision |
| Work Item | Ready → Scheduled → In Progress → Verified/Partial/Failure |
| Case | 접수/New → Assigned → In Progress → 보류/가맹점대기/외부업체대기 → Resolved → Closed; 재발 시 Reopen/Linked |
| Settlement | 작성중 → 검토대기 → 보류/승인확정 → 지급대기 → 정산완료; 별도 취소 |
| Management Decision | 기안 → 검토중 → 보류/반려/결정완료 → 실행중 → 결과검토 → 종료; 별도 취소 |

---

## 11. Acceptance Criteria 공통 기준

1. Required Field 누락 시 Submit/Confirm은 차단되어야 한다.
2. 권한이 없는 Actor의 중요 Command는 상태를 변경하지 않아야 한다.
3. Timeout/Unknown 외부 결과는 성공 상태로 선반영되지 않아야 한다.
4. Revision 대상 Entity의 기존 확정 이력은 덮어쓰지 않아야 한다.
5. 중복 요청/Callback은 Idempotency로 동일 Business Result를 유지해야 한다.
6. Partial/Waiting 상태를 Complete/Closed와 혼동하지 않아야 한다.
7. Source of Truth와 Projection 지연은 분리되어야 한다.
8. 모든 중요 상태변경은 Audit 가능한 Actor/Source/Before/After를 남겨야 한다.

---

## 12. 개인정보·보관·감사

- Person 정보는 Shared Person Master 정책을 따른다.
- OC는 필요한 업무 Scope에서만 Person/Store 정보를 참조한다.
- 계약/금전/승인/정산/경영 Decision의 중요 이력은 임의 삭제보다 Revision/Adjustment/Supersede를 사용한다.
- 실제 보관기간·삭제정책은 Company/Common Infrastructure 정책 확정이 필요하다.

---

## 13. 비기능 요구사항

- 주요 Command는 중복 제출에 안전해야 한다.
- 외부연동은 timeout/재시도/Unknown 상태를 운영자가 식별할 수 있어야 한다.
- 권한 없는 데이터는 UI 숨김만이 아니라 Server-side Guard가 필요하다.
- Customer 360/Today/Queue/Dashboard Projection 지연이 Source Transaction을 훼손해서는 안 된다.
- Audit/History는 운영 분쟁과 복구에 사용할 수 있는 수준으로 남긴다.

---

## 14. 미결정사항 / Risk

### Product/Policy Pending

- FLOW-007 상품/직군별 수당 계산식
- FLOW-007 수당 비율
- FLOW-007 항목별 영업팀장 단독승인 범위

### Common Infrastructure Physical Pending

- Shared Person Master Physical Implementation
- Shared Merchant Master Physical Implementation
- Shared IAM Physical Implementation
- Shared Device/Asset Master Physical Implementation

### Integration Pending

- e-sign Provider 최종 선정
- Message/Email Provider Physical Spec
- 실제 회계/지급 Provider Integration
- AI Provider Physical Architecture

위 항목은 미확정 값을 임의 하드코딩하지 않는다.

---

## 15. 문서 상태 / Coverage

| 검수 항목 | 결과 |
|---|---|
| User Flow 29개와 Traceability | PASS |
| Context 책임 분리 | PASS |
| Permission/Common Guard | PASS |
| 입력·Validation 기준 | PASS |
| 상태전이 기준 | PASS |
| 외부연동 실패/Unknown | PASS |
| Owner Decision P-01~P-05 반영 | PASS |
| FLOW-007 Policy Pending 분리 | PASS |
| Common Infrastructure Physical Pending 분리 | PASS |
| Claude PM3 Independent Audit | COMPLETED — PASS WITH MINOR / MINOR 4건 보정 반영 (2026-08-18) |
| Developer Review | READY TO REQUEST — 공식 Pending 명시 전제 |

**Business Direction Change:** NONE

**New Owner Decision:** NONE

**New Pending:** NONE

**Developer Template Alignment:** COMPLETE CANDIDATE

---

## 18. Latest SOT Synchronization Supplement — 2026-08-21

> 🔄 본 섹션은 2026-08-21 Main PM 추가 SOT를 기존 v4.1 CLEAN Rule 체계에 동기화하기 위한 보강 규칙이다. 기존 Rule ID와 Approved Decision을 변경하지 않으며, 신규 Physical API/DB/Provider/Screen ID를 확정하지 않는다.

### 18.1 Canonical Trace Set 해석 Guard

- 기존 C/O/S/P 29개 Flow는 **기존 Canonical Trace Set**이며 최신 전체 OC Capability 개수로 해석하지 않는다.
- 이후 추가된 Vehicle / Parking / Schedule·Meeting / Self-Service / Unified Intake / Customer Messaging은 기존 Flow·Subflow·Cross-Service Contract에 보강 연결하며, 공식 신규 Flow ID가 승인되기 전 임의 ID를 생성하지 않는다.

### 18.2 Multi-Entry / Single OC Intake

- `COMMON-R09` 가맹점 Request 접수 Entry는 OSP, Business OS, Kakao/CS Channel, External Form, Partner Channel 등 복수 Surface를 허용한다.
- `COMMON-R10` 실제 내부 처리가 필요한 Request의 Operational Master는 **OC Unified Intake**로 단일화한다. Source Surface는 자체 운영 원장을 별도로 만들지 않는다.
- `COMMON-R11` Unified Intake는 최소 `Source Channel`, `Request Type`, `Customer/Store Ref`, `Payload/Attachment`, `Consent Context`, `Correlation ID`를 식별·보존해야 한다. Exact Physical Field/API Schema는 Integration Pending이다.
- `COMMON-R12` OC는 Request Type과 Customer/Store Context를 기준으로 Owner Domain에 Route하며, 처리 결과와 가맹점 노출 상태는 필요한 Source Surface에 Projection한다.
- `COMMON-R13` 조회·다운로드·FAQ·정상 Self-Service는 실제 직원 처리 Request가 발생하지 않는 한 OC Request를 생성하지 않는다.

### 18.3 Contract Document Self-Service

- `CONTRACT-R06` 체결 완료된 전자계약서는 권한이 확인된 가맹점이 Business OS에서 조회·다운로드할 수 있는 Self-Service Projection을 제공한다.
- `CONTRACT-R07` 정상 계약서 조회·다운로드는 OC Request를 생성하지 않는다.
- `CONTRACT-R08` 과거 계약서 누락, 문서 손상/조회 실패, 본인·권한 확인 필요, 특수 재발급/증명 등 예외 상황에서만 `CONTRACT_COPY_REQUEST`를 OC Unified Intake로 전환한다.
- `CONTRACT-R09` Contract/Document 원본 상태와 체결 이력은 Contract Domain이 소유하며 Business OS는 조회/다운로드 Surface 역할을 한다.
- e-sign Provider, 보존기간, 문서 서명검증 방식의 Physical 상세는 기존 Pending을 유지한다.

### 18.4 Sales Data Self-Service

- `COMMON-R14` 매출자료 정상경로는 Business OS에서 매장·기간·자료종류를 선택하여 승인된 VAN/PG/여신계 Source를 조회하고 다운로드 또는 허용된 발송 채널로 전달하는 Self-Service를 우선한다.
- `COMMON-R15` 데이터 미수집, 권한 오류, 특수자료, 수동 증명, Provider 장애 등 정상경로로 해결되지 않는 경우에만 `DOCUMENT_SALES_DATA` Assisted Request를 OC Unified Intake로 생성한다.
- `COMMON-R16` 기존 KOVAN API/수집 구현은 **Reuse First Evidence**로 분류하되, Legacy Physical 구조를 Target Architecture로 자동 승격하지 않는다.
- KIS / 여신협회 / 추가 VAN·PG Provider, Export Format, Fax Provider, Retry/Backoff는 Integration Pending이다.

### 18.5 Shipment / Carrier

- `INVENTORY-R07` 계약상품 배송과 온라인 판매상품 배송은 가능한 한 공통 `Shipment` 운영구조에서 관리한다.
- `INVENTORY-R08` Shipment는 구매/계약 대상, 발송여부, 발송주체, 수령정보, 배송방식, Carrier, Tracking Number, Delivery Status, Return/Exchange/Reship History를 추적 가능하게 해야 한다.
- `INVENTORY-R09` 배송상태의 Source는 Shipment이며 Customer 360, Business OS, Notification, Messaging은 이를 Projection/전달한다.
- `INVENTORY-R10` 송장 등록 또는 배송상태 변경은 Customer Messaging Event를 발생시킬 수 있으나 메시지 발송 성공 여부가 Shipment Business State를 소유하지 않는다.
- 기존 로젠택배/TMS 연동은 Reuse First Evidence이며 현재 Credential/API 유효성은 재검증 필요하다.

### 18.6 Customer Operational Messaging

- `COMMON-R17` Kakao/SMS 등 Customer Messaging은 Source Domain의 Business Event를 받아 가맹점에게 전달하는 Communication Layer이며 업무 원장이 아니다.
- `COMMON-R18` Contract, Fulfillment, Case, Shipment, Schedule 등 Source Domain의 상태를 메시지 발송 결과가 직접 변경하지 않는다.
- `COMMON-R19` System State가 명확한 접수완료·일정확정·계약완료·출고/송장등록·설치완료·AS완료 등은 Auto-send 후보가 될 수 있다.
- `COMMON-R20` 영업자료 선택, 특수 계약, 중요 AS 등 담당자 판단이 필요한 안내는 Semi-auto Draft/Review 후보로 둔다.
- `COMMON-R21` 메시지 발송 실패는 Source Business Transaction을 Rollback하지 않으며 재시도/대체채널/운영확인 Queue로 분리한다.
- Provider, Template Approval, Retry Count/Backoff, Fallback Channel은 Integration Pending이다.

### 18.7 Schedule / Meeting

- `COMMON-R22` Schedule은 시간 약속을 관리하고, Queue는 처리할 일, Notification은 변화 신호를 관리한다. 세 개를 동일 원장으로 통합하지 않는다.
- `COMMON-R23` 설치·영업방문·AS방문 등 Source Workflow에서 일정이 확정되면 동일 내용을 별도 재입력하기보다 Schedule Projection/Relation을 생성하는 방식을 우선한다.
- `COMMON-R24` Schedule 최소 Visibility는 전사 / 부서 / 참여자 / Private 범주를 지원할 수 있어야 하며 Exact Permission Matrix는 Shared IAM/Permission Specification과 정합화한다.
- `COMMON-R25` 일정 변경·취소는 Source Workflow와 Schedule 간 Correlation을 보존하고 중복 일정 생성 방지 Guard를 가져야 한다.

### 18.8 Vehicle / Parking — Company Operations

- `COMMON-R26` Vehicle과 Parking은 People/HR 원장이 아니라 `Restricted Management > Company Operations` 운영 Capability로 관리한다.
- `COMMON-R27` Vehicle은 차량 기본정보, 소유/리스/렌탈, Driver/Owner Relation, 운행, 주유/충전, 정비·점검, 보험·검사, 사고·수리, 비용 및 History를 연결 가능한 운영기록으로 본다.
- `COMMON-R28` Parking은 직원/차량번호, 지점·주차장, 정기/임시/방문, 사용기간, 비용, 회사/개인 부담, 변경이력을 추적 가능하게 한다.
- `COMMON-R29` People/HR 상태변경·퇴사·지점변경은 Vehicle/Parking 운영 확인 Trigger가 될 수 있으나 HR가 Vehicle/Parking 원장을 직접 소유하지 않는다.
- `COMMON-R30` Vehicle / Parking의 신규 Logical Screen ID, Physical Schema, 외부 Parking Provider 연동은 현재 ID/Integration Pending이다.

### 18.9 Permission / Projection / Integration Guard

- 최신 보강 Capability도 `COMMON-R01~R08`의 Permission, Audit, Projection, Idempotency 원칙을 동일 적용한다.
- Business OS / OSP / External Entry는 OC Source State를 직접 Update하지 않고 Handoff 또는 Approved Projection만 사용한다.
- Customer 360 / Today / Schedule / Notification / Messaging / Source Surface는 각 Domain 원장을 복제하는 Secondary Master가 되어서는 안 된다.

### 18.10 Synchronization Verdict

- Structural Conflict: **0**
- Existing Rule/Decision overwritten: **0**
- New Physical Decision: **0**
- New Screen ID fabricated: **0**
- Remaining: Provider / Physical API·DB / Retry·Backoff / exact Permission / Screen ID normalization Pending
- Verdict: **PASS — LOGICAL RULE SYNCHRONIZED WITH NON-BLOCKING INTEGRATION PENDINGS**

---

## Developer Package Navigation

공식 Reading Order: `#1 Architecture → #2 Flow → #3 Rule → #4 Screen`

- **#1 Service Architecture / Menu & Depth:** [SERVICE_ARCHITECTURE_MENU_DEPTH.md](../07_ARCHITECTURE/SERVICE_ARCHITECTURE_MENU_DEPTH.md)
- **#2 User & Operations Flows:** [USER_AND_OPERATIONS_FLOWS.md](../04_FLOWS/USER_AND_OPERATIONS_FLOWS.md)
- **#3 현재 문서:** Detailed Requirements & Business Policies
- **#4 Screen & Navigation / Traceability:** [SCREEN_NAVIGATION_TRACEABILITY.md](../08_SPECIFICATIONS/SCREEN_NAVIGATION_TRACEABILITY.md)
- **Package Guide:** [DEVELOPER_PACKAGE_GUIDE.md](../DEVELOPER_PACKAGE_GUIDE.md)

이 문서는 #2의 Flow를 실제 개발 가능한 Rule/Validation/Permission/State/Exception으로 해석한다. 화면 위치와 Navigation은 #4를 기준으로 하고, 기능 Ownership/메뉴 위치는 #1을 기준으로 한다.

---

## Workforce Service Desk Supplemental Rules — 2026-08-21

> 기존 확정 Rule은 변경하지 않는다. 아래는 최신 Owner Decision에 따른 Supplemental Rule이다.

### HR-WSD-R01 — Workforce Self-Service Scope

재직자·외부직원·퇴사자·해촉자는 본인에게 허용된 `accessible_scope` 내 HR 문서와 Employment/Engagement 관계 결과만 조회할 수 있다.

### HR-WSD-R02 — Offboarding Access Boundary

퇴사·해촉 Effective End 시 내부 OC/IAM Access는 회수한다. 기본 유예기간은 제공하지 않는다. 필요한 경우에만 사전승인된 만료형 Temporary Transition Access를 발급하며 최소권한·만료·승인자·사유·Audit를 필수로 한다.

### HR-WSD-R03 — Former / External Worker Identity Verification

OC 계정이 없는 외부직원·퇴사자·해촉자의 기본 본인확인은 `One-time Secure Link`로 한다. Public Entry에서 입력된 값으로 기존 Shared Person/Worker를 Match한 뒤 **기존 등록 휴대폰 또는 이메일로 시스템이 자동 발송**한다. 사용자가 입력한 신규 연락처로 즉시 발송하지 않는다.

### HR-WSD-R04 — Manual Verification Exception

Identity Match 실패, 등록 연락처 변경·소실, Legacy 정보 불완전, 반복 인증 실패는 `MANUAL_VERIFICATION_REQUIRED`로 격리한다. 직원 수동 재발송/대체인증은 이 예외에서만 허용하며 Audit를 남긴다.

### COMP-WSD-R01 — Compensation Self-Service

확정된 수당/Commission/지급예정·지급완료 결과와 Policy Snapshot 근거 중 본인에게 허용된 항목은 Self-Service 조회 대상으로 한다. 단순 조회에는 Request를 생성하지 않는다.

### COMP-WSD-R02 — Compensation Dispute / Correction

수당 산식·대상·금액에 대한 이견, 누락, 수정 요청이 있을 때만 `COMMISSION_INQUIRY` 또는 관련 Request를 생성하고 Compensation Owner Queue로 Routing한다. 과거 Finalized Compensation은 정책변경만으로 자동 재계산하지 않는다.

### FIN-WSD-R01 — Payroll / Settlement Self-Service

급여명세서, 확정 지급내역, 정산서 등 이미 발행·확정된 본인 자료는 Self-Service 조회/다운로드를 우선한다.

### FIN-WSD-R02 — Finance Request Routing

미정산, 지급오류, 정산 이의, 세무문서 신규발급/정정 등 담당자 처리가 필요한 경우에만 `PAYSLIP`, `SETTLEMENT_INQUIRY`, `TAX_DOCUMENT` 등의 Request를 생성하여 Finance Owner Queue로 Routing한다.

### FIN-WSD-R03 — Secure Result Delivery

급여·수당·정산·세무·HR 민감문서는 Public URL로 제공하지 않는다. 인증된 세션 또는 만료형 Signed/Secure Link로 전달한다. 장기 Public/CDN Cache를 금지한다.

### Unified Intake Workforce Extension

- Source Channel: `Workforce Service Desk Public Entry`
- Envelope Fields: `requester_type`, `identity_verified`, `accessible_scope`
- Request Types: `PAYSLIP`, `SETTLEMENT_INQUIRY`, `COMMISSION_INQUIRY`, `CERTIFICATE`, `TAX_DOCUMENT`, `CONTRACT_DOCUMENT`, `PERSONAL_INFO_CORRECTION`, `GENERAL_HR`

### Implementation / Config Boundary

- Secure Link TTL, 인증 Retry Count, Lockout 시간, Signed Download Link TTL은 Security Config 값이다.
- SMS/Email Provider, token persistence, Identity Provider binding은 Physical / Provider Pending이다.
- HR 법정 보관기간·파기정책, VAT·원천세·계정과목 등은 Legal / Finance Reference Value이며 본 Rule에서 임의 숫자로 고정하지 않는다.

---

## Workforce Service Desk — Supplemental Flow ↔ Rule Direct Trace

기존 C/O/S/P 29개 Canonical Trace Set은 유지한다. 아래 WSD Supplemental Flow는 별도 직접 Trace로 관리한다.

- `WSD-C-01` Internal Worker Self-Service → `HR-WSD-R01`, `COMP-WSD-R01`, `FIN-WSD-R01`, `FIN-WSD-R03`
- `WSD-C-02` External/Former Worker Public Entry + Request → `HR-WSD-R01~R04`, `FIN-WSD-R03` + COMMON Permission/Audit Guard
- `WSD-O-01` Workforce Request Operator Processing → `HR-WSD-R03~R04`, `COMP-WSD-R02`, `FIN-WSD-R02~R03`

Guard:

- 조회 가능한 확정 데이터는 Request를 생성하지 않는다.
- 담당자 처리가 필요한 경우에만 Unified Intake Request를 생성한다.
- Public Entry 본인확인은 기존 등록 연락처로 시스템이 자동 발송하는 One-time Secure Link를 기본으로 한다.
- Identity Match 실패·등록 연락처 변경은 Manual Verification Queue로 전환한다.
- Public Entry 사용자는 본인 Scope 밖의 Search/List/Export를 사용할 수 없다.

---

## Human Handoff Supplemental — Finance / Compensation Pending Reduction Closure — 2026-08-21

### Finance / Billing / Receivable

- `Charge ≠ Billing ≠ Payment ≠ Receivable ≠ Settlement`로 구분한다.
- Charge ↔ Billing은 1:1로 고정하지 않는다. 분할청구와 통합청구를 허용할 수 있도록 Logical 수준에서 N:M 가능성을 열어둔다.
- Receivable은 Settlement Substate가 아니라 별도 Logical Entity다.
- Receivable Candidate State: `OPEN → PARTIALLY_PAID → PAID/CLOSED`, 보조상태 `ON_HOLD / DISPUTED / WRITE_OFF_CANDIDATE / OVERDUE`.
- `OPEN` 상태에서 `due_at` 경과 + 미수잔액 > 0이면 시스템이 `OVERDUE`로 판정한다.
- Billing Issued ≠ Payment Received, Approved Expense ≠ Paid, Receivable ≠ Settlement.
- VAT / 원천세 / 계정과목 / 회계분개 / Bank Matching은 회계·세무·Physical Integration 범위로 유지한다.

### Compensation Finalization Trigger

`Performance → Eligibility → Policy Snapshot → Calculation → Review → Approval → Finalization → Payment/Settlement`

- 필수 Approval이 모두 완료되고 추가 Review/Hold 조건이 없으면 Compensation Record는 `Finalized`로 전환된다.
- 별도 수동 Finalization이 필요한 예외 항목은 Approval Policy Configuration에서 명시적으로 설정해야 하며 코드 분기로 숨기지 않는다.
- 과거 Finalized Compensation은 정책 변경만으로 자동 재계산하지 않는다. 수정은 Adjustment/Clawback Record로 남긴다.

본 Supplemental은 기존 Rule ID를 임의 재번호하지 않고 Pending Reduction에서 이미 확정된 Human Handoff Guard를 개발자가 직접 읽을 수 있도록 보강한다.

---

## Human Handoff Cross-Audit Round 1 Corrections — 2026-08-21

Claude PM3 독립 Cross-Audit REVISE-B02 및 WSD Permission/Manual Verification 보강 반영.

### O-11 Compensation Trace Extension

O-11 수당·인센티브 구현 시 기존 `COMP-R01~R06`, `POLICY-R01~R04`와 함께 `COMP-WSD-R02`의 Dispute / Correction / No Retroactive Recalculation Guard를 적용한다.

Logical sequence:

`Performance Confirmed → Eligible Event → Policy Snapshot → Calculation Candidate → Review → Approval → Finalized Compensation → Payment / Settlement Link`

### WSD accessible_scope Policy

- 기본값은 Self-only.
- 내부 전일제/제한형/외부 Worker 모두 타인 급여·수당·정산·HR 문서 조회 금지.
- Role별 허용 Data Category / Request Type / Document Type은 IAM/Permission Config로 관리한다.
- 제한형 계정은 Config에 명시된 범위만 허용한다.
- Config 미확정 시 Default Deny를 적용하고 개발자가 임의 확대하지 않는다.

### Manual Verification Policy

- `MANUAL_VERIFICATION_REQUIRED`는 Identity 우회용 상태가 아니다.
- Authorized Operator가 승인된 Evidence로 본인 Match를 검토한다.
- 성공 시 최소 accessible_scope만 부여하고 정상 WSD 흐름으로 복귀한다.
- 실패 시 민감정보/문서 접근 없이 종료 또는 추가 검증 Queue로 전환한다.
- Verification Actor / Evidence / Result / Scope / Timestamp Audit 필수.
- 정확한 Evidence 종류, Retry Count, Lockout 시간은 Security Operations Config Pending.

Verdict: REVISE-B02 + WSD Developer Question Risk CLOSED AT LOGICAL/HUMAN-HANDOFF LEVEL.

---

## Human Handoff Final Guard — Required / Optional Contract Item Classification — 2026-08-21

`FULFILL-R06`의 `Required/Core Item 완료 시 비핵심 Item 보류 중이어도 Store Activation 허용` 원칙을 구현할 때 개발자가 Required/Optional 여부를 임의 판단하지 않는다.

- Required / Optional 분류 Source: **Contract Item Type 또는 Product Fulfillment Template의 명시적 Configuration**
- 해당 Configuration이 존재하면 그 값을 Activation Guard가 사용한다.
- Required / Optional 분류가 누락·미설정된 Item은 자동으로 Required 또는 Optional로 추정하지 않는다.
- 미설정 상태에서는 `CONFIGURATION_ERROR` 또는 `ACTIVATION_REVIEW_REQUIRED`로 격리하고 **자동 Store Activation을 금지**한다.
- 운영자가 승인된 Template/Policy Configuration을 보완한 뒤 Guard를 재평가한다.
- 이 규칙은 Product별 실제 Required Item 목록을 코드에 하드코딩하라는 의미가 아니다.

**Verdict:** GAP-5A CLOSED AT LOGICAL / HUMAN-HANDOFF LEVEL. Product별 실제 분류값은 Versioned Template / Business Policy Config 입력값이다.

---

## Intake Note — 2026-08-21 (Final SOT Resync)

- 본 문서는 Notion Developer Package Document #3의 **Final SOT Freeze 판본**을 GitHub에 Resync한 것이다. 직전 입고본(중간 Snapshot)은 커밋 `9e1ae35`로 보존된다.
- Resync 반영분: `FINAL SOT FREEZE` 블록 · §1.1 People/HR·Company Operations·Workforce Service Desk 범위 추가 · §1.2 FLOW-007 문구 갱신 · §3.0A Latest Supplemental Capability Areas · Workforce Service Desk Supplemental Rules (`HR-WSD-R01~R04`, `COMP-WSD-R01~R02`, `FIN-WSD-R01~R03`) · WSD Flow↔Rule Direct Trace · Finance/Receivable Closure · O-11 Compensation Trace Extension · WSD accessible_scope / Manual Verification Policy · Required/Optional Activation Guard.
- 기존 `[CONTEXT]-R[NN]` Rule ID는 **재번호하지 않았다.** 원문의 절 번호 건너뜀(15 → 18)도 그대로 보존했다.
- 기존 `PP-OC-REQS-001`은 SUPERSEDED 상태를 유지하며 본문은 계속 보존된다.
- Header Status는 Notion 원문을 유지했고 `APPROVED` / `Source of Truth YES`로 승격하지 않았다.
- Pending 값은 임의 확정하지 않았다.
