# PayPlay OC — User & Operations Flows

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/04_FLOWS/USER_AND_OPERATIONS_FLOWS.md` |
| Document ID | PP-OC-USER-OPS-FLOW-001 |
| Version | v5.2 CLEAN / CROSS-SYNC |
| Status | FREEZE READY / CLEAN / AUDITED / LATEST SOT SYNCHRONIZED |
| Final SOT Freeze | COMPLETE — 2026-08-21 16:54 KST · Human Handoff Ready: YES |
| Source of Truth | NO — Main PM 승인 전 APPROVED / Source of Truth YES로 승격하지 않는다. |
| Source Basis | Owner Decision + OC Final SOT + Candidate 1~5 Frozen + Approved Screen Specification + Cross-Service + latest supplemental Target specs |
| Owner | PayPlay OC |
| Last Reviewed | 2026-08-21 |
| Development Use | User / Operator / System / Partner 목적, 상태변화, Handoff, Alternative, Exception, Recovery Flow baseline. Physical API/DB/Provider binding 금지. |
| Resync | 2026-08-21 Final SOT Resync (Main PM GO) |
| Notion Source | https://app.notion.com/p/3bf53327fb868164bb03d968f010ea1f |
| Developer Package | Document #2 / 4 |
| Supersedes | `PP-OC-FLOWS-001` — [user-and-operations-flows.md](./user-and-operations-flows.md) (2026-08-21, Claude PM3 지시) |
| Related Pending | [FINAL_PENDING_REGISTER.md](../09_DECISIONS/FINAL_PENDING_REGISTER.md) |

## ✅ FINAL SOT FREEZE — 2026-08-21 16:54 KST

- Human Handoff Ready: **YES**
- Final SOT Freeze: **COMPLETE**
- Final Fix Verification: **PASS**
- Flow↔Rule Trace Break: **0**
- Existing 29 Canonical Flow ID Damage: **0**
- Package-wide Scope-Blocking Pending: **0**
- Remaining Pending: **Physical / Provider / Config boundaries only**

> 본 문서는 현재 OC User & Operations Flow Logical SOT로 Freeze합니다. 기존 Canonical Flow ID를 재번호하지 않으며 Physical Binding 값을 임의 확정하지 않습니다.

---

> 👀 **이 문서는 언제 보나요?**
> “누가, 어떤 목적으로, 어떤 순서로 일하고 어디서 다음 담당자에게 넘어가는가?”를 확인할 때 보는 **업무 흐름 문서**입니다.
> 주요 용어: User & Operations Flow (사용자·운영 업무 흐름), Handoff (업무 인계), Alternative (대안 경로), Exception (예외 상황), Recovery (복구 경로), State (업무 상태), Provider (외부 연동업체/시스템).
> 화면 목록을 보는 문서가 아니라 **업무의 시작→처리→완료 흐름**을 이해하는 문서입니다.
> 🧭 정우용 개발자님 제공 `사용자 및 운영 흐름 문서 템플릿`을 기준으로 PayPlay OC 전체 흐름을 재작성한 Clean Version이다. 화면 목록이 아니라 사용자·운영자·시스템·협력사가 달성하려는 목적, 상태 변화, 대안·예외·복구, Handoff와 외부 연결을 기준으로 한다. 상세 Field·Validation·Permission·판정조건은 `[OC] Detailed Requirements & Business Policies`의 Business Rule ID로 연결한다.

---

**Related Document:** [DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md](../05_REQUIREMENTS_POLICIES/DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md) (PP-OC-REQ-BIZ-POLICY-001), Approved Screen Specification, OC Final SOT
**Template Basis:** 사용자 및 운영 흐름 / 상세 요구사항 및 비즈니스 정책

## 1. 문서 목적

이 문서는 화면 단위가 아니라 **사용자와 운영자가 달성하려는 목적과 업무 상태 변화**를 중심으로 PayPlay OC의 흐름을 설명한다.
OC는 OSP 또는 기존 고객 요청을 받아 고객·매장 식별, 영업, 견적, 계약, 이행·설치, 재고·공급, CS·AS, 비용·정산, 수당, 경영 의사결정까지의 내부 운영을 연결한다.

### 1.1 작성 원칙

- 시작 조건부터 목적 달성까지의 흐름을 작성한다.
- 정상 경로뿐 아니라 실패·중단·재시도·운영 복구 경로를 함께 작성한다.
- 사용자 또는 팀이 바뀌는 Handoff를 명시한다.
- 외부 시스템 호출의 성공·실패·결과 불명 상태를 구분한다.
- 확정·제외·미확정 범위를 섞지 않는다.
- 상세 값·권한·Validation·판정조건은 Business Rule ID로 연결한다.
- Logical Screen ID는 Physical URL이 아니다.
- `Legacy Reality ≠ OC Target Architecture`; 기존 TMS는 참고자료다.

## 2. 용어와 흐름 식별자

### 2.1 사용자 유형

| 구분 | 식별자 | 설명 | 주요 목적 |
|---|---|---|---|
| 고객 | `C` | 신규·기존 고객, 매장 관계자 | 상담, 견적·계약, 설치 협의, CS·AS, 추가구매 |
| 운영자 | `O` | OC Backoffice 및 내부 업무 사용자 | 영업·승인·계약·설치·재고·지원·정산·관리 |
| 시스템 | `S` | 자동 검증, Queue, Snapshot, Notification, AI 보조 | 중복 방지, 자동화, 이력 보존, 업무 보조 |
| 협력사 | `P` | 외부 기사, Vendor, 제조사, 통신/PG/발송 Provider | 설치·배송·AS·외부 연동·결과 반환 |

### 2.2 흐름 식별자 규칙

| 대상 | 형식 | 예시 |
|---|---|---|
| 고객 흐름 | `C-[일련번호]` | `C-01` |
| 운영자 흐름 | `O-[일련번호]` | `O-01` |
| 시스템 흐름 | `S-[일련번호]` | `S-01` |
| 협력사 흐름 | `P-[일련번호]` | `P-01` |
| 대안 경로 | `[흐름 ID]-A[일련번호]` | `C-01-A01` |
| 예외·복구 경로 | `[흐름 ID]-E[일련번호]` | `C-01-E01` |

식별자는 재번호를 매기지 않는다. 폐기 흐름은 삭제 대신 상태와 대체 흐름을 기록한다.

> **Trace Set 해석 기준:** 본 문서의 기존 C/O/S/P 29개 ID는 2026-08-18 기준 Canonical Trace Set이며, 이후 Owner Decision과 Cross-Service 보강으로 추가된 모든 업무 Capability의 총 개수를 의미하지 않는다. 신규 업무가 기존 Flow의 Subflow / Projection / Cross-Service Handoff / Common Capability로 설명 가능한 경우 문서 숫자를 맞추기 위해 임의의 신규 Flow ID를 생성하지 않는다.

## 3. 이번 릴리스의 흐름 범위

| 포함 | 제외 | 제외 이유 또는 후속 계획 |
|---|---|---|
| 상담/Lead/Request 접수 및 고객·매장 Match | Shared Person/Merchant/IAM/Device·Asset Physical 구현 | Common Infrastructure 결정 |
| 담당자 배정·상담·방문·견적·계약 | FLOW-007 상품/직군별 수당 계산식·비율 | Business Policy Config 값 미입력 — 계산/승인 엔진 구조는 확정, 실제 Formula/Rate 값만 추후 입력 |
| 계약 Item 이행·설치·검증·복수 Item 처리 | FLOW-007 항목별 팀장 단독승인 범위 | Business Policy Config 값 미입력 — Approval Policy Configuration 구조는 확정, 실제 적용 항목만 추후 입력 |
| 재고·발주·배송·AS 공급 | 외부 Provider 실제 Endpoint/Provider 선정 | Integration 단계 결정 |
| CS·AS·Escalation·재오픈 | Product별 exact Evidence Template | Domain Configuration |
| 비용·정산·수당 Eligibility·경영 Decision | 미확정 Physical API/DB Schema | 별도 Architecture 결정 |
| Policy Snapshot·Queue·Notification·AI Guard |  |  |
| Vehicle·Parking·Schedule / Meeting 등 Company Operations·Common Supplemental Flow |  | Owner Decision 반영된 Target Scope. 기존 29 Canonical Flow ID를 재번호하지 않고 Supplemental Trace로 관리 |
| Workforce Service Desk — 재직자 Self-Service + 외부직원·퇴사자·해촉자 Public Entry / Request 처리 |  | WSD-C-01 / WSD-C-02 / WSD-O-01 Supplemental Flow로 관리 |

### 3.1 범위 판단 기준

- **포함:** 현재 SOT와 Owner Decision으로 구현·검수 가능한 흐름.
- **제외:** 이번 릴리스에서 제공하지 않거나 Common Infrastructure/Provider 결정이 선행되어야 하는 범위.
- **미확정:** 세부 값 또는 포함 여부가 결정되지 않아 고정 구현하면 안 되는 범위.

### 3.2 흐름 요약

| 흐름 ID | 사용자 | 목적 | 시작점 | 완료 상태 | 범위 | 관련 컨텍스트 |
|---|---|---|---|---|---|---|
| `C-01` | 고객 | 상담·영업 요청 접수 | OSP/외부채널 | OC Intake Accepted | 포함 | SALES |
| `C-02` | 고객 | 견적 확인·수정·수락 | 견적 링크/영업 안내 | Accepted/Negotiating/Rejected | 포함 | QUOTE |
| `C-03` | 고객 | 계약 확인·서명 | 계약/전자서명 | Contract Signed | 포함 | CONTRACT |
| `C-04` | 고객 | 설치 일정·결과 확인 | 설치 연락/일정 | Verified/Partial/Revisit | 포함 | FULFILLMENT |
| `C-05` | 고객 | CS·AS 요청 | 고객센터/전화/메시지 | Activity 기록 또는 Case `New` 생성 | 포함 | CASE |
| `C-06` | 고객 | AS 결과 확인·재요청 | 처리결과 안내 | Closed/Reopened | 포함 | CASE |
| `C-07` | 고객 | 추가구매·변경 요청 | 기존 Customer/Store | Opportunity Created | 포함 | SALES |
| `O-01` | 영업 운영자 | 고객·매장 Match/Opportunity 생성 | Intake | Opportunity New | 포함 | SALES |
| `O-02` | 영업 관리자 | 담당자 배정 | Opportunity | Assigned | 포함 | SALES |
| `O-03` | 영업 담당자 | 상담·방문·요구사항 확정 | Assigned Opportunity | Quote Ready/Follow-up | 포함 | SALES |
| `O-04` | 영업/승인자 | 견적 작성·승인·발송 | Quote Ready | Sent/Accepted | 포함 | QUOTE |
| `O-05` | 계약 관리자 | 계약 체결 | Accepted Revision | Contract Signed | 포함 | CONTRACT |
| `O-06` | 설치 관리자 | 이행 준비·설치 배정 | Signed Contract | Work Scheduled | 포함 | FULFILLMENT |
| `O-07` | 현장 담당자 | 설치·검증·완료 | Scheduled Work | Verified/Partial/Failure | 포함 | FULFILLMENT |
| `O-08` | 재고/구매 | 재고·발주·배송 | Material Requirement | Reserved/Allocated/Shipped | 포함 | INVENTORY |
| `O-09` | CS/AS | Case 처리·해결 | 고객 요청/장애 | Resolved/Closed | 포함 | CASE |
| `O-10` | 재무 | 비용 검토·승인·정산 | Expense Event | 정산완료/취소 | 포함 | FINANCE |
| `O-11` | 보상/재무 | 수당 Eligibility·승인 | 계약/설치/입금 Event | 지급대기 | 부분 포함 | COMP |
| `O-12` | 경영진 | 의사결정 기록·실행·복기 | Decision 필요 | 종료/취소 | 포함 | MGMT |
| `O-13` | 영업 | 기존 고객 추가구매/변경 | Customer 360 | Opportunity Assigned | 포함 | SALES |
| `O-14` | 계약/설치 | 복수 Item 병렬 이행 | Multi-item Contract | 부분완료/완료/Activation | 포함 | FULFILLMENT |
| `O-15` | CS/AS | 중대·반복 장애 Escalation | Open Case | 해결/종료 | 포함 | CASE |
| `S-01` | 시스템 | 중복 고객/매장 후보 탐지 | Intake/Opportunity | Match/Review Candidate | 포함 | CUSTOMER |
| `S-02` | 시스템 | Policy Snapshot 보존 | Policy 적용 Event | Snapshot Saved | 포함 | POLICY |
| `S-03` | 시스템/AI | Contextual AI 보조 | 업무 Context | Draft/Human-confirmed Command | 포함 | AI |
| `S-04` | 시스템 | Queue/Notification 생성 | 업무 Event | Queue/Notification 반영 | 포함 | COMMON |
| `P-01` | 외부 기사 | 설치/현장 작업 수행 | Assigned Work | 결과 반환 | 포함 | FULFILLMENT/CASE |
| `P-02` | Vendor/제조사 | 배송·AS 외부 처리 | External Request | 결과 반환/대기 | 포함 | INVENTORY/CASE |
| `P-03` | 외부 Provider | 발송·전자서명 등 연동 | External Command | Success/Failure/Unknown | 포함 | QUOTE/CONTRACT |

## 4. 고객 흐름

### C-01. 상담·영업 요청 접수

**상태:** 확정
**목적:** 고객이 PayPlay 상담 또는 영업 요청을 제출하고 후속 연락 대상으로 등록된다.
**사용자:** 신규 고객, 기존 고객, 매장 관계자
**시작 조건:** 상담/추가구매/변경 요청 의사가 있다.
**시작점:** OSP 상담신청, 외부 채널, 내부 기존고객 요청
**완료 상태:** OC Intake Accepted 또는 Human Review

#### 정상 경로

> 신청 진입 → 정보 입력 → 필수값 검증 → 등록 → OC Handoff → 고객/매장 Match → 접수 완료

1. 고객이 상담/영업 요청 화면 또는 채널에 진입한다.
2. 이름/연락처/매장 또는 요청 내용을 입력한다.
3. 시스템이 해당 채널의 필수값을 검증한다.
4. 고객이 등록/신청 Action을 수행한다.
5. Source와 Request가 OC로 Handoff된다.
6. OC가 고객/매장 후보를 확인하고 Intake를 수락하거나 Review로 보낸다.

#### 대안 경로

- **`C-01-A01`**** 기존 고객:** 신규 Customer를 만들지 않고 기존 Customer/Store에 Request/Opportunity를 연결한다.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `C-01-E01` | 필수값 누락 | 제출 차단 | 누락 항목 안내 | 입력 보완 | 미완료 |
| `C-01-E02` | 복수/애매 Match | 자동 Merge 금지 | 내부 확인 | Human Review | Review Pending |
| `C-01-E03` | OC Handoff 실패 | 성공 처리 금지 | 재시도/확인 안내 | 재전송·운영확인 | Pending |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Request | 없음/New | OC 수신·검증 | Intake Accepted/Review | 시스템/운영자 | 상담 신청 접수 |

#### 외부 연결 지점

| 시점 | 외부 시스템 | 주고받는 내용 | 성공 기준 | 실패·결과 불명 처리 |
|---|---|---|---|---|
| 신청 제출 | OSP/외부 채널 | Lead, Source, Request | OC ACK/수신 Trace | 재전송·운영확인 |

### C-02. 견적 확인·수정 요청·수락

**상태:** 확정
**목적:** 고객이 견적을 확인하고 수락·수정요청·거절 중 하나를 선택한다.
**사용자:** 계약 의사결정권이 있는 고객 관계자
**시작 조건:** 발송 가능한 Quote Revision이 존재한다.
**시작점:** 견적 링크/PDF/영업 담당자 안내
**완료 상태:** Accepted / Negotiating / Rejected

#### 정상 경로

> 견적 진입 → 상품/수량/금액/조건 확인 → 수락 또는 수정요청 → 결과 기록 → 계약 Handoff

1. 고객이 최신 유효 견적을 연다.
2. 상품·수량·금액·조건을 확인한다.
3. 고객이 수락 또는 수정요청/거절 Action을 선택한다.
4. 시스템/운영자가 최신 유효 Revision인지 검증한다.
5. 수락이면 Accepted Revision으로 기록하고 계약으로 인계한다.

#### 대안 경로

- **`C-02-A01`**** 수정 요청:** 기존 Sent Revision은 보존하고 New Revision을 만든다.
- **`C-02-A02`**** 보류/거절:** 사유와 Follow-up 필요 여부를 기록한다.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `C-02-E01` | 견적 링크/발송 실패 | Sent 성공 간주 금지 | 재발송 안내 | 재전송 | Ready/Sending |
| `C-02-E02` | 오래된 Revision 접근 | 직접 수정 금지 | 최신본 안내 | 최신 유효 Revision 확인 | 기존 상태 |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Quote Revision | Sent | 수락 | Accepted | 고객/운영자 | 견적 수락 완료 |
| Quote Revision | Sent | 수정 요청 | Negotiating | 고객/운영자 | 수정 협의 중 |

#### 외부 연결 지점

| 시점 | 외부 시스템 | 주고받는 내용 | 성공 기준 | 실패·결과 불명 처리 |
|---|---|---|---|---|
| 견적 발송 | Message/Email Provider | 견적 링크/PDF | Provider 성공 응답 | 재시도·조회·운영확인 |

### C-03. 계약 확인·서명

**상태:** 확정
**목적:** 고객이 Accepted Quote 기반 계약내용을 확인하고 서명한다.
**사용자:** 계약 당사자 또는 서명 권한자
**시작 조건:** Accepted Revision과 계약 초안이 존재한다.
**시작점:** 계약 링크/전자서명/계약 담당자 안내
**완료 상태:** Contract Signed

#### 정상 경로

> 계약 진입 → 계약내용 확인 → 서명 → Provider 결과 확인 → Signed → 설치/이행 Handoff

1. 고객이 계약서를 연다.
2. 계약 당사자·상품·금액·약정조건을 확인한다.
3. 고객이 서명 Action을 수행한다.
4. Provider 또는 운영자가 완료 결과를 확인한다.
5. 성공 확인 후 Contract를 Signed로 전환한다.

#### 대안 경로

- **`C-03-A01`**** 계약 수정 필요:** 원 계약을 덮어쓰지 않고 Revision/Amendment로 되돌린다.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `C-03-E01` | 전자서명 실패/timeout | Signed 전환 금지 | 재시도 안내 | Provider 재조회/재시도 | Pending |
| `C-03-E02` | 중복 서명 결과 | Idempotency | 이미 처리됨 안내 | 기존 계약 확인 | 기존 상태 |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Contract | Draft/Ready | 서명 완료 확인 | Signed | 고객+시스템/운영자 | 계약 완료 |

#### 외부 연결 지점

| 시점 | 외부 시스템 | 주고받는 내용 | 성공 기준 | 실패·결과 불명 처리 |
|---|---|---|---|---|
| 전자서명 | e-sign Provider | 계약서/서명 결과 | Provider 완료 + 내부 확인 | 재조회·재시도·Human Confirm |

### C-04. 설치 일정 협의·설치 확인

**상태:** 확정
**목적:** 고객이 설치 일정과 현장조건을 협의하고 설치 결과를 확인한다.
**사용자:** 매장 운영자/현장 Contact
**시작 조건:** Contract Item이 설치 준비 대상으로 생성된다.
**시작점:** 설치 일정 연락/안내
**완료 상태:** Verified Complete / Partial / Revisit

#### 정상 경로

> 일정 제안 → 고객 일정 확인 → 현장 작업 → Evidence/Verification → 결과 확인

1. 고객과 설치 가능한 날짜/시간을 협의한다.
2. 설치 장소와 현장 연락처를 확인한다.
3. 기사가 현장 작업을 수행한다.
4. 고객 확인이 필요한 경우 결과를 확인한다.
5. 필수 Evidence와 Verification 충족 시 Item을 완료한다.

#### 대안 경로

- **`C-04-A01`**** 일정 변경:** 기존 일정 이력을 보존하고 새 Schedule을 기록한다.
- **`C-04-A02`**** 일부 Item 미완료:** 완료 Item은 유지하고 미완료 Item만 Revisit한다.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `C-04-E01` | 설치 실패 | Work/Item Failure 기록 | 재방문/지원 안내 | Case/Revisit | Failure/Partial |
| `C-04-E02` | 필수 Evidence 누락 | Verified 차단 | 내부 누락 안내 | Evidence 보완 | Verification Pending |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Work Item | Scheduled | 작업 시작 | In Progress | 기사/운영자 | 설치 진행 |
| Contract Item | In Progress | Verification 완료 | Verified Complete | 운영자/시스템 | 설치 완료 |

#### 외부 연결 지점

외부 기사 수행 시 `P-01`을 참조한다.

### C-05. CS·AS 요청 접수

**상태:** 확정
**목적:** 고객이 문의 또는 장애를 접수하고 처리 추적 가능한 상태를 만든다.
**사용자:** 고객/매장 관계자
**시작 조건:** 문의·고장·장애·변경 요청이 발생한다.
**시작점:** 고객센터/전화/메시지/내부 접수
**완료 상태:** Activity 또는 Case 생성

#### 정상 경로

> 요청 접수 → Customer/Store 확인 → 유형/영향 입력 → Case 필요 판정 → 접수 결과 안내

1. 고객 요청을 접수한다.
2. Customer/Store를 확인한다.
3. 증상·요청내용·영향도를 기록한다.
4. 추적 필요 시 Case를 생성한다.
5. 접수 결과와 다음 행동을 안내한다.

#### 대안 경로

- **`C-05-A01`**** 단순 문의:** Case 없이 Activity 기록 후 종료.
- **`C-05-A02`**** 심각 장애:** Escalation 조건이면 `O-15`로 연결.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `C-05-E01` | Customer/Store 식별 불가 | 자동 연결 금지 | 추가정보 요청 | Human Review | Review Pending |
| `C-05-E02` | 중복 Open Case 의심 | 경고 | 기존 Case 확인 | 연결/신규 판단 | Open |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Case | 없음 | Case 생성 | New | 운영자 | AS/문의 접수 |

#### 외부 연결 지점

외부 채널로 접수된 경우 채널의 Request ID/Source를 보존한다.

### C-06. AS 결과 확인·재요청

**상태:** 확정
**목적:** 고객이 처리 결과를 확인하고 미해결·재발 시 재처리를 요청한다.
**사용자:** 고객/매장 관계자
**시작 조건:** Case Work가 처리되었거나 Resolution이 제시된다.
**시작점:** 처리 결과 안내
**완료 상태:** Closed / Reopened / Linked Case

#### 정상 경로

> 처리결과 확인 → Resolution 확인 → Close Guard → 종료 안내

1. 운영자가 처리 결과를 기록한다.
2. 고객에게 결과를 안내한다.
3. 필수 Work와 Resolution 완료 후 Close한다.
4. 고객에게 종료를 안내한다.

#### 대안 경로

- **`C-06-A01`**** 미해결:** In Progress 유지 또는 추가 Work 생성.
- **`C-06-A02`**** 재발:** Reopen 또는 Linked Case 생성.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `C-06-E01` | Vendor 완료 통보만 존재 | 내부 Close 자동 금지 | 내부 확인 중 | Human Confirm | Verification Pending |
| `C-06-E02` | 재발 | 기존 이력 삭제 금지 | 재처리 안내 | Reopen/Linked Case | Reopened/Open |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Case | Resolved | Close Guard 충족 | Closed | 운영자 | 처리 완료 |
| Case | Closed | 재발 확인 | Reopened/Linked | 운영자 | 재처리 |

#### 외부 연결 지점

Vendor/외부 기사 결과는 내부 검증 전 최종 Close 근거가 되지 않는다.

### C-07. 기존 고객 추가구매·변경 요청

**상태:** 확정
**목적:** 기존 고객의 추가구매·변경 요청을 기존 이력과 연결한다.
**사용자:** 기존 고객/매장 관계자
**시작 조건:** 기존 Customer/Store가 존재한다.
**시작점:** Customer 360/전화/담당자 접수
**완료 상태:** Opportunity Created/Assigned

#### 정상 경로

> 기존 고객 확인 → Store 선택 → 기존 계약/Asset/Case 확인 → 요청 기록 → Opportunity 생성 → 상담/견적

#### 대안 경로

- **`C-07-A01`**** Store 불명확:** Match/Human Review 후 정상 흐름으로 복귀.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `C-07-E01` | 기존 Store 식별 실패 | 자동 신규 생성 금지 | 추가 정보 확인 | O-01 Match | Review Pending |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Opportunity | 없음 | 추가구매 요청 연결 | New/Assigned | 운영자 | 상담 진행 |

#### 외부 연결 지점

N/A.

## 5. 운영자 흐름

### O-01. 고객·매장 식별 및 Opportunity 생성

**상태:** 확정
**목적:** Intake를 올바른 Customer/Store에 연결하고 Opportunity를 생성한다.
**사용자:** 영업 운영자, Operations Admin
**시작 조건:** Intake Accepted
**시작점:** Intake/Lead Detail
**완료 상태:** Opportunity New

#### 정상 경로

> Intake 열기 → 식별정보 확인 → Match 검색 → 후보 확인 → 연결/신규 Candidate → Opportunity 생성

1. Intake Detail에 들어간다.
2. 이름·전화·상호·주소·사업자정보 등 식별정보를 확인한다.
3. 고객/매장 검색 Action을 수행한다.
4. 단일 명확 후보면 기존 Store에 연결한다.
5. 신규면 Candidate를 만든다.
6. Opportunity 생성 Action을 수행한다.

#### 대안 경로

- **`O-01-A01`**** 단일 명확 Match:** 기존 Store 연결.
- **`O-01-A02`**** 신규 고객:** 신규 Candidate 생성.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-01-E01` | 복수/애매 Match | Auto-link 금지 | 후보 비교 | Human Review | Review Pending |
| `O-01-E02` | 중복 Opportunity | Idempotency | 기존건 안내 | 기존 Opportunity 이동 | 기존 상태 |
| `O-01-E03` | 검색 timeout | 결과 확정 금지 | 재시도 | 재검색 | Pending |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Opportunity | 없음 | Create | New | 운영자 | 영업기회 생성 |

