# User & Operations Flows — PayPlay OC

| 항목 | 내용 |
|------|------|
| Document ID | PP-OC-FLOWS-001 |
| Product / Service | PayPlay OC |
| Document Type | User & Operations Flow |
| Status | SUPERSEDED |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-15 |
| Source of Truth | NO (SUPERSEDED — 2026-08-21) |
| Development Use | Flow 기준선. Development Ready / QA Ready 선언문서 아님. |
| Notion Source | https://app.notion.com/p/3bc53327fb868183bc28ce151442cebf |
| Related Decision | DECISION_REGISTER.md |
| Supersedes | — |
| Superseded by | PP-OC-USER-OPS-FLOW-001 — [10_OC/04_FLOWS/USER_AND_OPERATIONS_FLOWS.md](./USER_AND_OPERATIONS_FLOWS.md) |
| Superseded date | 2026-08-21 |
| Supersede Note | Claude PM3 지시(2026-08-21)에 따른 Header 표기 변경. **본문 내용은 삭제·수정하지 않았다.** 기존 Flow/정책 서술과 식별자는 이력 추적용으로 계속 유효하다. |

> ✅ PayPlay OC의 최종 User & Operations Flow 통합문서.
> Main PM의 Shared Entity 검수 결과를 반영했으며, 승인된 구조와 Pending을 명확히 구분한다.
> 본 문서는 업무흐름 기준 Final Documentation Candidate이며, Development Ready / QA Ready 선언문서는 아니다.


> ⚠️ **SUPERSEDED — 2026-08-21.** 이 문서는 `PP-OC-USER-OPS-FLOW-001` ([10_OC/04_FLOWS/USER_AND_OPERATIONS_FLOWS.md](./USER_AND_OPERATIONS_FLOWS.md))로 승계되었다.
> 신규 개발 기준으로 사용하지 말 것. 본 문서는 이력 보존 및 기존 식별자 추적용으로 유지된다.

---

## 1. Document Scope

본 문서는 PayPlay OC의 실제 업무 흐름을 `사용자/운영자 Actor → Trigger → 업무 단계 → State/Decision → Handoff → 기록/감사` 구조로 통합한다.

대상 범위:

- OSP Lead Handoff 이후 영업 실행
- Customer 360 / Customer Account / Store 운영
- Quote / Approval / Contract
- Fulfillment / Installation / Activation
- Inventory / Purchase / Shipment
- Customer Request / CS / AS / Case
- Cost / Settlement / Expense
- Sales Commission / Incentive
- Management Decision
- Existing/New Customer Opportunity
- Multi Contract Item Fulfillment
- Commercial Policy Snapshot
- Contextual Team Chat / AI Operations Assistant
- Today / Queue / Dashboard 운영 Projection

---

## 2. Shared Entity Decision Applied

### Decision

- **Customer Account** = 동일 실질 운영관계로 PayPlay가 통합 관리하는 고객그룹.
- **Store** = 실제 서비스·설치·운영·AS가 발생하는 사업장 단위.
- **Store 양도양수** = 동일 장소·운영 연속성 유지 시 기존 Store ID 유지 후보, 타지역 이전은 신규 Store 우선, 애매하면 Human Review.
- **Legal Entity** = Store에 단일 고정값으로 두지 않고 역할·기간별 Assignment History로 관리.
- **Product / Commercial Policy** = OC Master Owner.

### External Dependency / Pending

- Person Master 물리 위치
- Merchant Account 최종 구조
- Shared IAM 물리 Architecture

이 3개는 본 Flow에서 논리 Reference만 사용하며 물리 DB/Table/Repository를 확정하지 않는다.

---

## 3. Actor Model

### Internal

- Executive / Owner
- Operations Admin
- Team Lead
- Internal Sales
- CS
- Internal Field / Installation
- Inventory / Supply
- Finance / Settlement
- Product / Commercial Policy Manager
- Approval Authority

### External

- External Sales
- External Technician
- Vendor / Partner

### Customer-side

- 실질 운영자
- 법적 대표자
- 직원 / 배우자 / 자녀 / 회계·현장 담당자 등 Contact

Customer-side Person은 논리 관계로 취급하며 Person Master의 물리 Owner는 Pending이다.

---

## 4. End-to-End Backbone

```
OSP Lead / Existing Customer Request
→ Customer Account / Store Match
→ Opportunity / Request
→ Sales Assignment
→ Consultation / Visit
→ Quote Revision
→ Margin / Policy Review
→ Approval when required
→ Contract
→ Contract Item
→ Fulfillment / Inventory / Shipment / Installation
→ Store Activation / Service Use
→ CS / Case / AS / Change / Additional Purchase
→ Cost / Settlement / Commission
→ Activity / Audit / Dashboard / Management Review
```

