# PayPlay OC — Developer Package 4문서 이해 가이드

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/DEVELOPER_PACKAGE_GUIDE.md` |
| Document ID | PP-OC-DEV-PACKAGE-GUIDE-001 |
| Version | v1.0 |
| Status | GUIDE / EXPLANATORY — 구현 기준 문서 아님 |
| Source of Truth | NO — 설명용 Navigation Guide. 실제 구현 기준은 각 원문 문서를 따른다. |
| Owner | PayPlay OC |
| Last Reviewed | 2026-08-21 |
| Development Use | Developer Package 4문서의 역할·읽기순서 안내 전용. |
| Notion Source | https://app.notion.com/p/3c053327fb86813eb1fbd595d9fa60a9 |
| Final Pending Register | [FINAL_PENDING_REGISTER.md](./09_DECISIONS/FINAL_PENDING_REGISTER.md) |

> ✅ **Main PM Final Gate — 2026-08-21: PASS.** Developer Readable **YES** / Development Startable **YES** / Major OC Flow Implementable **YES** / Package-wide Scope-Blocking Pending **0** / QA Ready **NOT YET**. Pending-dependent Production Finalization은 Final Pending Register의 해당 항목 해소 전 금지한다.

**Final Pending Register:** [OC Final Pending Register — Developer Package v1.0](./09_DECISIONS/FINAL_PENDING_REGISTER.md)

**Cross-Audit:** GPT ↔ Claude unresolved difference **0** / Development Blocker **0**.

> ✅ **Developer Package Official Reading Order — 2026-08-21:** `#1 Service Architecture / Menu & Depth → #2 User & Operations Flows → #3 Detailed Requirements & Business Policies → #4 Screen & Navigation / Traceability`. 아래 링크가 현재 Finalization 기준 공식 4문서다.