#### 외부 연결 지점

OSP 유입 시 C-01의 OSP→OC Handoff를 참조한다.

### O-02. 영업 담당자 배정

**상태:** 확정
**목적:** Opportunity를 실제 처리 담당자에게 배정한다.
**사용자:** 영업 관리자
**시작 조건:** Opportunity New/Unassigned
**시작점:** Opportunity Detail/Assignment Action
**완료 상태:** Assigned

#### 정상 경로

> Opportunity 열기 → 담당자 선택 → 활성/권한 확인 → 배정 → Queue 반영

#### 대안 경로

- **`O-02-A01`**** 즉시 배정 불가:** Team Queue 대기.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-02-E01` | 유효 담당자 없음 | 배정 차단 | 담당자 없음 | Team Queue/재배정 | Unassigned |
| `O-02-E02` | 권한 없음 | 변경 금지 | Access Denied | 권한자 요청 | 기존 상태 |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Opportunity | New/Unassigned | Assign | Assigned | 영업 관리자 | 담당자 배정 완료 |

#### 외부 연결 지점

N/A.

### O-03. 상담·방문 및 요구사항 확정

**상태:** 확정
**목적:** 고객 요구·상품·예산·설치조건을 확인해 견적 가능 상태로 만든다.
**사용자:** 내부/외부 영업 담당자
**시작 조건:** Opportunity Assigned
**시작점:** Opportunity Detail/Touch 기록
**완료 상태:** Quote Ready / Follow-up / Rejected

#### 정상 경로

> 상담 기록 → 필요 시 방문 일정 → 요구사항 입력 → 다음 행동 선택 → Quote Ready

1. Opportunity에 들어간다.
2. 상담 결과/접촉 채널/다음 연락일을 기록한다.
3. 방문이 필요하면 일정을 잡고 결과를 기록한다.
4. 상품·수량·예산·설치조건을 정리한다.
5. 견적 가능하면 Quote Ready로 인계한다.

#### 대안 경로

- **`O-03-A01`**** 방문 불필요:** 원격 상담으로 진행.
- **`O-03-A02`**** 보류:** Follow-up 일자 저장.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-03-E01` | 고객 연락 불가 | Activity 기록 | 내부 후속 안내 | Follow-up | Follow-up |
| `O-03-E02` | 고객 거절 | 사유 저장 | 영업 종료 | 향후 재기회 가능 | Rejected |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Opportunity | Assigned | 요구사항 확정 | Quote Ready | 영업 담당자 | 견적 준비 |