---

## 5. OC-FLOW-001 — OSP Lead → 영업 실행 → 계약 전환

**Trigger:** OSP에서 상담신청/Lead 생성 또는 외부 채널에서 신규 영업기회가 유입됨.

**Actors:** OSP System, 영업 관리자, 내부/외부 영업 담당자, 계약 관리자.

**Flow:**

1. OSP는 Lead와 유입 Source를 OC에 Handoff한다.
2. OC는 Customer Account / Store 중복 후보를 검색한다.
3. 기존 고객이면 해당 Customer Account/Store에 Opportunity를 연결하고, 신규이면 Customer/Store Candidate를 생성한다.
4. 담당자 배정 및 1차 상담 Queue에 진입한다.
5. 통화·메시지·방문 등 Touch를 Activity로 기록한다.
6. 방문 필요 시 방문 Queue로 전환하고 담당자를 배정한다.
7. 고객 요구사항·상품·예산·설치조건을 정리한다.
8. Quote가 필요하면 OC-FLOW-002로 Handoff한다.
9. 고객 거절/보류/취소 시 사유와 다음 Follow-up을 기록한다.
10. 계약 합의 시 Contract Flow로 전환한다.

**Guard:** OSP는 Lead 생성/유입 Source Owner이며 사람 상담·계약 실행 State의 Owner가 아니다.

---

## 6. OC-FLOW-002 — 견적 작성 → 원가/마진 검토 → 승인 → 계약

**Trigger:** Opportunity에서 가격/구성/계약조건 제안이 필요함.

**Actors:** 영업 담당자, Product/Commercial Policy 담당자, 승인자, 계약 관리자.

**Flow:**

1. 승인된 Product / Commercial Policy Version을 불러온다.
2. 상품·수량·기간·설치비·PG/요금·할인·프로모션 후보를 구성한다.
3. Quote Revision을 생성한다.
4. Cost/Margin/Commission Restricted 정보는 권한 있는 사용자만 조회한다.
5. 기준정책 밖의 할인·마진·수당·계약조건은 Approval Request를 생성한다.
6. 승인/반려/수정요청 결과를 Quote Revision과 Activity/Audit에 연결한다.
7. 발송된 Quote Revision은 불변 이력으로 유지한다.
8. 고객 수락 시 Accepted Revision을 Contract Source로 승계한다.

**Guard:** 이후 Commercial Policy 변경으로 과거 발송 Quote의 금액/조건을 소급 변경하지 않는다.

---

## 7. OC-FLOW-003 — 계약 완료 → 설치 대상 생성 → 설치 완료

**Trigger:** Contract Signed 또는 설치 가능한 계약 Item 확정.

**Actors:** 계약 관리자, 설치 관리자, CS, Field Team, 외부 기사.

**Flow:**

1. Contract Header와 Contract Item을 분리 확인한다.
2. 각 Item별 Fulfillment Requirement를 생성한다.
3. 설치 주소·일정·연락 대상·필요서류·장비·재고·Vendor 의존성을 확인한다.
4. 재고 부족 시 OC-FLOW-004로 Handoff한다.
5. 설치 일정과 담당자를 배정한다.
6. 현장 설치·설정·검증·고객확인을 수행한다.
7. 장비/Serial/Service Instance를 Store와 Contract Item에 연결한다.
8. 설치 결과·사진·예외·재방문 필요사항을 기록한다.
9. Item별 Fulfillment Complete를 판단한다.
10. 모든 필수 Item이 완료되어야 Store Activation/계약 이행완료 Projection을 갱신한다.

**Guard:** Contract Signed와 Installation Complete는 서로 다른 State다.

---

## 8. OC-FLOW-004 — 재고/발주/배송 → 설치·AS 공급

**Trigger:** 설치, 교체, AS, 신규 구매로 자재/장비가 필요함.

**Actors:** 재고 담당자, 구매 담당자, 물류 담당자, Vendor, 설치/CS 담당자.

**Flow:**