1. [#1 Service Architecture / Menu & Depth — Final Candidate v1.0](./07_ARCHITECTURE/SERVICE_ARCHITECTURE_MENU_DEPTH.md)
2. [#2 User & Operations Flows — v5.2 CLEAN / CROSS-SYNC](./04_FLOWS/USER_AND_OPERATIONS_FLOWS.md)
3. [#3 Detailed Requirements & Business Policies — v4.1 CLEAN / AUDITED](./05_REQUIREMENTS_POLICIES/DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md)
4. [#4 Screen & Navigation / Traceability — Final Candidate v1.0](./08_SPECIFICATIONS/SCREEN_NAVIGATION_TRACEABILITY.md)

**Reading Rule:** #1에서 기능 위치/Ownership을 먼저 확인하고 → #2에서 Actor·목적·상태변화·Handoff를 이해하고 → #3에서 Rule·Validation·Permission·Exception을 확인한 뒤 → #4에서 실제 Screen/Navigation 구현 위치를 확정한다. 역순으로 읽어 Screen을 기준으로 업무 의미를 재정의하지 않는다.

> 📦 이 페이지는 성재님과 개발자가 OC 개발문서 4종의 역할을 한눈에 이해하기 위한 설명용 패키지다. 실제 구현 기준은 각 원문 문서를 따른다.

---

## 1. 이 패키지의 목적

OC 개발 시 필요한 정보를 **구조 → 흐름 → 규칙 → 화면** 순서로 이해하도록 4개 문서를 묶는다.

- **1번:** 서비스가 어떻게 나뉘는가
- **2번:** 사용자가 어떻게 움직이는가
- **3번:** 각 기능이 어떤 규칙으로 동작하는가
- **4번:** 실제 어느 화면에서 구현되는가

> 이 4개 문서가 모두 완성되고 서로 Traceability가 연결되어 있으면 **기능 개발 착수에는 충분한 핵심 패키지**가 된다. 다만 실제 배포·운영 완료까지는 Physical API/DB/IAM/외부 Provider, 환경설정, 테스트·배포 항목 중 Pending인 부분이 별도로 해소되어야 한다.

<details>
<summary><b>1. Service Architecture / Menu &amp; Depth — 서비스 구조·메뉴·뎁스</b></summary>

### 이 문서가 답하는 질문

**"OC에는 어떤 카테고리가 있고, 메뉴가 몇 단계로 나뉘며, 어떤 기능이 어디에 속하는가?"**

### 왜 필요한가

User Flow만 보면 업무 순서는 이해할 수 있지만 전체 제품의 구조를 한눈에 보기 어렵다. 이 문서는 개발자가 처음 OC를 열었을 때 **제품 지도** 역할을 한다.

### OC 샘플

```text
OC
├─ Today
│  ├─ My Queue
│  ├─ Team Queue
│  └─ Alerts
├─ Sales
│  ├─ Lead / Request
│  ├─ Opportunity
│  │  ├─ 상담
│  │  ├─ 방문
│  │  └─ Activity
│  └─ Customer / Store
├─ Quote
│  ├─ Quote List
│  ├─ Quote Detail
│  ├─ Revision
│  └─ Approval
├─ Contract
│  ├─ Contract List
│  ├─ Contract Detail
│  ├─ Contract Item
│  ├─ 변경
│  ├─ 양도양수
│  └─ 해지
├─ Fulfillment
│  ├─ Readiness
│  ├─ Schedule
│  ├─ Work
│  ├─ Evidence
│  └─ Verification
├─ Inventory
│  ├─ Stock
│  ├─ Reservation
│  ├─ Purchase
│  ├─ Shipment
│  ├─ Return
│  └─ Asset / Serial
├─ CS / AS
│  ├─ Case
│  ├─ Work
│  ├─ Escalation
│  ├─ Vendor Handoff
│  └─ Resolution
├─ Finance
│  ├─ Expense
│  ├─ Approval
│  └─ Settlement
├─ Compensation
│  ├─ Eligibility
│  ├─ Calculation
│  ├─ Approval
│  └─ Adjustment
└─ Management
   ├─ Decision
   ├─ Execution
   └─ Review
```

### 개발자가 여기서 읽는 것

- 1Depth / 2Depth / 3Depth
- 메뉴 소속
- 기능 그룹
- 화면이 어느 Domain에 속하는지
- 같은 기능이 여러 메뉴에 중복되지 않는지

### 다른 문서와의 연결

각 메뉴/기능은 반드시 `Flow ID`, `Screen ID`, `Rule ID`와 연결한다.

### 권장 표

| 1Depth | 2Depth | 3Depth/기능 | 주요 사용자 | Flow ID | Screen ID | Rule ID | 상태 |
|---|---|---|---|---|---|---|---|
| Sales | Opportunity | 상담 | 영업 담당자 | O-03 | OC-OPP-002 | SALES-Rxx | 포함 |
| Contract | Contract Detail | 계약 변경 | 계약 관리자 | Pending Review | OC-CONTRACT-002 | CONTRACT-Rxx | 검토 필요 |

</details>

<details>
<summary><b>2. User &amp; Operations Flows — 사용자 및 운영 흐름</b></summary>

### 이 문서가 답하는 질문

**"누가 무엇을 달성하기 위해 어디서 시작하고, 어떤 행동을 하고, 성공·실패 시 어떻게 끝나는가?"**

### 현재 OC 원문

[User & Operations Flows — v5.2 CLEAN / CROSS-SYNC](https://app.notion.com/p/3bf53327fb868164bb03d968f010ea1f)

### OC 샘플 — C-02 견적 확인·수정·수락

**사용자:** 고객
**목적:** 받은 견적을 확인하고 수락·수정요청·거절 중 하나를 선택한다.
**시작점:** 견적 링크 / 영업 안내
**완료 상태:** Accepted / Negotiating / Rejected

**정상 경로 예시**

1. 고객이 견적 링크를 연다.
2. 상품·수량·금액·조건을 확인한다.
3. 고객이 수락 또는 수정요청을 선택한다.
4. 시스템은 현재 Quote Revision이 유효한지 확인한다.
5. 수락 시 Accepted Revision으로 기록하고 계약 Flow로 Handoff한다.

**예외 예시**

- 만료된 견적 → 최신 Revision 안내
- 발송 실패 → Sent로 처리하지 않고 재시도
- 수정 요청 → 기존 Sent Revision 직접 수정 금지, New Revision 생성

### 개발자가 여기서 읽는 것

- Actor
- 시작 조건
- 입력/선택 순서
- Action
- 정상 경로
- Alternative
- Error/Recovery
- 상태 변화
- 다음 Handoff

### 핵심

이 문서는 **화면 목록이 아니다.**
`화면 A → 화면 B`보다 **사용자 목적과 업무 상태 변화**가 중심이다.

</details>

<details>
<summary><b>3. Detailed Requirements &amp; Business Policies — 상세 요구사항 및 비즈니스 정책</b></summary>

### 이 문서가 답하는 질문

**"그 Flow가 어떤 입력값·권한·Validation·Business Rule·State로 실제 동작하는가?"**

### 현재 OC 원문

[Detailed Requirements & Business Policies — v4.1 CLEAN / AUDITED](https://app.notion.com/p/3bf53327fb8681ba8a9dceb9dd71652c)

### OC 샘플 — 견적 Rule

- Sent 상태의 Quote Revision은 직접 덮어쓰지 않는다.
- 고객 수정 요청 시 New Revision을 생성한다.
- Required Field가 누락되면 Send Command를 차단한다.
- Approval Pending이면 발송할 수 없다.
- 외부 발송 Provider가 timeout/unknown이면 Sent 성공으로 확정하지 않는다.

### 개발자가 여기서 읽는 것

- Required / Optional / Conditional
- Validation
- Permission
- Approval
- Guard
- State Transition
- Error/Recovery
- Notification
- External Integration
- Acceptance Criteria
- Pending / Decision

### 샘플 표

| Rule ID | 조건 | Action | 성공 결과 | 실패/복구 | Permission |
|---|---|---|---|---|---|
| QUOTE-R01 | Revision = Sent | 수정 요청 | New Revision 생성 | 기존 Revision 보존 | 영업 담당자 |
| QUOTE-R02 | Required 누락 | Send 클릭 | N/A | Send 차단 + 누락 표시 | 영업 담당자 |

### 핵심

User Flow가 **이야기**라면 이 문서는 **개발 규칙**이다.

</details>

<details>
<summary><b>4. Screen &amp; Navigation / Traceability — 화면·네비게이션·추적성</b></summary>

### 이 문서가 답하는 질문

**"이 Flow와 Rule을 실제 어느 화면에서 구현하고, 사용자는 어디로 이동하는가?"**

### 역할

Service Tree가 전체 제품 구조를 보여준다면 이 문서는 **화면 단위 구현 지도**다.

### OC 샘플

| Screen ID | 화면명 | Menu | 주요 Flow | 주요 Action | Rule | 다음 화면/상태 |
|---|---|---|---|---|---|---|
| OC-OPP-002 | Opportunity Detail | Sales > Opportunity | O-02, O-03 | 담당자배정, 상담기록 | SALES-Rxx | Quote Ready |
| OC-QUOTE-003 | Quote Editor | Quote | O-04 | 저장, 승인요청, 발송 | QUOTE-Rxx | Sent/Accepted |
| OC-CONTRACT-002 | Contract Detail | Contract | O-05 | 계약생성, 서명요청 | CONTRACT-Rxx | Contract Signed |
| OC-WORK-002 | Work Detail | Fulfillment | O-07 | 작업시작, 증빙제출, 완료 | FULFILL-Rxx | Verified/Partial |
| OC-CASE-001 | Case Detail | CS/AS | O-09 | 배정, 처리, 해결, 재오픈 | CASE-Rxx | Resolved/Closed |

### 개발자가 여기서 읽는 것

- Screen ID
- 메뉴 위치
- 화면 목적
- 주요 Component/Action
- 진입 조건
- Flow ID
- Rule ID
- 다음 화면
- 상태 변경

### 핵심

이 문서가 있어야 개발자가 **"이 Rule을 어디에 코딩하지?"**를 바로 찾을 수 있다.

---

### 단계별 상세 설명 — 역할·담당자·목표·주의사항

### 이 표를 보는 법

각 단계는 **무엇을 결정하는 단계인지(목표)**, **누가 주도하는지(주 담당자)**, **무엇을 만들어야 하는지(산출물)**, **무엇을 조심해야 하는지(주의사항)**, **언제 다음 단계로 넘어가도 되는지(Gate)**로 나눠 본다.

### 1. 사업 목적·문제 정의

- **목표:** 왜 이 제품/기능을 만드는지, 누구의 어떤 문제를 해결하는지 확정한다.
- **역할:** 개발 이전에 방향을 고정하는 최상위 기준점.
- **주 담당자:** 성재님 / Main PM / Product Planning.
- **주요 산출물:** Product Goal, Problem Statement, 핵심 KPI 후보, 사업 우선순위.
- **예시:** OC의 목적을 "상담·계약·설치·AS·재고·정산 업무를 하나의 운영 상태와 이력으로 연결하여 누락·중복·인계 오류를 줄인다"로 정의한다.
- **주의사항:** 기능 목록부터 만들지 않는다. 문제와 목적이 불명확한 상태에서 개발로 넘어가면 이후 모든 문서가 흔들린다.
- **다음 단계 Gate:** 제품이 해결할 문제와 성공 기준을 한 문장으로 설명할 수 있어야 한다.

### 2. Recovery / 기존 자료 복원

- **목표:** 과거 결정·기획·운영자료·코드에서 현재 유효한 사실을 복원한다.
- **역할:** 이미 결정한 것을 다시 결정하거나 과거 실수를 반복하지 않게 한다.
- **주 담당자:** 각 Domain GPT 연구세션 / PM 운영실 / Claude PM3.
- **주요 산출물:** Recovery Evidence, 기존 Decision 목록, Pending 목록, Legacy 참고자료.
- **예시:** 기존 TMS 코드, 과거 Notion 기획, 계약·설치·AS 운영자료를 읽고 `확정 Decision / 미확정 Pending / Legacy 참고`로 나눠 복원한다.
- **주의사항:** `Legacy Reality ≠ Target Architecture`. 기존 코드가 있다는 이유만으로 목표 구조를 Legacy에 맞추지 않는다.
- **다음 단계 Gate:** Fact / Decision / Pending / Legacy Reference가 구분되어 있어야 한다.

### 3. Product Scope / Domain Boundary 확정

- **목표:** 이 제품이 어디까지 책임지고 어디부터 다른 Product/Common Infrastructure가 책임지는지 결정한다.
- **역할:** 중복 개발과 Ownership 충돌을 방지한다.
- **주 담당자:** 성재님 / Main PM / Domain PM / Common Infrastructure 책임 세션.
- **주요 산출물:** 포함·제외 범위, Product Ownership, Context Boundary, Handoff 정의.
- **예시:** OC는 계약·설치·AS·재고·정산의 운영 Owner이며, OSP는 온라인 유입·전환, Business OS는 매장 운영 Surface, PayPoint는 Marketing Play 소유 Product로 경계를 나눈다.
- **주의사항:** 다른 Product의 내부 화면·DB·정책을 자기 Domain에서 임의 확정하지 않는다.
- **다음 단계 Gate:** 각 핵심 기능에 Owner와 책임 경계가 명확해야 한다.

### 4. **Service Architecture / Menu & Depth — 서비스 구조·메뉴·뎁스**

- **목표:** 제품 전체 카테고리, 1Depth·2Depth·3Depth, 기능 소속을 구조화한다.
- **역할:** 제품의 **지도**. 개발자가 전체 제품을 어디서부터 어떻게 나눌지 이해하게 한다.
- **주 담당자:** Product/Domain PM + UX/UI + 개발자 Review.
- **주요 산출물:** Service Tree, Menu Tree, Category/Depth Matrix, Feature Ownership.
- **예시:** `OC > Sales > Opportunity > 상담/방문/Activity`, `OC > Contract > Contract Detail > 계약 Item`, `OC > CS/AS > Case > Work/Resolution`처럼 실제 메뉴 뎁스를 정리한다.
- **주의사항:** 메뉴 구조와 업무 Flow를 혼동하지 않는다. 같은 기능이 여러 메뉴에 중복되지 않도록 한다.
- **다음 단계 Gate:** 모든 주요 기능이 어느 카테고리에 속하는지 설명 가능해야 한다.

### 5. **User & Operations Flows — 사용자 및 운영 흐름**

- **목표:** 고객·운영자·시스템·협력사가 목적을 달성하는 실제 흐름을 정의한다.
- **역할:** 제품의 **이야기와 업무 흐름**. 누가 어디서 시작해 무엇을 하고 어떻게 끝나는지 보여준다.
- **주 담당자:** Domain PM / 실제 운영담당자 / 개발자 Review.
- **주요 산출물:** C/O/S/P Flow, 정상·대안·예외·복구, 상태변화, Handoff.
- **예시:** 고객이 `견적 링크 진입 → 견적 확인 → 수정 요청 또는 수락 → 시스템 검증 → Accepted/Negotiating → 계약 Flow 인계`로 움직이는 `C-02` 흐름을 작성한다.
- **주의사항:** `화면 A → 화면 B`만 쓰지 않는다. 실제 입력·선택·Action·검증·완료·복구를 써야 한다.
- **다음 단계 Gate:** 주요 업무마다 시작조건·행동·완료상태·실패복구를 설명할 수 있어야 한다.

### 6. **Detailed Requirements & Business Policies — 상세 요구사항 및 비즈니스 정책**

- **목표:** 각 Flow가 어떤 Rule·권한·입력·Validation·State로 동작하는지 정의한다.
- **역할:** 제품의 **규칙집**. 개발자가 임의 판단하지 않도록 구현 조건을 고정한다.
- **주 담당자:** Domain PM / 업무 Owner / 성재님 Decision / 개발자 Review.
- **주요 산출물:** Business Rule ID, Required/Optional/Conditional, Permission, Validation, State Transition, AC.
- **예시:** `Sent 견적 Revision은 직접 수정할 수 없다`, `필수값 누락 시 Send를 차단한다`, `Approval Pending이면 발송할 수 없다`처럼 구현·테스트 가능한 Rule로 고정한다.
- **주의사항:** 미확정 정책을 문서 완성을 위해 만들지 않는다. Pending은 Pending으로 남긴다.
- **다음 단계 Gate:** 주요 Action이 언제 허용·차단되고 성공·실패 시 무엇이 되는지 테스트 가능한 문장으로 표현돼야 한다.

### 7. **Screen & Navigation / Traceability — 화면·네비게이션·추적성**

- **목표:** 구조·Flow·Rule을 실제 Screen과 Action에 연결한다.
- **역할:** 구조·흐름·규칙을 **실제 화면에 꽂는 구현 지도**.
- **주 담당자:** Product/Domain PM + UX/UI + 개발자.
- **주요 산출물:** Screen ID, 화면 목적, 진입조건, 주요 Action, Flow ID, Rule ID, 다음 화면/상태.
- **예시:** `OC-QUOTE-003 Quote Editor`에 `O-04`, `QUOTE-Rxx`, `저장/승인요청/발송` Action과 `Sent/Accepted` 다음 상태를 연결한다.
- **주의사항:** 화면을 만들었다고 업무 Rule이 정의된 것은 아니다. Screen/Flow/Rule 간 Traceability가 끊기면 안 된다.
- **다음 단계 Gate:** 개발자가 모든 핵심 Rule에 대해 "어느 화면/Action에 구현하는가?"를 찾을 수 있어야 한다.

### 8. Logical Data Model / Entity 설계

- **목표:** 업무에 등장하는 객체와 관계를 데이터 관점에서 정의한다.
- **역할:** 화면과 Flow 뒤에서 어떤 데이터가 지속적으로 관리되는지 정한다.
- **주 담당자:** Domain PM + 개발자/아키텍트 + Common Infrastructure.
- **주요 산출물:** Entity 목록, 관계, 상태, Master/Projection 구분, 논리 데이터 모델.
- **예시:** `Customer Account ↔ Store ↔ Opportunity ↔ Quote ↔ Contract ↔ Contract Item ↔ Work/Case` 관계를 정의하고, Shared Person/Asset은 공통 Master 참조로 구분한다.
- **주의사항:** Logical Entity와 실제 Physical DB Table을 성급하게 동일시하지 않는다. Shared Master Owner를 침범하지 않는다.
- **다음 단계 Gate:** 주요 Flow의 입력·상태·결과를 어느 Entity가 보존하는지 추적 가능해야 한다.

### 9. API / Integration Specification

- **목표:** 화면·Domain·외부 시스템 사이에 어떤 요청과 응답이 오가는지 정의한다.
- **역할:** 프론트·백엔드·외부 Provider 사이의 **계약서** 역할.
- **주 담당자:** 개발자/아키텍트 + Domain PM + 외부연동 담당자.
- **주요 산출물:** Logical API, Command/Query, Payload 후보, Error/Timeout/Callback, Idempotency 기준.
- **예시:** `견적 발송 Command → 외부 Message/Email Provider → 성공 ACK 시 Sent`, Timeout/Unknown이면 Sent로 확정하지 않고 재조회·재시도하도록 계약을 정의한다.
- **주의사항:** Provider가 미정인데 실제 Endpoint나 Physical Schema를 확정하지 않는다. Timeout/Unknown을 성공으로 처리하지 않는다.
- **다음 단계 Gate:** 주요 Screen Action과 시스템 Handoff에 필요한 Interface가 빠짐없이 식별돼야 한다.

### 10. Physical Architecture / DB / IAM / Provider 결정

- **목표:** 논리 설계를 실제 기술스택·DB·인증·외부 Provider에 배치한다.
- **역할:** "무엇을 만들지"를 "어디에 어떻게 구현할지"로 변환한다.
- **주 담당자:** 개발자/아키텍트 + Common Infrastructure + Main PM 승인 필요 시 성재님.
- **주요 산출물:** Physical DB Schema, Repository 위치, IAM Provider, Integration Provider, Deployment Architecture.
- **예시:** Shared IAM을 어느 Provider로 구현할지, Person/Merchant/Device Master를 어느 공통 Repository·DB에 둘지, OC가 어떤 방식으로 참조할지를 실제 기술 결정으로 확정한다.
- **주의사항:** Domain 문서에서 공통 인프라 결정을 임의로 선점하지 않는다. Logical Spec과 Physical 구현을 구분한다.
- **다음 단계 Gate:** 개발자가 실제 Repository/DB/API/Auth 환경에서 구현을 시작할 기술결정이 확보돼야 한다.

### 11. Development Planning / 개발계획

- **목표:** 구현 순서·의존성·작업단위·완료기준을 실제 개발 일정으로 바꾼다.
- **역할:** 문서를 실제 Sprint/Task로 변환한다.
- **주 담당자:** 개발 PM / 개발자 / Main PM.
- **주요 산출물:** Epic, Task, Dependency, Priority, Definition of Done, 개발 순서.
- **예시:** `Lead/Opportunity → Quote → Contract → Fulfillment/Installation → Case/AS` 순으로 Epic을 나누고, 각 Epic에 화면·API·데이터·테스트 Task를 묶는다.
- **주의사항:** 화면 수만 기준으로 일정 산정하지 않는다. 데이터·API·외부연동·Migration·QA까지 포함한다.
- **다음 단계 Gate:** 개발자가 다음 작업을 추가 질문 없이 Task 단위로 선택할 수 있어야 한다.

### 12. Implementation / 실제 개발

- **목표:** 승인된 구조·Flow·Rule·Screen·기술결정을 실제 코드로 구현한다.
- **역할:** 제품 정의를 실행 가능한 시스템으로 만든다.
- **주 담당자:** 개발자. PM은 질문·정책 Gap·Scope Change를 관리한다.
- **주요 산출물:** Code, Migration, API, UI, Test Code, Commit/PR.
- **예시:** 개발자가 `OC-QUOTE-003` 화면과 Quote Command/API를 구현하고, `Sent Revision 수정 금지` Rule을 Guard와 Test Code로 반영한다.
- **주의사항:** 개발 중 새로운 Product Policy를 개발자가 임의 생성하지 않는다. Gap은 PM/Decision Queue로 올린다.
- **다음 단계 Gate:** Definition of Done과 해당 Flow/Rule Acceptance Criteria를 충족해야 한다.

### 13. QA / Acceptance / 인수검수

- **목표:** 구현물이 문서의 Flow·Rule·Screen 기준대로 동작하는지 검증한다.
- **역할:** "코드가 돌아간다"가 아니라 "의도한 업무가 정확히 돌아간다"를 확인한다.
- **주 담당자:** QA / 개발자 / PM / 실제 운영담당자.
- **주요 산출물:** Test Case, Bug List, Regression 결과, Acceptance Result.
- **예시:** 견적 정상 발송뿐 아니라 `필수값 누락`, `승인대기`, `Provider Timeout`, `중복 요청`, `수정 요청 후 New Revision`까지 Test Case로 검증한다.
- **주의사항:** 정상경로만 검사하지 않는다. Alternative·Exception·Recovery·권한·중복·Timeout도 검수한다.
- **다음 단계 Gate:** BLOCKER/MAJOR가 해소되고 핵심 Acceptance Criteria가 PASS해야 한다.

### 14. Release / Deployment — 배포

- **목표:** 검증된 버전을 실제 사용자 환경에 안전하게 배포한다.
- **역할:** 개발환경 결과물을 Production Service로 전환한다.
- **주 담당자:** 개발자/DevOps + PM 승인 + 운영팀.
- **주요 산출물:** Release Version, Migration 실행, 환경설정, Rollback Plan, 배포기록.
- **예시:** OC v1 배포 전에 DB Migration과 환경변수를 적용하고, 배포 후 로그인 → Lead 조회 → Quote 저장/발송 → Case 조회 같은 핵심 Smoke Test를 실행한다.
- **주의사항:** DB Migration·Credential·환경변수·Rollback·기존 데이터 영향 확인 없이 배포하지 않는다.
- **다음 단계 Gate:** 배포 후 핵심 Health Check와 주요 Flow Smoke Test가 정상이어야 한다.

### 15. Operations / Monitoring / Improvement — 운영·관제·개선

- **목표:** 실제 운영 중 장애·문의·사용성·성과를 관찰하고 다음 개선으로 연결한다.
- **역할:** 출시 후 실제 Reality를 수집해 다음 Product Decision의 Evidence로 만든다.
- **주 담당자:** OC 운영팀 / CS·AS / PM / 개발자 / 성재님.
- **주요 산출물:** Monitoring, Incident, 사용자 Feedback, KPI, 개선 Backlog, Decision Evidence.
- **예시:** 실제 운영에서 `설치 일정 변경 누락`, `AS 반복 장애`, `견적 승인 지연`이 반복되면 Incident/지표로 기록하고 다음 Flow·Rule 개선 Backlog로 환류한다.
- **주의사항:** 운영 중 나온 예외를 즉시 임시정책으로 굳히지 않는다. 반복 문제는 Rule/Flow/Architecture 개선으로 환류한다.
- **다음 단계 Gate:** 끝나는 단계가 아니라 다시 1~7번 기획/문서 개선으로 순환한다.

### 성재님이 기억하면 되는 핵심

> **1~3번은 무엇을 만들지 정하는 단계** → **4~7번은 그것을 개발자가 구현할 수 있게 번역하는 핵심 문서 단계** → **8~11번은 실제 기술 구현 준비** → **12~14번은 개발·검수·배포** → **15번은 운영하면서 다시 개선하는 단계**.

따라서 4문서만으로 회사의 모든 개발업무가 끝나는 것은 아니지만, **제품 기획을 개발 구현으로 넘기는 가장 중요한 Bridge Package**라고 이해하면 된다.

</details>

> 참고 — 전체 제품 기획·개발 절차에서 이 4개 문서의 위치 (성재님 이해용): https://app.notion.com/p/3c153327fb86804bb58de3569e37f09b

---

## 2. 네 문서의 관계

```text
Service Architecture / Menu & Depth
        ↓ 어디에 있는 기능인가
User & Operations Flows
        ↓ 누가 어떻게 사용하는가
Detailed Requirements & Business Policies
        ↓ 어떤 규칙으로 동작하는가
Screen & Navigation / Traceability
        ↓ 어느 화면에서 구현하는가
```

### 한 기능 예시

`견적 수락`

- **Service Tree:** Quote > Quote Detail / Revision
- **Flow:** C-02 / O-04
- **Rule:** QUOTE 관련 Revision·Approval·Send Rule
- **Screen:** Quote Detail / Quote Editor

이 4개가 같은 기능을 서로 다른 관점에서 설명한다.

---

## 3. 4개 문서만 있으면 개발 가능한가?

### 결론

**기능 개발 착수 기준으로는 YES — 단, 4개 문서가 완성되고 서로 Traceability가 연결되어 있다는 조건이다.**

다만 **서비스 전체를 운영 배포까지 완료하는 데 필요한 모든 기술문서가 이 4개라는 뜻은 아니다.** 아래 항목이 이미 공통 인프라나 Repository에서 확정돼 있지 않다면 별도로 필요하다.

- Physical API 계약
- DB Physical Schema / Migration
- Shared IAM 실제 구현
- 외부 Provider Credential / Endpoint / Callback
- 환경변수 / 배포환경
- 테스트 실행 및 Release Gate
- Monitoring / Logging / Rollback

OC에서는 일부가 Common Infrastructure 또는 Integration Pending으로 이미 분리되어 있으므로, 개발자는 **확정된 Scope부터 착수**하고 Pending 의존 영역은 고정 구현하지 않아야 한다.

---

## 4. 개발자에게 전달할 때 권장 읽기 순서

1. **Service Architecture / Menu & Depth** — 전체 제품 구조 파악
2. **User & Operations Flows** — 업무 흐름 이해
3. **Detailed Requirements & Business Policies** — 구현 Rule 확인
4. **Screen & Navigation / Traceability** — 실제 화면 구현 위치 확인

---

## 5. PM Gate

개발자 전달 전 아래가 모두 YES여야 한다.

| Gate | 기준 |
|---|---|
| Service Tree Complete | 주요 Category/Depth/기능 누락 없음 |
| Flow Complete | 주요 사용자 목적 및 운영 Flow 누락 없음 |
| Rule Complete | 개발자가 임의 Business Decision을 만들 필요 없음 |
| Screen Trace Complete | Flow/Rule이 실제 화면과 연결됨 |
| Pending Explicit | 미확정 범위를 확정사항처럼 작성하지 않음 |
| Cross-Document Consistency | 메뉴/Flow/Rule/Screen 간 충돌 없음 |

**PayPlay OC — Main Handoff v3:** https://app.notion.com/p/3be53327fb8681b6842cec140b8f7b56

---

## 6. GitHub Intake Status — 2026-08-21

Claude PM3 Documentation Controller가 수행한 Developer Package GitHub 입고 결과다. Header Status는 Notion 원문을 유지했으며 입고 과정에서 `APPROVED` / `Source of Truth YES`로 승격하지 않았다.

| # | 문서 | Document ID | GitHub Path | Intake Status |
|---|---|---|---|---|
| #1 | Service Architecture / Menu & Depth | `PP-OC-SVC-ARCH-MENU-001` | `10_OC/07_ARCHITECTURE/SERVICE_ARCHITECTURE_MENU_DEPTH.md` | GITHUB COMMITTED (신규) |
| #2 | User & Operations Flows | `PP-OC-USER-OPS-FLOW-001` | `10_OC/04_FLOWS/USER_AND_OPERATIONS_FLOWS.md` | GITHUB COMMITTED (신규 · `PP-OC-FLOWS-001` 승계) |
| #3 | Detailed Requirements & Business Policies | `PP-OC-REQ-BIZ-POLICY-001` | `10_OC/05_REQUIREMENTS_POLICIES/DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md` | GITHUB COMMITTED (신규 · `PP-OC-REQS-001` 승계) |
| #4 | Screen & Navigation / Traceability | `PP-OC-SCREEN-NAV-TRACE-001` | `10_OC/08_SPECIFICATIONS/SCREEN_NAVIGATION_TRACEABILITY.md` | GITHUB COMMITTED (신규) |
| — | Final Pending Register | `PP-OC-FINAL-PENDING-REGISTER-001` | `10_OC/09_DECISIONS/FINAL_PENDING_REGISTER.md` | GITHUB COMMITTED (신규) |
| — | Developer Package Guide (현재 문서) | `PP-OC-DEV-PACKAGE-GUIDE-001` | `10_OC/DEVELOPER_PACKAGE_GUIDE.md` | GITHUB COMMITTED (신규) |

### #2 / #3 Supersede 처리 — 2026-08-21 RESOLVED

최초 입고 시 #2 / #3은 기존 GitHub 공식 문서와 Document ID·Status가 달라 STOP Condition으로 보류했다. **Claude PM3 추가 지시(2026-08-21)로 Supersede 방식이 승인되어 입고를 완료했다.**

| 구분 | 기존 문서 (SUPERSEDED) | 신규 문서 (승계) |
|---|---|---|
| #2 | `PP-OC-FLOWS-001` · `10_OC/04_FLOWS/user-and-operations-flows.md` · Flow ID `OC-FLOW-001~013` | `PP-OC-USER-OPS-FLOW-001` · `10_OC/04_FLOWS/USER_AND_OPERATIONS_FLOWS.md` · Flow ID `C/O/S/P` 29개 |
| #3 | `PP-OC-REQS-001` · `10_OC/05_REQUIREMENTS_POLICIES/detailed-requirements-and-business-policies.md` · 절 단위 정책 서술 | `PP-OC-REQ-BIZ-POLICY-001` · `10_OC/05_REQUIREMENTS_POLICIES/DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md` · Business Rule ID `[CONTEXT]-R[NN]` |

**처리 원칙 (준수 확인)**

- 기존 파일 **삭제하지 않음.** Header Status만 `SUPERSEDED`로 변경했고 본문은 byte 단위로 동일하게 보존했다.
- 따라서 기존 `OC-FLOW-001~013` Flow ID와, 이를 참조하는 `10_OC/08_SPECIFICATIONS/SCREEN_SPECIFICATION_TRACEABILITY_SUMMARY.md`의 `OC-FLOW-008` Traceability는 계속 해석 가능하다. **Trace Break 없음.**
- 신규 문서 Header Status는 Notion 원문의 `FREEZE READY`를 유지했고 `APPROVED` / `Source of Truth YES`로 승격하지 않았다.
- Pending 값 임의 확정 없음. Legacy 항목 삭제·누락 없음.

**Main PM 확인 요청 1건:** 기존 두 파일의 `Source of Truth`를 `YES → NO (SUPERSEDED — 2026-08-21)`로 함께 조정했다. PM3 지시에 명시된 4개 항목(Status / Superseded by / Superseded date / Note)에는 없었으나, `SUPERSEDED` 문서가 `Source of Truth YES`로 남으면 `80_DEVELOPMENT/DEVELOPMENT_GUARDRAILS.md`의 "SUPERSEDED = 구버전, 사용 금지" 규정과 충돌하고 개발자가 구버전을 기준문서로 오인할 수 있어 함께 반영했다. 원복이 필요하면 회신 바란다.