#### 외부 연결 지점

통화/메시지 Provider는 Physical Provider 결정 전 Interface Only.

### O-04. 견적 작성·승인·발송

**상태:** 확정
**목적:** 승인된 정책을 기준으로 견적 Revision을 작성하고 고객에게 발송한다.
**사용자:** 영업 담당자, 승인자
**시작 조건:** Quote Ready
**시작점:** Quote Create/Edit
**완료 상태:** Sent / Accepted / Negotiating

#### 정상 경로

> 견적 작성 → Policy 적용 → Validation → 필요 시 승인 → 발송 → 고객 결과 반영

1. Quote 작성 화면에 들어간다.
2. 상품·수량·가격·할인·조건을 입력한다.
3. Approved+Effective Policy를 적용한다.
4. Validation 및 Approval 필요 여부를 확인한다.
5. 필요 시 승인 요청을 보낸다.
6. 승인 후 견적 발송 Action을 수행한다.
7. 고객 수락/수정 결과를 C-02와 연결한다.

#### 대안 경로

- **`O-04-A01`**** 정책 범위 내:** Approval 없이 발송 가능.
- **`O-04-A02`**** 수정 요청:** Sent Revision 보존 + New Revision.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-04-E01` | Policy/Formula 오류 | 발송 차단 | 오류 안내 | 수정 후 재검증 | Draft |
| `O-04-E02` | Approval Pending | 발송 차단 | 승인대기 | 승인 후 재시도 | Approval Pending |
| `O-04-E03` | Provider 실패/Unknown | Sent 자동변경 금지 | 발송확인 필요 | 재시도/조회 | Ready/Unknown |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Quote Revision | Draft | Approval 제출 | Approval Pending | 영업 | 승인 대기 |
| Quote Revision | Approved/Ready | 발송 성공 | Sent | 시스템/운영자 | 견적 발송 |

#### 외부 연결 지점

| 시점 | 외부 시스템 | 주고받는 내용 | 성공 기준 | 실패·결과 불명 처리 |
|---|---|---|---|---|
| 견적 발송 | Message/Email Provider | Quote Link/PDF | Provider 성공 응답 | 재시도/조회/운영확인 |

### O-05. 계약 체결

**상태:** 확정
**목적:** Accepted Revision을 계약으로 전환하고 계약 이력을 보존한다.
**사용자:** 계약 관리자, 영업 담당자
**시작 조건:** Accepted Revision
**시작점:** Contract Create/Detail
**완료 상태:** Contract Signed

#### 정상 경로

> Accepted Revision 확인 → 계약 생성 → 당사자/조건 확인 → Policy Snapshot → 서명 → Signed → Fulfillment 생성

#### 대안 경로

- **`O-05-A01`**** 계약 변경:** 원 계약 덮어쓰기 금지, Amendment/Revision 사용.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-05-E01` | 중복 Conversion | 신규 생성 차단 | 기존 계약 이동 | 기존건 확인 | 기존 상태 |
| `O-05-E02` | 서명 결과 Unknown | Signed 금지 | 확인 필요 | Provider 재조회 | Pending |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Contract | Draft/Ready | 서명 완료 | Signed | 시스템/운영자 | 계약 체결 완료 |