1. Contract Item/Case에서 Material Requirement를 생성한다.
2. 현재 Inventory Availability를 확인한다.
3. 재고가 있으면 Reservation/Allocation한다.
4. 부족하면 Purchase/PO Candidate를 생성하고 승인 필요 여부를 확인한다.
5. Vendor 입고/직배송/창고출고를 구분한다.
6. Shipment/Transfer를 생성하고 운송장·수령 상태를 추적한다.
7. 설치/AS에서 실제 사용량·Serial을 확정한다.
8. 미사용/회수/불량품은 Return/Repair/Disposal Flow로 보낸다.
9. 모든 수량 변경은 Inventory Transaction으로 기록하고 Balance는 Projection으로 계산한다.

**Guard:** 수량 Inventory와 개별 Asset/Serial을 분리한다.

---

## 9. OC-FLOW-005 — 문의/장애 → 원격지원 → AS/현장복구

**Trigger:** 고객 문의, 장애, 변경요청, 장비/프로그램 문제 발생.

**Actors:** CS, Field Team, 외부 기사, Vendor, 고객 Contact.

**Flow:**

1. Customer Account / Store를 검색해 요청을 연결한다.
2. 문의 유형·심각도·서비스 영향·계약/보증 범위를 확인한다.
3. 단순 안내는 Activity로 처리하고 종료할 수 있다.
4. 추적이 필요한 요청은 Case를 생성한다.
5. 원격 해결 가능하면 Remote Support Work Item을 수행한다.
6. 해결되지 않으면 현장방문/제조사/Vendor Work Item을 생성한다.
7. 담당자·일정·필요 장비/자재를 배정한다.
8. 고객 과실/유상 AS 가능성이 있으면 승인된 CS/AS Policy를 적용한다.
9. 해결 결과와 Root Cause/재발방지 정보를 기록한다.
10. 모든 필수 Work Item 완료 후 Case를 Resolution/Close한다.

**Guard:** Case Close와 개별 Work Item Complete를 구분한다.

---

## 10. OC-FLOW-006 — 비용 발생 → 정산/지출 검토 → 확정

**Trigger:** 계약·설치·구매·배송·AS·일반 운영에서 비용/정산 Event 발생.

**Actors:** 업무 담당자, 재무 담당자, 승인자, 경영진.

**Flow:**

1. 비용 Source Entity와 증빙을 연결한다.
2. 비용유형·금액·귀속 Customer/Store/Contract/Case/Vendor를 확인한다.
3. Budget/Policy/Approval Threshold를 검증한다.
4. 필요 시 Approval을 진행한다.
5. 승인 후 Settlement/Expense 상태를 확정한다.
6. 수정/취소는 원 Record를 지우지 않고 Adjustment/Correction 이력을 남긴다.
7. Restricted Finance 정보는 최소권한으로 제한한다.

---

## 11. OC-FLOW-007 — 실적 확정 → 수수료/인센티브 계산 → 승인

**Trigger:** 계약·설치·매출 등 Commission 기준 Event가 확정됨.

**Actors:** Sales/Operations, Compensation 담당자, 승인자, Finance.

**Flow:**

1. Commission Eligibility Event를 식별한다.
2. 판매 당시 Commercial Policy Version과 Channel/Role/DB Source를 확인한다.
3. Fixed/Percent/Per-unit/Revenue Share Rule로 계산한다.
4. 예외·취소·환수·DB 차감 조건을 반영한다.
5. 계산 근거와 Applied Policy Snapshot을 저장한다.
6. 승인 후 지급/정산 대상이 된다.
7. 사후 Policy 변경으로 과거 수당을 자동 재계산하지 않는다.

**Pending:** Compensation의 세부 계산·승인 정책은 기존 Decision Queue와 연결한다.

---

## 12. OC-FLOW-008 — 경영 Decision 기록 → 실행 → 결과 → Review

**Trigger:** 주요 운영·재무·인사·상품·정책 의사결정 필요.

**Actors:** 경영진, 팀장, 관련 Domain 담당자.

**Flow:**

1. Decision Context와 Source Evidence를 모은다.
2. 선택지·이유·기대효과·Risk를 기록한다.
3. 승인/결정 후 실행 Task/Work Item을 연결한다.
4. 일정 기간 후 실제 결과를 기록한다.
5. 예상 대비 차이를 Review한다.
6. Decision 변경은 기존 기록 삭제보다 Revision/Supersede를 사용한다.

**Guard:** Restricted Management/Finance/HR 정보는 권한·Audit 적용.

---

## 13. OC-FLOW-009 — Existing/New Customer → Opportunity/Request → Quote → Contract

**Trigger:** 기존 고객의 추가구매/변경/재문의 또는 신규 고객의 영업기회.

**Flow:**