#### 외부 연결 지점

전자서명은 `P-03` 참조.

### O-06. 계약 Item 이행 준비·설치 배정

**상태:** 확정
**목적:** Contract Item별 설치/이행 조건을 확인하고 Work를 배정한다.
**사용자:** 설치 관리자
**시작 조건:** Contract Signed
**시작점:** Contract/Fulfillment Detail
**완료 상태:** Work Scheduled

#### 정상 경로

> Item 분해 → Requirement 생성 → Readiness 확인 → 자재/주소/연락처 확인 → 담당자·일정 배정

#### 대안 경로

- **`O-06-A01`**** 재고 부족:** `O-08` Handoff.
- **`O-06-A02`**** 일부 Item Ready:** Ready Item부터 병렬 진행.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-06-E01` | Not Ready | Schedule 차단 | Blocker 표시 | 조건 충족 후 재검사 | Not Ready |
| `O-06-E02` | Assignee 없음 | 배정 차단 | 담당자 필요 | Team Queue | Pending |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Work Item | Ready | 배정·일정 저장 | Scheduled | 설치 관리자 | 설치 예정 |

#### 외부 연결 지점

외부 기사 배정 시 `P-01`, Vendor/배송 필요 시 `P-02`.

### O-07. 현장 설치·검증·완료

**상태:** 확정
**목적:** 현장 작업을 수행하고 Evidence/Verification으로 Item 완료를 판정한다.
**사용자:** Field Team, 외부 기사
**시작 조건:** Work Scheduled
**시작점:** Work Detail/Mobile Work
**완료 상태:** Verified / Partial / Failure

#### 정상 경로

> 작업 시작 → 설치/설정 → Evidence 입력·업로드 → 완료 요청 → Verification → 완료

#### 대안 경로

- **`O-07-A01`**** Partial:** 잔여수량/원인 기록 + Revisit Work.
- **`O-07-A02`**** Failure:** Case 생성 + 원 Work Context 유지.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-07-E01` | Evidence 누락 | Verified 차단 | 누락 표시 | 보완 업로드 | Verification Pending |
| `O-07-E02` | 업로드 실패 | 상태 유지 | 재시도 | Idempotent 재업로드 | In Progress |
| `O-07-E03` | 작업 실패 | Failure 기록 | 재방문/AS | Case/Revisit | Failure |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Work Item | Scheduled | 작업 시작 | In Progress | 기사 | 작업중 |
| Work Item | In Progress | Verification | Verified/Partial/Failure | 운영자/시스템 | 완료/부분완료/실패 |

#### 외부 연결 지점

외부 기사면 `P-01` 참조.

### O-08. 재고·발주·배송

**상태:** 확정
**목적:** 설치/AS에 필요한 수량재고와 Asset/Serial을 확보한다.
**사용자:** 재고·구매·물류 담당자
**시작 조건:** Material Requirement
**시작점:** Inventory/Requirement Detail
**완료 상태:** Reserved/Allocated/Shipped

#### 정상 경로

> Availability 확인 → Reservation → Allocation → 부족 시 PO → Shipment → 실제 사용 기록

#### 대안 경로

- **`O-08-A01`**** 재고 부족:** PO Candidate 생성.
- **`O-08-A02`**** Vendor 직배송:** 창고 입고 없이 Shipment 추적.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-08-E01` | Vendor 지연 | Waiting External | 지연 표시 | 추적/재조달 | Waiting |
| `O-08-E02` | 배송 오류/반품 | Return/Repair 기록 | 재배송/반품 안내 | 새 Shipment | Exception |
| `O-08-E03` | 중복 Transaction | Idempotency | 기존건 안내 | 기존 Transaction 확인 | 기존 상태 |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Material | Required | Reservation | Reserved/Allocated | 재고 담당자 | 자재 확보 |

#### 외부 연결 지점

Vendor/배송은 `P-02` 참조.

### O-09. CS·AS 접수 및 해결

**상태:** 확정
**목적:** 고객 문의/장애를 Case로 추적하고 해결 후 종료한다.
**사용자:** CS, AS, Field Team
**시작 조건:** 고객 요청/장애
**시작점:** Case Create/Customer 360
**완료 상태:** Resolved/Closed

#### 정상 경로

> 고객/Store 확인 → 유형/Severity 입력 → Case 생성 → 담당자 배정 → Work 처리 → Resolution → Close

#### 대안 경로

- **`O-09-A01`**** 단순 문의:** Activity 기록 후 종료.
- **`O-09-A02`**** 재발:** Reopen 또는 Linked Case.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-09-E01` | Remote timeout | Case 자동변경 금지 | 결과확인 필요 | 수동결과/재시도 | In Progress |
| `O-09-E02` | Vendor 대기 | Waiting | 외부업체 대기 | Follow-up | Waiting |
| `O-09-E03` | Close Guard 미충족 | Close 차단 | 누락조건 표시 | Work/Resolution 보완 | Open |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Case | New | Assign | Assigned | 운영자 | 담당자 배정 |
| Case | Assigned | 처리 시작 | In Progress | 담당자 | 처리중 |
| Case | Resolved | Close Guard 충족 | Closed | 운영자 | 처리 완료 |

#### 외부 연결 지점

외부 기사/Vendor는 `P-01/P-02` 참조.

### O-10. 비용·정산

**상태:** 확정
**목적:** 업무 비용을 입력·검토·승인하고 정산 이력을 보존한다.
**사용자:** 업무 담당자, Finance, 승인자
**시작 조건:** Expense/Settlement Event
**시작점:** Finance Restricted Surface
**완료 상태:** 정산완료/취소

#### 정상 경로

> 비용 입력 → 귀속 Source 확인 → 증빙 확인 → 검토 제출 → 승인 → 지급대기 → 정산완료

#### 대안 경로