1. Customer Account/Store 중복을 확인한다.
2. 기존이면 Customer 360에 연결하고 신규면 Candidate를 생성한다.
3. 요청 목적을 Opportunity/Request로 등록한다.
4. 기존 Contract/Asset/Case History를 조회한다.
5. 추가구매·교체·재계약·신규설치 여부를 판정한다.
6. Quote/Approval/Contract Flow를 재사용한다.

**원칙:** 신규/기존 고객을 별도 업무체계로 분리하지 않고 동일 Opportunity Backbone을 재사용한다.

---

## 14. OC-FLOW-010 — Contract → Multi Contract Item → Team Fulfillment → Store Activation

**Trigger:** 한 계약에 POS·테이블오더·인터넷·CCTV·단말기·서비스 등 복수 Item이 포함됨.

**Flow:**

1. Contract를 Item 단위로 분해한다.
2. 각 Item에 담당 Domain/팀을 할당한다.
3. 공통 선행조건과 Item별 선행조건을 구분한다.
4. 병렬 가능한 작업은 동시에 진행한다.
5. 하나의 Item 지연이 전체 Contract State를 잘못 왜곡하지 않도록 Item Fulfillment State를 별도 관리한다.
6. 모든 필수 Item의 완료조건을 충족하면 Store Activation/완료 상태를 갱신한다.

---

## 15. OC-FLOW-011 — Customer Request / AS → Case → Escalation → Resolution

**Trigger:** 고객요청이 단순 Activity를 넘어 추적·책임·SLA가 필요한 경우.

**Flow:**

1. Customer 360 또는 외부 채널 요청을 Customer Account/Store에 매칭한다.
2. Case를 생성하고 유형/Severity/Priority를 지정한다.
3. 담당 Queue/Owner를 할당한다.
4. Work Item으로 분해한다.
5. 일정/장비/Vendor/Approval 의존성을 연결한다.
6. SLA 위험·반복장애·고객 불만 등은 Escalation한다.
7. 최종 해결·고객확인·후속조치 후 Case를 종료한다.

---

## 16. OC-FLOW-012 — Policy → Quote / CS Charge / Commission / Contract Snapshot

**Trigger:** 가격·수수료·PG·Revenue Share·CS요금·계약조건이 업무에 적용됨.

**Flow:**

1. OC의 승인된 Effective Policy Version을 선택한다.
2. 조건을 평가해 적용 Rule을 결정한다.
3. 계산된 값과 Rule 근거를 Snapshot한다.
4. Quote/Contract/CS Charge/Commission에 Snapshot ID와 resolved value를 연결한다.
5. Policy가 이후 변경되어도 과거 적용값은 유지한다.
6. 오류 Formula/WIP Policy는 Effective로 사용하지 않는다.

---

## 17. OC-FLOW-013 — Contextual Team Chat + AI Operations Assistant

**Trigger:** 특정 Customer/Store/Contract/Case/Work Item을 중심으로 협업·AI 지원이 필요함.

**Actors:** 권한 있는 내부/외부 사용자, AI Assistant.

**Flow:**

1. 현재 업무 Context를 기준으로 Conversation을 연다.
2. 팀원이 메모·질문·파일·결정사항을 공유한다.
3. AI는 허용된 Source만 조회해 요약·검색·다음 Action·초안·Risk를 제안한다.
4. 상태/금액/승인/계약조건 변경이 필요하면 AI는 Command를 준비할 수 있다.
5. Human Confirm 또는 Approval 후 Domain Service가 실제 변경을 Commit한다.
6. Commit 결과는 Activity/Audit에 남긴다.

**Guard:** AI 답변 자체는 Business State 변경이 아니다. Secret/Restricted Field는 AI Access Policy를 따른다.

---

## 18. Customer 360 Operational Flow

Customer 360은 Master Table이 아니라 Projection이다.

조회 단위:

- Customer Account Summary
- Store별 현재 상태
- 주요 Contact Relationship
- Opportunity / Quote / Contract
- 설치·Asset·Service
- Case / AS
- Payment/Settlement 관련 허용 Summary
- Activity Timeline
- 빠른 Action: 전화/메시지/상담/견적/계약/Case/방문/메모

한 Customer Account 아래 여러 Store가 있을 수 있고, Store별 법적 명의·계약·PG·정산 관계는 분리해 표시한다.

---

## 19. Legal Entity / Transfer Flow

### 동일 장소 양도양수

1. Store Continuity Evidence 확인.
2. 기존 Store ID 유지 Candidate.
3. 이전 Legal Entity Assignment 종료일 기록.
4. 신규 BUSINESS_REGISTRATION_HOLDER / CONTRACTING_PARTY / PG_MERCHANT_PARTY / SETTLEMENT_PARTY Assignment 생성.
5. 이전 Contract/채권/정산을 신규 주체에 병합하지 않는다.

### 타지역 이전

신규 Store Candidate가 기본이며 기존 Store는 종료/이전 History를 보존한다.

### Ambiguous

자동 Merge/Transfer 금지, Human Review Queue로 보낸다.

---

## 20. Work Queue / Today / Dashboard

### Work Queue

실제 처리해야 하는 Work Item/Case/Approval/Follow-up/Installation/Shipment를 담당자 기준으로 보여준다.

### Today

오늘 필요한 업무를 Priority/SLA/약속시간/Blocker 기준으로 집계하는 Projection이다.

### Dashboard

영업·계약·설치·AS·재고·정산·수당·운영 KPI를 Source Entity에서 집계한다.

**원칙:** Queue/Today/Dashboard는 Source of Truth가 아니며, Projection에서 직접 임의 State를 만들지 않는다.

---

## 21. Handoff Rules

- OSP → OC: Lead/Source/Request Handoff.
- Sales → Contract: Accepted Quote / Required Documents / Customer·Store Context.
- Contract → Fulfillment: Contract Item / Schedule / Material Requirement.
- Fulfillment → CS/Business OS: Installed Asset / Service Activation / Support Context.
- CS → Sales: 추가구매/교체/재계약 Opportunity Candidate.
- Inventory → Fulfillment: Reserved/Shipment/Serial.
- Approval → Source Domain: 승인 결과만 반영, Approval이 Source Entity를 대체하지 않음.

---

## 22. Cross-cutting Business Flow Rules

1. Business State와 Workflow State를 분리한다.
2. 모든 중요한 상태·금액·승인 변경은 Activity/Audit를 남긴다.
3. Quote/Contract/Commission에는 적용 당시 Commercial Policy Snapshot을 보존한다.
4. Customer Account는 법적 계약주체가 아니다.
5. Store와 Legal Entity 관계는 역할·기간 History를 가진다.
6. Person은 논리 Reference만 사용하며 물리 Master 위치는 Pending이다.
7. Merchant Account 최종 Entity 구조를 본 문서에서 확정하지 않는다.
8. Shared IAM 물리 구조를 본 문서에서 확정하지 않는다.
9. 외부 영업/설치/Vendor는 Assigned Scope 중심 최소권한을 적용한다.
10. AI는 Suggest/Prepare까지 가능하며 중요 Commit은 Human Confirm/Approval을 거친다.

---

## 23. Exception / Recovery Principles

- 취소/철회/반려는 삭제가 아니라 State/Event로 보존.
- 재계약/추가구매는 기존 Contract 덮어쓰기보다 새 Opportunity/Contract/Revision을 사용.
- 잘못된 Identity Merge는 Correction/Merge Event와 Legacy Trace를 유지.
- 설치 실패/재방문은 Contract 자체 실패로 단순 치환하지 않고 Work Item/Item Fulfillment 상태로 관리.
- Policy 오류는 과거 Sheet Formula를 억지 복원하지 않고 검증된 신규 Version으로 전환.

---

## 24. External Dependency / Pending Register

### PENDING-EXT-001 Person Master Physical Location

논리 Person/Contact Relationship은 필요하나 물리 DB/Owner는 Common Infrastructure 검토 후 결정.

### PENDING-EXT-002 Merchant Account Final Structure

Customer Account/Store/User Identity와 분리 필요성은 인정되지만 최종 Merchant Account/Membership/Store Access 구조는 Business OS/Common Infrastructure 검토 후 결정.

### PENDING-EXT-003 Shared IAM Physical Architecture

OC Domain Permission 요구사항은 유지하되 인증·Session·User Identity·Cross-Product Membership 물리 Architecture는 Common Infrastructure가 결정.

---

## 25. Final Gate Judgment

**PASS — FINAL FLOW DOCUMENT COMPLETE WITH 3 EXTERNAL STRUCTURAL PENDINGS**

본 문서는 Main PM 판정에 맞춰 OC의 최종 User & Operations Flow 기준선으로 사용할 수 있다.

---

→ 관련 문서: [detailed-requirements-and-business-policies.md](../05_REQUIREMENTS_POLICIES/detailed-requirements-and-business-policies.md)
→ Audit: [OC_TRACEABILITY_GAP_AUDIT_v1.md](../10_AUDIT/OC_TRACEABILITY_GAP_AUDIT_v1.md)