- **`O-10-A01`**** 증빙 미첨부:** 경고 후 저장·승인 허용.
- **`O-10-A02`**** 중복 의심:** 경고 후 운영자 확인으로 진행 가능.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-10-E01` | 필수 금액/귀속 오류 | 제출 차단 | 오류 안내 | 수정 | 작성중 |
| `O-10-E02` | 정산 후 정정 | 원본 삭제 금지 | Adjustment 필요 | Correction/Adjustment | 이력 유지 |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Settlement | 작성중 | 검토 제출 | 검토대기 | 담당자 | 검토 대기 |
| Settlement | 검토대기 | 승인 | 승인확정 | 승인자 | 승인 완료 |
| Settlement | 승인확정 | 지급 준비 | 지급대기 | Finance | 지급 대기 |
| Settlement | 지급대기 | 지급/정산 확인 | 정산완료 | Finance | 정산 완료 |

#### 외부 연결 지점

실제 지급/회계 Provider는 Physical Integration 결정 전 Interface Only.

### O-11. 수당·인센티브 처리

**상태:** 부분 확정
**목적:** Eligibility를 판정하고 계산근거·승인을 보존해 지급대상으로 만든다.
**사용자:** Sales/Operations, Compensation, Finance, 승인자
**시작 조건:** 계약 완료 + 설치 완료 + 회사 입금 완료
**시작점:** Compensation Restricted Surface
**완료 상태:** 지급대기

#### 정상 경로

> Eligibility 확인 → Policy Snapshot → 계산 → 영업팀장 검토 → 대표 승인 → 지급대기

#### 대안 경로

- **`O-11-A01`**** 팀장 단독승인:** 대상 항목은 Configuration Pending.
- **`O-11-A02`**** 취소/환불/미수/해지:** 원 이력 삭제 없이 Adjustment/Clawback.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-11-E01` | Eligibility 미충족 | 지급대상 제외 | 미충족 조건 표시 | 조건 충족 후 재평가 | Pending |
| `O-11-E02` | 계산식/비율 미확정 | 고정 계산 금지 | Policy Pending | 정책 확정 후 | Pending |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 비고 |
|---|---|---|---|---|---|
| Compensation | `Not Eligible / Pending` | 계약 완료 + 설치 완료 + 회사 입금 완료 확인 | `Eligible` | 시스템/운영자 | Eligibility 3조건 모두 충족 |
| Compensation | `Eligible` | 영업팀장 검토 + 대표/최종권한자 승인 | `지급대기` | 승인자 | 계산식·비율은 Policy Pending이며 임의 고정 금지 |

정확한 계산 중간 State는 상품/직군별 Policy 확정 전까지 별도 고정하지 않는다.

#### 외부 연결 지점

N/A. 지급 연동은 Finance 영역 Physical Integration 결정 후 연결.

### O-12. 경영 의사결정 기록·실행·복기

**상태:** 확정
**목적:** 주요 경영 Decision을 근거와 함께 기록하고 실행 결과까지 추적한다.
**사용자:** 대표, 위임결정권자, 팀장
**시작 조건:** 운영/재무/인사/상품/정책 Decision 필요
**시작점:** Management Decision Surface
**완료 상태:** 종료/취소

#### 정상 경로

> 메뉴 진입 → 새 기안 → 필수/선택값 입력 → 저장/검토요청 → 권한자 결정 → 실행 Work 연결 → 결과 입력 → 결과검토 → 종료

1. 경영 의사결정 메뉴에 들어간다.
2. `새 기안`을 선택한다.
3. 제목, Decision 유형, 배경/문제, 결정 필요사항을 입력한다.
4. 선택 또는 조건부 정보로 관련 Customer/Store/계약/Case/금액/첨부/희망결정일 등을 연결할 수 있다.
5. `저장` 또는 `검토 요청` Action을 수행한다.
6. 시스템이 필수값, 권한, 현재 상태를 검증한다.
7. 권한자가 `보류 / 반려 / 결정완료` 중 허용된 Action을 수행한다.
8. 결정완료 후 실행이 필요한 경우 실행 Work/담당자를 연결한다.
9. 담당자가 실행 결과와 Evidence를 입력한다.
10. 권한자가 결과를 검토하고 종료한다.

#### 대안 경로

- **`O-12-A01`**** 대표전결:** 대표가 직접 결정완료.
- **`O-12-A02`**** 위임전결:** 설정된 Authority 범위 내 위임자 결정.
- **`O-12-A03`**** 합의·승인:** 필요한 승인/합의를 거쳐 결정완료.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-12-E01` | 필수값 누락 | 검토요청 차단 | 누락 항목 표시 | 입력 보완 | 기안 |
| `O-12-E02` | Decision Authority 없음 | 결정완료 차단 | 권한 없음 | 권한자 Handoff | 검토중 |
| `O-12-E03` | 확정 Decision 변경 필요 | 원본 덮어쓰기 금지 | Revision 필요 | Revision/Supersede | 이력 유지 |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Decision | 기안 | 검토요청 | 검토중 | 작성자 | 검토중 |
| Decision | 검토중 | 결정 | 보류/반려/결정완료 | Decision Authority | 결정 상태 |
| Decision | 결정완료 | 실행 시작 | 실행중 | 담당자 | 실행중 |
| Decision | 실행중 | 결과 제출 | 결과검토 | 담당자 | 결과 검토 |
| Decision | 결과검토 | 종료 | 종료 | 권한자 | 종료 |

#### 외부 연결 지점

N/A.

### O-13. 기존 고객 추가구매·변경 영업

**상태:** 확정
**목적:** 기존 Customer/Store의 요청을 과거 이력과 연결해 신규 Opportunity로 처리한다.
**사용자:** 영업 담당자
**시작 조건:** 기존 Customer/Store 존재
**시작점:** Customer 360
**완료 상태:** Opportunity New/Assigned

#### 정상 경로

> Customer 360 → Store 선택 → 계약/Asset/Case 확인 → 요청 입력 → Opportunity 생성 → 담당자 배정 → 견적 흐름

#### 대안 경로

- **`O-13-A01`**** Store 불명확:** O-01 Match로 분기.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-13-E01` | Store 식별 실패 | 자동 신규생성 금지 | Match 필요 | O-01 | Review |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Opportunity | 없음 | 기존고객 요청 생성 | New/Assigned | 운영자 | 추가상담 진행 |

#### 외부 연결 지점

N/A.

### O-14. 복수 Contract Item 병렬 이행

**상태:** 확정
**목적:** 한 계약의 여러 Item을 독립 진행하며 전체 Fulfillment와 Store Activation을 올바르게 판정한다.
**사용자:** 계약/설치 운영자
**시작 조건:** Contract Item 2개 이상
**시작점:** Contract/Fulfillment Detail
**완료 상태:** 부분완료/완료 + Activation 가능 여부

#### 정상 경로

> Item 분리 → Item별 Readiness/Work → 병렬 진행 → Item별 Completion → Required/Core Item 기준 Activation → 전체 Projection

#### 대안 경로

- **`O-14-A01`**** 특정 Item 보류:** 해당 Item만 보류, 나머지 진행.
- **`O-14-A02`**** 비핵심 Item 지연:** Required/Core Item 완료 시 Store Activation 가능.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-14-E01` | 한 Item Failure | 전체 Contract 실패 금지 | 해당 Item 문제 표시 | Case/Revisit | 부분완료 |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Fulfillment | 진행중 | 일부 Item 완료 | 부분완료 | 시스템 Projection | 일부 완료 |
| Store | Activation 대기 | Required Item 완료 | Active 가능 | 운영자/시스템 Guard | 사용 가능 |

#### 외부 연결 지점

Item별 외부 기사/Vendor는 각각 `P-01/P-02`로 연결한다.

### O-15. AS Escalation

**상태:** 확정
**목적:** 중대·반복·고객영향 장애를 높은 관리 수준으로 처리한다.
**사용자:** CS, AS 담당자, AS팀장
**시작 조건:** Escalation Trigger 충족
**시작점:** Case Detail
**완료 상태:** 해결/종료

#### 정상 경로

> Trigger 확인 → Severity 설정 → 관리자 알림 → 기존 담당자 유지 + AS팀장 공동담당 → 필요 시 재배정/외부 Handoff → 해결 → Close

**Escalation Trigger:** 영업중단, 카드/PG 불가, 핵심기능 전체 불능, 반복장애, 설치 직후 중대장애, 강한 불만/해지 위험, 약속시간 초과, 외부업체 협업 필요, 다수 매장 동시 장애.
**반복장애 기준:** 동일 Store + 동일/유사 증상 + 30일 이내 2회 이상.

#### 대안 경로

- **`O-15-A01`**** 팀장 재배정:** 필요 시 수동 재배정.
- **`O-15-A02`**** 외부업체 필요:** Waiting External + P-02 Handoff.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `O-15-E01` | 반복장애 감지 | Escalation | 반복장애 표시 | AS팀장 공동담당 | Escalated |
| `O-15-E02` | 외부업체 장기대기 | Waiting External | 지연 표시 | Follow-up/재배정 | Waiting |

#### 상태 변화

| 대상 | 이전 상태 | 행동·사건 | 다음 상태 | 변경 주체 | 사용자에게 보이는 표현 |
|---|---|---|---|---|---|
| Severity | 미설정/기존 | Impact 판정 | S1/S2/S3/S4 | 운영자/시스템 보조 | 긴급/높음/일반/낮음 |
| Case | Assigned/In Progress | Escalation | 상태 유지 + Escalated/공동담당 | 운영자/시스템 | 상향 처리 |

#### 외부 연결 지점

Vendor/통신/PG 등 외부협업은 `P-02/P-03`으로 연결한다.

## 6. 시스템 흐름

### S-01. 고객·매장 중복 후보 탐지

**상태:** 확정
**목적:** 잘못된 자동 Merge를 방지하면서 기존 Customer/Store 후보를 제시한다.
**사용자:** 시스템 + 운영자
**시작 조건:** Intake/Opportunity 생성 또는 Match 요청
**시작점:** Match Event
**완료 상태:** Match Candidate / Review

#### 정상 경로

> 식별정보 수신 → 후보 검색 → 후보 제시 → 운영자 확인 → Link

#### 대안 경로

- **`S-01-A01`**** 신규:** 후보가 없으면 Candidate 생성 경로 안내.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `S-01-E01` | 복수/애매 후보 | Auto Merge 금지 | Human Review | 운영자 판정 | Review |
| `S-01-E02` | 검색 timeout | 결과 확정 금지 | 재시도 | 재검색 | Pending |

#### 상태 변화

Match 결과는 Candidate/Review 상태를 만들지만 Human Review 전 불명확한 Entity를 자동 Merge하지 않는다.

#### 외부 연결 지점

Shared Person/Merchant Master는 Logical Reference만 사용하며 Physical 구현은 Common Infrastructure Pending.

### S-02. Commercial Policy Snapshot

**상태:** 확정
**목적:** 실제 적용된 Policy Version과 계산근거를 불변 이력으로 보존한다.
**사용자:** 시스템
**시작 조건:** Quote/Contract/Commission에 Policy 적용 필요
**시작점:** Policy Resolve Event
**완료 상태:** Snapshot Saved

#### 정상 경로

> Approved+Effective Version 선택 → Rule 평가 → resolved value 계산 → Snapshot 저장 → Source 연결

#### 대안 경로

- **`S-02-A01`**** 정책 예외:** Approval이 필요한 Source Flow로 Handoff.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `S-02-E01` | Effective Version 없음 | 적용 차단 | 정책 없음 | 정책 승인 후 재시도 | Blocked |
| `S-02-E02` | Formula Error | 적용 차단 | 계산오류 | 신규 Version 수정 | Blocked |

#### 상태 변화

Snapshot 생성 후 이후 Policy Version 변경으로 기존 Snapshot을 덮어쓰지 않는다.

#### 외부 연결 지점

N/A.

### S-03. Contextual AI Operations Assistant

**상태:** 확정
**목적:** 현재 업무 Context를 바탕으로 요약·초안·다음 Action을 제안하되 중요한 Commit은 Human Confirm을 요구한다.
**사용자:** 권한 있는 내부 사용자
**시작 조건:** AI Assistant 호출
**시작점:** Customer/Store/Quote/Contract/Case Context
**완료 상태:** Draft 또는 Human-confirmed Domain Command

#### 정상 경로

> Context Load → AI Suggest/Draft → User Review → Human Confirm → Permission/Guard 재검증 → Domain Command → Audit

#### 대안 경로

- **`S-03-A01`**** 제안만 사용:** Commit 없이 Draft 종료.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `S-03-E01` | Restricted Field 접근 | 차단 | 접근불가 | 권한 범위 재요청 | No Change |
| `S-03-E02` | Human Confirm 없음 | Commit 금지 | 확인 필요 | 사용자 확인 | Draft |
| `S-03-E03` | Domain Guard 실패 | Command 실패 | 실패사유 | 조건 보완 | No Change |

#### 상태 변화

AI 제안 자체는 Domain State를 변경하지 않는다. Human Confirm과 기존 Domain Guard 통과 후에만 변경된다.

#### 외부 연결 지점

AI Provider Physical 선정은 Pending. Provider가 Domain Permission을 우회할 수 없다.

### S-04. Queue·Notification 생성

**상태:** 확정
**목적:** 상태 변화나 기한 Event를 업무 Queue와 필요 알림에 반영한다.
**사용자:** 시스템
**시작 조건:** 업무 Event/상태 변화/기한 도래
**시작점:** Domain Event
**완료 상태:** Queue/Notification Projection 반영

#### 정상 경로

> Event 수신 → 대상/권한 계산 → Queue 갱신 → 필요한 경우 Notification 생성 → Source Entity 이동 가능

#### 대안 경로

- **`S-04-A01`**** Notification 불필요:** Queue만 갱신.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `S-04-E01` | Notification 실패 | Business Transaction Rollback 금지 | Queue에서 확인 | 재전송/운영확인 | Source 상태 유지 |
| `S-04-E02` | Projection 지연 | Source of Truth 변경 금지 | 재조회 | Projection 재계산 | Source 상태 유지 |

#### 상태 변화

Queue/Notification은 Projection이며 Source Entity의 상태를 대신하지 않는다.

#### 외부 연결 지점

Message/Push Provider가 사용될 수 있으나 실제 Provider는 별도 Integration 결정.

## 7. 협력사 흐름

### P-01. 외부 기사 설치·현장 작업

**상태:** 확정
**목적:** 외부 기사가 Assigned Work를 수행하고 결과/Evidence를 OC로 반환한다.
**사용자:** 외부 설치기사/AS 기사
**시작 조건:** Work Assignment
**시작점:** 외부 기사 Work View/안내
**완료 상태:** 결과 반환 + 내부 Verification

#### 정상 경로

> Assignment 확인 → 일정/주소 확인 → 현장 수행 → 결과/Evidence 입력 → 제출 → OC 검증 → 내부 State 반영

#### 대안 경로

- **`P-01-A01`**** 일정 변경:** 운영자와 재일정.
- **`P-01-A02`**** 부분완료:** Partial + Revisit 요청.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `P-01-E01` | Timeout/결과불명 | 내부 성공상태 변경 금지 | 확인 필요 | 재조회/수동확인 | Waiting |
| `P-01-E02` | 작업 실패 | Failure Event | 재처리 | 재배정/Revisit | Failed/Waiting |

#### 상태 변화

외부 제출은 내부 Verification 전 `Verified Complete`를 보장하지 않는다.

#### 외부 연결 지점

기사용 외부/모바일 Surface와 OC Work Item을 Work ID로 연결한다.

### P-02. Vendor·제조사 배송/AS 처리

**상태:** 확정
**목적:** Vendor/제조사 요청을 OC의 Inventory/Case와 연결하고 결과를 추적한다.
**사용자:** Vendor/제조사 담당자
**시작 조건:** 발주·배송·수리·교체·외부 AS 요청
**시작점:** Vendor Request
**완료 상태:** 결과 수신/Waiting/Failed

#### 정상 경로

> 외부 요청 생성 → Vendor Reference 기록 → 진행상태 추적 → 결과 수신 → 내부 운영자 확인 → Source 상태 반영

#### 대안 경로

- **`P-02-A01`**** 직배송:** Inventory 입고 없이 Shipment 추적.
- **`P-02-A02`**** 장기대기:** Waiting External 유지 + Follow-up.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `P-02-E01` | Vendor 결과 없음 | 성공 확정 금지 | 외부대기 | Follow-up | Waiting |
| `P-02-E02` | 반품/교체 | 원 이력 보존 | 반품/교체 표시 | 새 Transaction/Shipment | Exception |

#### 상태 변화

Vendor 상태는 OC Source Entity와 분리해 기록하고 내부 확인 후 필요한 State를 반영한다.

#### 외부 연결 지점

Vendor API가 없는 경우 Manual Reference/Status Update 방식도 허용한다.

### P-03. 외부 Provider 발송·전자서명·Callback

**상태:** 확정
**목적:** 외부 Provider 요청의 성공·실패·결과불명을 OC Business State와 안전하게 연결한다.
**사용자:** 시스템/외부 Provider
**시작 조건:** Quote Send, e-sign 등 외부 Command
**시작점:** Provider Request
**완료 상태:** Success / Failure / Unknown

#### 정상 경로

> 요청 생성 → Provider Reference 저장 → 응답 수신 → 성공조건 검증 → 내부 State 반영 → Audit

#### 대안 경로

- **`P-03-A01`**** 비동기 callback:** callback 수신 후 동일 검증.
- **`P-03-A02`**** 수동 확인:** 조회 기능이 없으면 운영자 확인 후 반영.

#### 예외·복구

| ID | 실패·중단 조건 | 시스템 처리 | 사용자 안내 | 복구·재시도 | 최종 상태 |
|---|---|---|---|---|---|
| `P-03-E01` | Timeout | 성공 단정 금지 | 확인 필요 | 재조회/재시도 | Unknown |
| `P-03-E02` | 중복 callback | Idempotency | N/A | 기존 결과 재사용 | 기존 상태 |
| `P-03-E03` | 응답 순서 역전 | 최종 Business Guard 확인 | 운영 확인 가능 | 대사/수동확인 | Pending/기존 상태 |

#### 상태 변화

외부 성공 응답만으로 내부 Permission/Business Guard를 우회하지 않는다.

#### 외부 연결 지점

실제 Provider/Endpoint/Schema는 Integration 단계에서 확정한다.

## 8. 공통 Handoff 규칙

| From | To | 전달 내용 | 완료 기준 |
|---|---|---|---|
| OSP/외부채널 | OC Intake | Lead, Source, Request | OC 수신 Trace + Intake Accepted |
| C-01/O-01 | O-02 | Customer/Store Context, Opportunity | Opportunity 생성·연결 |
| O-02/O-03 | O-04 | 요구사항, 담당자, 상담이력 | Quote Ready |
| O-04/C-02 | O-05 | Accepted Revision, Policy Snapshot | Accepted Revision 확인 |
| O-05 | O-06 | Contract, Contract Items | Contract Signed |
| O-06 | O-07 | Work, Schedule, Assignment | Work Scheduled |
| O-06/O-07 | O-08 | Material Requirement | 재고/자재 필요 |
| O-07 | O-09 | Failure/Issue Context | Case 생성 |
| O-09 | O-13 | 추가구매/교체 후보 | Opportunity Candidate |
| O-10/O-11 | Finance | 승인/지급 대상 | Approval 완료 |

## 9. 공통 상태·복구 원칙

1. 중요한 State 변경은 화면 이동만으로 발생하지 않는다.
2. Domain Command + Permission + Guard를 통과해야 한다.
3. 외부 Provider 실패/timeout/unknown이면 성공 State를 먼저 반영하지 않는다.
4. 중요 History는 삭제/덮어쓰기보다 Revision/Correction/Adjustment를 사용한다.
5. Waiting은 Complete/Closed가 아니다.
6. Notification 실패는 Business Transaction 성공과 분리한다.
7. 중복 Command는 Idempotency Guard를 적용한다.
8. Customer 360/Today/Queue/Dashboard는 Projection이며 Source of Truth가 아니다.

## 10. Business Rule 연결

상세 Field / Required·Optional·Conditional / Validation / Permission / Notification / External Integration / Acceptance Criteria는 `[OC] Detailed Requirements & Business Policies`를 기준으로 한다.

## 11. 현재 Pending

### Product / Policy Pending

- FLOW-007 상품/직군별 계산식
- FLOW-007 상품/직군별 수당 비율
- FLOW-007 항목별 영업팀장 단독승인 범위

### Common Infrastructure Physical Pending

- Shared Person Master Physical Implementation
- Shared Merchant Master Physical Implementation
- Shared IAM Physical Implementation
- Shared Device / Asset Master Physical Implementation

위 Pending은 임의 하드코딩하지 않는다.

## 12. Template Coverage Self-Audit

| 검수 항목 | 결과 |
|---|---|
| Flow Inventory | C 7 / O 15 / S 4 / P 3 = 29 |
| 상태/목적/사용자/시작조건/시작점/완료상태 | PASS |
| 정상 경로 | PASS |
| 대안 경로 | PASS 또는 N/A |
| 예외·복구 | PASS |
| 상태 변화 | PASS 또는 명시적 N/A/설명 |
| 외부 연결 지점 | PASS 또는 N/A |
| 확정/부분확정/Pending 구분 | PASS |
| Physical 미확정 임의 확정 방지 | PASS |
| Raw HTML Table 사용 | 0 |
| Claude PM3 Independent Audit | COMPLETED — PASS WITH MINOR / MINOR 4건 보정 반영 (2026-08-18) |
| Developer Review | READY TO REQUEST — 공식 Pending 명시 전제 |

**문서 상태:** Developer Template Aligned — CLEAN CANDIDATE / 개발자 검토 전 승인 아님.

## 40. Latest SOT Supplemental Flow Coverage — 2026-08-21

본 Section은 기존 29개 Canonical Trace Set을 삭제·재번호하지 않고, 2026-08-21 이후 확정된 Owner Direction 및 Cross-Service 정합성 결과를 최신 Flow 해석 기준으로 연결한다.

### 40.1 Multi-Entry / Single OC Intake

고객·가맹점 Request의 Entry Surface는 복수일 수 있다.

- PayPlay OSP
- PayPlay Business OS
- Kakao / CS Channel
- External Form
- Partner Channel

실제 내부 처리가 필요한 Request의 Operational Master는 **OC Unified Intake**로 단일화한다.
기준 흐름:
`Source Surface → Request → OC Unified Intake → Customer/Store Match → Request Type → Owner Domain Route → Task/Case/Work → Status/Result → Source Surface Projection`
OC Intake는 최소 Source Channel / Request Type / Customer / Store / Payload·Attachment / Consent / Correlation ID를 식별·보존한다.
조회·다운로드·FAQ·정상 Self-Service처럼 실제 내부 처리가 발생하지 않는 행위는 OC Request를 생성하지 않는다.

### 40.2 Contract Document Self-Service

정상 경로는 Business OS 로그인 → Contract 조회 → 체결 전자계약서 보기/다운로드이다. 정상 다운로드는 신규 OC Request를 만들지 않는다.
문서 누락·권한확인·조회실패·특수 재발급 등 사람이 처리해야 하는 예외만 `CONTRACT_COPY_REQUEST`로 OC Unified Intake에 진입한다.
Contract / Document Source State는 Contract Domain이 소유하고 Self-Service 화면은 Projection / Access Surface로 동작한다.

### 40.3 Sales Data Self-Service

장기 정상경로는 Business OS에서 Store/기간/자료유형을 선택하고 VAN·PG·여신계 Source를 조회하여 Download 또는 Fax 발송하는 것이다.
기존 KOVAN API 자산은 Reuse First 대상으로 보존한다. KIS / 추가 VAN / PG / 여신계 Provider 세부 구현은 Integration Pending이다.
데이터 미수집·권한 오류·특수 증명·Source 장애처럼 수동 처리가 필요한 경우에만 `DOCUMENT_SALES_DATA` Assisted Request가 OC Unified Intake로 전환된다.

### 40.4 Shipment / Carrier

Shipment는 Inventory & Supply 영역의 배송 Source State를 소유한다.
`Order/Contract Item → Allocation/Preparation → Shipment → Carrier/Tracking → Delivered / Return / Exchange / Reship`
Customer 360, Contract/Fulfillment 및 Business OS 고객 화면은 필요한 Shipment 상태를 Projection하며 별도 배송 원장을 만들지 않는다.

### 40.5 Customer Operational Messaging

계약·영업방문·설치·AS·배송 등 Source Domain의 Event를 기준으로 Kakao/SMS 등 고객 안내를 자동 또는 반자동 발송할 수 있다.
`Source Event → Recipient → Template/Draft → Channel → Auto/Semi-auto Send → Delivery Result → Audit`
메시지는 업무 상태를 소유하지 않는다. Contract / Case / Shipment / Schedule이 각각 Source State를 소유한다.

### 40.6 Schedule / Meeting

Schedule은 공통 Collaboration Capability다.
영업 방문, 설치 일정, AS 방문 등 Source Workflow에서 시간 약속이 확정되면 Schedule Projection을 생성·갱신한다. 동일 일정을 여러 Domain에서 중복 입력하지 않는다.

- Schedule = 시간 약속
- Queue = 처리할 일
- Notification = 변화 알림
- Source Domain = 실제 업무 상태

내부/외부 Meeting 및 회사 일정은 Schedule 자체에서 생성 가능하되, Domain 업무 일정은 원 Source와 연결되어야 한다.

### 40.7 Vehicle / Parking

Vehicle과 Parking은 Owner Decision으로 OC Target에 포함된 **Company Operations** Capability다.

- Vehicle: 차량 기본정보, 소유/임대, 담당/운전자, 운행, 주유/충전, 점검·정비, 보험·검사, 사고/수리, 비용, History
- Parking: 직원/차량, 지점/주차장, 정기·임시·방문, 기간, 비용, 회사/개인 부담, 변경 History

기존 29개 Flow ID에 대응되는 공식 독립 ID는 아직 생성하지 않는다. `Company Operations & Schedule Minimal Spec v0.1`을 Supplemental Flow Source로 사용하며 Screen ID normalization도 Pending으로 유지한다.

### 40.8 O-15 해석 고정

`O-15` 중대·반복 장애 Escalation은 별도 메뉴 또는 독립 Case Core가 아니라 `O-09 CS·AS 해결`의 Escalation Subflow로 해석한다. 기존 ID는 Trace 호환성을 위해 보존한다.

### 40.9 개발자 해석 Guard

- 기존 29개 ID = Canonical Trace Set, 최신 OC 전체 Capability 개수 아님
- 신규 SOT를 반영하기 위해 임의 Flow ID를 생성하지 않음
- Self-Service 정상경로와 OC Assisted Request를 구분
- Multi-Entry라도 Operational Request Master는 OC Unified Intake 하나
- Projection / Queue / Notification / Messaging이 Source Domain State를 복제 소유하지 않음
- Vehicle / Parking / Schedule Screen ID는 별도 normalization 전까지 명칭 기반 Family로 추적

**Supplemental Flow Sync Verdict:** PASS — 기존 Flow 구조 유지, 최신 SOT Coverage 보강 완료. Physical Provider/API/DB 및 신규 Screen/Flow ID normalization은 별도 Pending.

## Developer Package Navigation

공식 Reading Order: `#1 Architecture → #2 Flow → #3 Rule → #4 Screen`

- **#1 Service Architecture / Menu & Depth:** [SERVICE_ARCHITECTURE_MENU_DEPTH.md](../07_ARCHITECTURE/SERVICE_ARCHITECTURE_MENU_DEPTH.md)
- **#2 현재 문서:** User & Operations Flows
- **#3 Detailed Requirements & Business Policies:** [DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md](../05_REQUIREMENTS_POLICIES/DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md)
- **#4 Screen & Navigation / Traceability:** [SCREEN_NAVIGATION_TRACEABILITY.md](../08_SPECIFICATIONS/SCREEN_NAVIGATION_TRACEABILITY.md)
- **Package Guide:** [DEVELOPER_PACKAGE_GUIDE.md](../DEVELOPER_PACKAGE_GUIDE.md)

이 문서는 업무 목적·Actor·상태변화·Handoff를 설명한다. 기능 위치는 #1, 세부 Rule/Validation/Permission은 #3, 실제 Screen 구현 위치는 #4를 기준으로 한다.

## Cross-Audit Clarification — Customer Messaging Flow Trace

Claude PM3 Independent Cross-Audit의 `MINOR-01`을 반영한다.

- Customer Operational Messaging은 기존 Canonical C/O/S/P 29개 Flow에 독립 Flow ID를 추가하지 않는다.
- §3.2 흐름 요약 Table은 기존 Canonical Trace Set이며 최신 모든 Supplemental Capability의 총 목록이 아니다.
- Customer Messaging은 `Contract / Schedule / Case / Shipment Source Event → Communication Layer → Customer Delivery Result / Failure / Audit`로 동작하는 Supplemental Cross-Service/System Flow다.
- 따라서 Table만 참조할 경우에도 Messaging이 누락된 것으로 해석하지 않으며, 상세 Trace는 최신 Supplemental Flow Coverage 및 Operational Self-Service & Communication Integration Minimal Spec을 함께 본다.
- Message 전달 성공은 Source Business State 완료를 의미하지 않는다.

**Cross-Audit Resolution:** `MINOR-01 CLOSED / NON-BLOCKING / NO NEW FLOW ID`

## 41. Workforce Service Desk Supplemental Flows — 2026-08-21

> 기존 29개 Flow ID는 유지하며 renumber하지 않는다. 본 섹션은 최신 Owner Decision에 따른 Supplemental Flow다.

### WSD-C-01 — Internal Worker Self-Service (내부 재직자 본인조회)

**Actor:** 재직 내부직원 / 제한형 OC 계정을 가진 외근·내외근 영업직·프리랜서·외부기사
`OC 로그인 → Workforce Service Desk → 본인 Scope 확인 → 급여/수당/Commission/정산/발행문서 조회 → 필요 시 Download → 이견·수정이 필요할 때만 Request 생성 → Unified Intake Routing`
**Guard**

- 조회 가능한 확정 데이터는 Request를 만들지 않는다.
- 본인 Scope 밖의 HR/Finance/Compensation 데이터는 열람할 수 없다.
- 이미 발행된 명세서/확정 수당/지급내역은 Self-Service 우선.

### WSD-C-02 — External / Former Worker Public Entry (외부·퇴사자 공개진입)

**Actor:** OC 계정 없는 외부직원·퇴사자·해촉자
`OC Workforce Service Desk Public Entry → 최소정보 입력 → 기존 Shared Person/Worker 기록 Match → 기존 등록 휴대폰/이메일로 One-time Secure Link 시스템 자동 발송 → 추가정보 Match → identity_verified = true → accessible_scope 산정 → 본인 조회 또는 Request 생성 → Secure Result / Document Delivery`
**Exception / Recovery**

- Identity Match 실패, 등록 연락처 변경/소실, Legacy 정보 불완전 → `MANUAL_VERIFICATION_REQUIRED` Queue
- 직원의 수동 Secure Link 발송/재발송은 위 예외에서만 허용
- 반복 인증 실패 → Security Config에 따른 제한 후 Manual Verification

**Security Guard**

- 입력한 신규 연락처로 즉시 발송하지 않는다. 기존 등록 연락처를 사용한다.
- Secure Link는 1회성·만료형이다.
- 인증 전 급여·수당·정산·HR 문서를 노출하지 않는다.
- 민감문서 Public URL / 장기 CDN Cache 금지.

### WSD-O-01 — Workforce Request Operator Processing (담당자 처리)

`Unified Intake 수신 → requester_type / identity_verified / accessible_scope 확인 → Request Type 분류 → HR / Compensation / Finance Owner Queue → 필요 시 Approval → 결과 생성 → Secure Result / Signed Download Link 전달 → Request Close → Audit`
**Routing**

- HR 문서 / 재직·퇴직 관계 → HR
- 수당 / Commission → Compensation
- 급여 / 지급 / 정산 / 세무자료 → Finance
- Entry / Request Routing / History → Workforce Service Desk / Unified Intake

### Unified Intake Extension

- Source Channel 추가: `Workforce Service Desk Public Entry`
- Request Envelope 추가 필드: `requester_type`, `identity_verified`, `accessible_scope`
- Request Type Candidate: `PAYSLIP`, `SETTLEMENT_INQUIRY`, `COMMISSION_INQUIRY`, `CERTIFICATE`, `TAX_DOCUMENT`, `CONTRACT_DOCUMENT`, `PERSONAL_INFO_CORRECTION`, `GENERAL_HR`

### Flow Implementation Boundary

- Secure Link TTL / Retry Count / Lockout 시간은 Security Config.
- SMS/Email Provider, token persistence, Signed URL 구현은 Physical Binding Pending.
- Flow / Routing / Security Boundary는 **CLOSED**.

## Human Handoff Supplemental — Finance / Receivable Flow Closure — 2026-08-21

기존 `O-10 비용·정산` Canonical Flow ID는 유지하며 아래 Finance Subflow를 추가 Trace로 사용한다.
`Charge / Contract Obligation → Billing → Receivable → Payment / Adjustment / Write-off Reference → Balance → Closed`
운영 Guard:

- Charge와 Billing은 1:1 고정관계가 아니다. 분할청구 및 통합청구를 허용할 수 있도록 Logical 관계를 N:M 가능 구조로 취급한다.
- Billing Issued와 Payment Received를 동일 상태로 취급하지 않는다.
- Receivable은 Settlement의 Substate가 아니라 별도 Logical Entity다.
- Receivable이 `OPEN`이고 `due_at`이 경과했으며 미수잔액이 0보다 크면 시스템 판정으로 `OVERDUE`가 된다. 담당자의 수동 상태변경으로만 처리하지 않는다.
- Settlement는 기대금액/실제금액/대사 결과를 다루며 Receivable 원장을 소유하지 않는다.
- VAT / 원천세 / 계정과목 / 회계분개 / Bank Matching Physical 구현은 Finance/Accounting Integration 범위로 유지한다.

이 Supplemental은 신규 Canonical Flow ID를 생성하지 않으며 기존 O-10 Finance Flow의 Human Handoff 해석을 보완한다.

## Human Handoff Cross-Audit Round 1 Corrections — 2026-08-21

Claude PM3 독립 Cross-Audit REVISE-B01 / GAP-B01 / GAP-B02 반영.

### O-11 Compensation State Guard

`Eligible`은 즉시 `지급대기`를 의미하지 않는다. Logical 처리 순서는 아래와 같다.
`Eligible → Calculation Candidate → Review Pending → Approval Pending → Finalized Compensation → Payment / Settlement Link`

- 실제 UI State Enum은 별도 Physical/Config 단계에서 정규화할 수 있으나 위 논리 단계를 생략해 구현하지 않는다.
- Policy Snapshot은 계산 시점 기준으로 고정하고, 이후 Policy 변경만으로 과거 Finalized Compensation을 자동 재계산하지 않는다.

### WSD accessible_scope Guard

- Internal Worker와 Limited/External Worker의 Self-Service는 모두 `본인 데이터 only`가 기본이다.
- 타인 급여/수당/정산/문서/요청이력 조회는 허용하지 않는다.
- Role별 세부 Self-Service 범위는 IAM/Permission Config에서 관리한다.
- 제한형 계정은 허용된 Request Type / Document Type / Data Category만 노출한다.
- Config 미확정 상태에서 개발자가 임의로 범위를 넓히지 않는다.

### MANUAL_VERIFICATION_REQUIRED Operator Flow

`WSD-C-02 → MANUAL_VERIFICATION_REQUIRED` 발생 시:
`Manual Verification Queue → Authorized Operator Review → Approved Evidence Match → Verified / Rejected → 최소 accessible_scope 산정 → 정상 WSD 흐름 복귀 또는 종료`

- 담당자의 임의 Identity Override 금지.
- 확인 근거, Actor, 일시, 결과, Scope를 Audit으로 남긴다.
- 연락처 변경 등 예외는 검증 완료 전 Secure Result/민감정보 접근을 허용하지 않는다.
- 정확한 허용 Evidence 종류와 재시도/잠금 수치는 Security Operations Config Pending.

Verdict: REVISE-B01 / GAP-B01 / GAP-B02 CLOSED AT LOGICAL/HUMAN-HANDOFF LEVEL.

---

## Intake Note — 2026-08-21 (Final SOT Resync)

- 본 문서는 Notion Developer Package Document #2의 **Final SOT Freeze 판본**을 GitHub에 Resync한 것이다. 직전 입고본(중간 Snapshot)은 커밋 `77e655d`로 보존된다.
- Resync 반영분: `FINAL SOT FREEZE` 블록 · §41 Workforce Service Desk Supplemental Flows(`WSD-C-01`, `WSD-C-02`, `WSD-O-01`) · Human Handoff Supplemental — Finance/Receivable Flow Closure · Human Handoff Cross-Audit Round 1 Corrections(O-11 Compensation State Guard · WSD accessible_scope Guard · MANUAL_VERIFICATION_REQUIRED Operator Flow · Unified Intake Extension · Flow Implementation Boundary).
- **기존 29 Canonical Flow ID(C 7 / O 15 / S 4 / P 3)는 삭제·재번호하지 않았다.** WSD Flow는 별도 `WSD-*` 식별자로 추가되어 Canonical Set과 충돌하지 않는다.
- 기존 `PP-OC-FLOWS-001`은 SUPERSEDED 상태를 유지하며 본문은 계속 보존된다.
- Header Status는 Notion 원문을 유지했고 `APPROVED` / `Source of Truth YES`로 승격하지 않았다.
- Pending 값은 임의 확정하지 않았다.
