# Detailed Requirements & Business Policies — PayPlay OC

| 항목 | 내용 |
|------|------|
| Document ID | PP-OC-REQS-001 |
| Product / Service | PayPlay OC |
| Document Type | Detailed Requirements & Business Policies |
| Status | WORKING |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-15 |
| Source of Truth | YES |
| Development Use | Policy 기준선. Development Ready / QA Ready 선언문서 아님 |
| Notion Source | https://app.notion.com/p/3bc53327fb8681449e1be8af801b869c |
| Related Decision | DECISION_REGISTER.md |
| Supersedes | — |

> ✅ PayPlay OC의 최종 Detailed Requirements & Business Policies 통합문서.
> Recovery Source, Main PM Shared Entity Decision, 최종 User & Operations Flow,
> Permission/State/Commercial Policy/Migration/Security Architecture를 통합한 Final Documentation Candidate다.
> **Development Ready / QA Ready 선언문서는 아니다.**

---

## 1. Document Scope

본 문서는 PayPlay OC의 기능 요구사항과 Business Policy를 다음 기준으로 정의한다.

- Customer / Sales / Quote / Contract / Fulfillment / Installation / CS / AS
- Product / Commercial Policy / Approval
- Inventory / Purchase / Shipment / Asset
- Finance / Settlement / Compensation / Management Decision
- Work Queue / Today / Dashboard / Team Chat / AI
- Permission / Row Scope / Field Masking / Audit
- State / Transition / Exception / Notification
- Legacy Migration / Identity Resolution / Credential Isolation / Data Quality
- OC ↔ Business OS ↔ OSP 서비스 경계

본 문서는 기존 Reality와 승인 Decision을 통합한 최종 정책 문서이며, 미확정 사항은 명시적으로 Pending으로 남긴다.

---

## 2. Authority & Decision Baseline

### Decision

- **Customer Account** = 동일 실질 운영관계로 PayPlay가 통합 관리하는 고객그룹.
- **Store** = 실제 서비스·설치·운영·AS가 발생하는 사업장 단위.
- **Store 양도양수 Identity** = 동일 장소·운영 연속성 유지 시 기존 Store ID 유지 후보, 타지역 이전은 신규 Store 우선, 애매하면 Human Review.
- **Legal Entity** = Store에 단일 고정값으로 두지 않고 역할·기간별 Assignment History로 관리.
- **Product / Commercial Policy Master Owner** = OC.

### External Dependency / Pending

- Person Master 물리 위치
- Merchant Account 최종 구조
- Shared IAM 물리 Architecture

이 3개는 논리 Reference로만 사용하고 물리 DB/Table/Repository를 확정하지 않는다.

---

## 3. Core Business Entity Requirements

### Customer Account

- 여러 Store를 하나의 실질 운영관계로 집계할 수 있어야 한다.
- 계약·세금·PG·정산의 법적 주체로 사용하지 않는다.
- Customer 360에서 Store별 개별 상태와 그룹 전체 상태를 함께 볼 수 있어야 한다.

### Store

- Opportunity, Quote, Contract, Case, Asset, Activity의 업무 기준점이 될 수 있어야 한다.
- Store Identity는 외부 TID/MID/사업자번호가 아니라 불변 내부 ID를 사용한다.

### Legal Entity Assignment

최소 관계유형:

- BUSINESS_REGISTRATION_HOLDER
- CONTRACTING_PARTY
- BILLING_PARTY
- PG_MERCHANT_PARTY
- SETTLEMENT_PARTY

각 관계는 유효기간과 Source/Evidence를 보존해야 한다.

### Person / Contact

- 대표자·실질운영자·직원·배우자·자녀·회계·현장 담당자 등 여러 Contact를 Store/Customer Account에 연결할 수 있어야 한다.
- 단, Person Master의 물리 Owner/DB는 Common Infrastructure Pending이다.

---

## 4. Customer 360 Requirements

OC는 Customer 360을 거대 단일 Master Table이 아닌 Aggregate Projection으로 제공해야 한다.

필수 조회영역:

- Customer Account Summary
- Store List / Store별 상태
- Contact / Person Reference
- Opportunity / Quote / Contract
- Product / Device / Service
- Installation / Fulfillment
- Case / CS / AS
- Billing / Settlement Summary 권한 범위
- Activity Timeline
- Document / File
- Approval / Exception
- 다음 Action / Queue

Customer 360에서 수정된 데이터는 해당 Source Domain을 통해 저장해야 하며 Projection을 직접 Source of Truth로 사용하지 않는다.

---

## 5. Sales / Opportunity Requirements

- OSP Lead, 외부영업, 기존 고객 추가구매, 재문의는 Opportunity/Request 구조로 수용할 수 있어야 한다.
- Lead Source와 OC의 영업 실행 State를 분리한다.
- 담당자 배정, 상담, 방문, 후속연락, 보류, 거절, 계약전환을 기록한다.
- 외부 영업은 Assigned Row Scope 중심으로 제한한다.
- 상담/방문/메시지/통화는 Activity Event로 기록한다.
- 동일 Customer Account/Store 중복 후보를 확인한 후 신규 생성 또는 기존 관계에 연결한다.

---

## 6. Quote Requirements & Policy

- Quote와 Quote Revision을 분리한다.
- 발송된 Revision은 과거 이력으로 불변 유지한다.
- Quote 작성 시 승인된 Commercial Policy Version을 사용한다.
- Product, Quantity, Price, Installation Fee, Contract Term, PG/Rate, Discount, Promotion, Exception을 Revision에 Snapshot한다.
- 기준 밖 할인·마진·수당·계약조건은 Approval Request를 거쳐야 한다.
- Quote Accepted와 Contract Signed는 별도 Business State다.
- 이후 Policy 변경이 기존 Quote Revision을 소급 변경해서는 안 된다.

---

## 7. Contract Requirements & Policy

- Contract Header와 Contract Item을 분리한다.
- Contract 1:N Contract Item을 허용한다.
- POS, Table Order, Kiosk, CCTV, Internet, Printer 등 상품/서비스별 이행을 Item 단위로 추적한다.
- Contract Signed와 Fulfillment Complete를 분리한다.
- 계약 상태와 설치팀 Workflow 상태를 하나의 필드로 합치지 않는다.
- Accepted Quote Revision이 있는 경우 Contract의 상업조건 Source로 연결한다.
- 계약 당시 Legal Entity Assignment와 Applied Commercial Policy Snapshot을 보존한다.
- 계약 변경/해지/양도양수는 원본 계약을 덮어쓰기보다 Revision/Amendment/관련 Event 이력을 남긴다.

---

## 8. Fulfillment / Installation Requirements

- Contract Item별 Fulfillment Requirement를 생성할 수 있어야 한다.
- 설치 주소, 일정, Contact, Required Document, Product/Asset, Inventory Dependency, Vendor Dependency를 확인한다.
- 담당자/외부기사 Assignment를 지원한다.
- 설치 완료 시 장비/Serial/Service Instance를 Store와 Contract Item에 연결한다.
- 설치사진·고객확인·예외·재방문 필요사항을 기록한다.
- Item별 완료와 전체 계약 이행완료를 분리한다.
- 실패·재방문·일정변경은 별도 Workflow State/Event로 기록한다.

---

## 9. Case / CS / AS Requirements

- 단순 문의와 추적이 필요한 Case를 구분한다.
- Case는 Store/Customer Account/Contract/Asset과 연결할 수 있어야 한다.
- 원격지원, 현장방문, 제조사/Vendor AS를 Work Item으로 분리할 수 있어야 한다.
- Case Close와 Work Item Complete는 별도 State다.
- AS 비용 발생 시 승인된 CS/AS Fee Policy를 적용한다.
- 장애 원인, 처리 결과, 재발방지 정보, 고객 확인을 기록한다.
- 기존 CMS 장문 메모 방식 대신 통화/메시지/Action/Event를 구조화한다.

---

## 10. Product / Service Master Requirements

- Product/Service의 정체성, Category, Variant, SKU, 운영속성을 관리한다.
- Price, Fee, Commission, PG Rate, Contract Rule을 Product Master 자체에 혼합하지 않는다.
- Legacy Alias를 Canonical Product/Service와 분리한다.
- Owner Fact 기준 수량 약어:
  - `P{n}` = POS n개
  - `T{n}` = 테이블오더 n개
  - `K{n}` = 키오스크 n개
  - `NFC{n}` = NFC 오더 n개
  - `QR{n}` = QR 오더 n개
  - `CC{n}` = CCTV 카메라 n대
- `인8`은 인터넷 8개가 아니라 월 8,000원 의미이므로 동일 Parser Rule을 적용하지 않는다.
- `배4`는 배달앱 4개 가입 의미다.

---

## 11. Commercial Policy Requirements

Commercial Policy는 OC Master로 관리한다.

정책영역:

- Product / Service Price
- Installation / One-time / Monthly Fee
- PG / Revenue Share
- Sales Commission
- CS / AS Fee
- Contract / Fulfillment Rule
- Promotion / Discount
- Subscription / Offer

구조 원칙:

`Commercial Policy → Policy Version → Policy Rule / Formula → Approval → Effective Version → Applied Policy Snapshot`

- Formula Error가 남은 Version은 Approval 제출 금지.
- `수정 중 / 미작성 / 확인 필요` Source는 자동 Effective 금지.
- 승인된 Effective Version 직접 수정 금지. 변경은 신규 Version 생성.
- Quote/Contract/Commission에 적용된 당시 Version을 Snapshot한다.
- 사후 정책 변경으로 과거 견적·계약·수당을 자동 변경하지 않는다.

---

## 12. Marketing Subscription 1/2/3 Policy

Legacy `PP1/PP2/PP3`는 Hardware Product가 아니라 Service Subscription / Commercial Offer 계열이다.

Display Name:

- 마케팅 구독 1
- 마케팅 구독 2
- 마케팅 구독 3

현재 상태:

- 과거 PG 수수료 연계 마케팅 서비스 제공안의 구독 개념이 존재했음.
- 현재 그대로 사용하지 않음.
- 향후 마케팅 + 경영지원 Tier로 재기획 필요.
- 가맹점 월 매출의 약 1~3% Revenue Share 방향은 Proposal이며 정확 요율/혜택/최소·최대/PG 연계는 Pending.
- 신규 Effective Version 승인 전 Quote/Contract에 자동 적용 금지.

---

## 13. Approval Requirements

Approval은 Source Business Object를 대체하지 않는 공통 Workflow다.

- Source Entity 1:N Approval Request 허용.
- Source Business State와 Approval State를 분리한다.
- 할인·마진·수당·비용·정책·예외계약 등 승인 대상은 Domain Policy에서 정의한다.
- 요청자와 승인자 분리 Candidate를 유지한다.
- 승인·반려·수정요청·철회·만료 이력을 Audit한다.
- 승인 후 Source Entity가 실제 Command를 통해 변경되어야 한다.
- AI는 Approval/Effective 전환 권한을 갖지 않는다.

---

## 14. State / Transition Policy

Business State와 Workflow State를 분리한다.

최소 State Family:

- Customer Relationship State
- Sales Stage
- Quote State
- Contract Business State
- Contract Item Fulfillment State
- Work Item Workflow State
- Case State
- Approval State
- Asset State
- Shipment State
- Policy Version State

공통 Guard:

- 허용되지 않은 Transition은 거부한다.
- Transition은 Actor, Time, Before/After, Reason, Source를 Audit한다.
- 외부 Provider 실패 시 성공 State를 선반영하지 않는다.
- Notification 실패는 Business Transaction 성공과 분리하되 재시도/실패로그를 남긴다.
- 동시성 충돌 시 최신 Revision 재조회 후 재시도한다.

---

## 15. Inventory / Supply Requirements

- Quantity Inventory와 Asset/Serial을 분리한다.
- Material Requirement → Reservation/Allocation → Shipment/Transfer → Use/Install → Return/Repair/Disposal 흐름을 지원한다.
- 재고 수량 변경은 Inventory Transaction Ledger로 기록한다.
- Balance는 Transaction 기반 Projection으로 계산한다.
- 발주/PO, Vendor, 입고, 직배송, 창고출고를 구분한다.
- 설치/AS와 실제 사용 Asset/Serial을 연결한다.
- 기존 날짜별 가로형 Inventory Sheet를 신규 구조로 그대로 복제하지 않는다.

---

## 16. Finance / Settlement Requirements

- 비용/정산은 Source Entity와 증빙을 연결해야 한다.
- Customer/Store/Contract/Case/Vendor 귀속을 명시한다.
- 수정·취소는 원 Record 삭제보다 Adjustment/Correction을 사용한다.
- Finance Restricted 정보는 최소권한으로 제한한다.
- 계약 상대방, PG 명의, Settlement Party가 다를 수 있으므로 Legal Entity Assignment를 기준으로 귀속한다.

---

## 17. Compensation / Commission Requirements

- 판매 당시 Commercial Policy Version을 기준으로 계산한다.
- Fixed / Percent / Per-unit / Revenue Share Rule을 지원할 수 있어야 한다.
- DB 차감, 취소, 환수, 예외수당은 근거와 Approval을 보존한다.
- 과거 수당은 사후 Policy Version 변경으로 자동 재계산하지 않는다.
- 정확한 Compensation 계산/승인 정책은 기존 Decision Queue Pending을 유지한다.

---

## 18. Permission / Security Requirements

OC의 논리 권한 모델은 다음 7축을 사용한다.

`Role + Row Scope + Field Visibility + Action + Approval + Audit + AI Access`

Restricted 영역:

- FINANCE
- PEOPLE/HR
- COMPENSATION
- MANAGEMENT
- DECISION
- Commercial Restricted: 원가, 마진, 수당기준, PG Revenue Share, 특별정책

원칙:

- 메뉴 숨김은 보안이 아니다.
- 외부 영업/기사/Vendor는 Assigned Scope 중심.
- Field Masking을 지원한다.
- Reveal/Export/Approval/Secret Access 등 민감행위는 Audit한다.
- Shared IAM 물리 Architecture는 Common Infrastructure Pending이다.

---

## 19. Credential Isolation Policy

Legacy Customer Master에서 확인된 Login ID/PW/Key는 일반 Customer/Store Master로 Migration하지 않는다.

원칙:

- 일반 Core에는 Credential 존재여부, Provider, Status, Reference 등 Metadata만 둔다.
- Secret Payload는 별도 Secret Store/Vault 또는 재등록/Rotation 흐름을 사용한다.
- 가능하면 기존 PW/Key를 그대로 이관하지 않고 Reset/Rotate/Reissue를 우선한다.
- Search, AI Embedding, 일반 Export, Activity Log에 Secret 원문을 포함하지 않는다.
- Reveal/Copy/Rotate/Delete/Import/Export 시도는 Audit하되 Secret Value 자체를 로그에 남기지 않는다.
- 외부 영업/기사/Vendor는 기본적으로 Secret 접근 불가.
- Vault Provider/물리 구현은 별도 Implementation Decision이다.

---

## 20. AI Operations Policy

AI는 `Read → Suggest → Prepare Command → Human Confirm → Service Command → Audit` 흐름을 따른다.

AI가 할 수 있는 것:

- 정보 요약
- 이상징후 탐지
- 후속 Action 제안
- Draft Quote/Reply/Task/Policy 비교
- Migration Candidate 분류

AI가 독자적으로 하면 안 되는 것:

- 계약/정책 승인
- 민감 재무/수당 정보 무권한 조회
- Secret 원문 조회
- 중요 State 변경
- 지급/정산 확정
- Effective Policy 활성화

AI 결과는 Source Entity/Evidence를 추적할 수 있어야 한다.

---

## 21. Activity / Audit Requirements

중요 Event는 Activity 또는 Audit으로 기록한다.

예:

- 상담/통화/메시지/방문
- 견적 발송/수락
- 계약 체결/변경/해지
- 설치/배송/AS
- State Transition
- Approval
- Policy 변경
- Permission/Secret Reveal
- AI Commit

정정은 과거 Event 삭제보다 Correction/Amendment Event를 우선한다.

---

## 22. API / Service Boundary Requirements

- 한 Entity의 최종 Business State를 여러 Service가 직접 수정하지 않는다.
- Write는 해당 Domain Service Command를 통해 수행한다.
- Generic State PATCH보다 Business Command를 우선한다.

예:

- sendQuote
- convertQuoteToContract
- terminateContract
- verifyFulfillment
- closeCase
- adjustInventory

모든 Write는 Authorization + Business Guard + State Guard + Audit을 통과해야 한다.

Person/IAM은 Shared Interface Dependency로 취급한다.

Merchant Account 관련 API는 최종 구조 확정 전 Draft Interface만 허용한다.

---

## 23. Cross-Service Boundary Policy

### OSP

- 외부 유입, 설명, 상담신청, Lead 생성 Source.
- 승인된 Offer/Price/Promotion을 표현.
- 사람 상담·계약 실행 State의 Master가 아니다.

### OC

- Lead Handoff 이후 영업 실행
- Quote / Contract / Fulfillment / CS / AS
- Product / Commercial Policy Master
- Approval / Inventory / Internal Operations

### Business OS

- 매장 사장님·구성원의 Store 운영 Surface
- Store Runtime 운영데이터와 Self-service 접점
- OC의 계약/상품/정책 결과 Projection 소비

동일 Field의 Dual Master를 만들지 않는다.

---

## 24. Legacy Migration Policy

Migration 기본 흐름:

`Raw → Snapshot → Staging → Normalize/Parse → Mapping → DQ → Entity Candidate → Conflict Queue → Human Review → Core Import → Legacy Link → Reconciliation`

원칙:

- Legacy Source는 Master Candidate / Event Source / Policy Candidate / Supporting Evidence / Archive로 구분한다.
- 거대 Row를 Customer/Store/Contract/Product/Device/Payment/Installation 등으로 분해한다.
- 사업자번호/TID/전화/상호 하나만으로 자동 Merge하지 않는다.
- Strong Signal도 단독으로 Merge 근거가 되지 않는다.
- 모든 Import는 Idempotent해야 한다.
- 자동화가 위험한 충돌은 Human Review로 보낸다.

---

## 25. Identity Resolution Policy

실제 운영 케이스:

- 한 실질 운영자가 여러 Store, 명의는 가족별로 상이
- 같은 사업자가 여러 Store 운영
- 같은 장소 양도양수
- 양도양수 + 타지역 이전
- 법인명과 실제 상호 상이
- 계약 상대방과 PG/정산 명의 상이

분류 Candidate:

- SAME_STORE_SAME_LEGAL_ENTITY
- SAME_CUSTOMER_MULTI_STORE
- SAME_STORE_RENAMED
- STORE_TRANSFERRED_NEW_LEGAL_ENTITY
- CLOSED_AND_REOPENED
- SAME_LEGAL_ENTITY_MULTI_STORE
- IDENTIFIER_REUSED_OR_MOVED
- CONTACT_SHARED_ONLY
- UNRELATED
- AMBIGUOUS

Merge는 Hard Delete보다 Link/Event/History 보존을 우선한다.

---

## 26. Legacy Data Quality Guards

현재 Source에서 확인된 주요 문제를 Migration Guard로 유지한다.

- Business Number / Store Name / Phone Duplicate Candidate
- Cross-store Identifier/TID Collision Candidate
- Mixed Date Format
- Product Alias 혼재
- CMS 장문 메모에 사건/금액/통화/Action 누적
- Inventory 가로형 날짜 구조
- 색상에 의존한 Status
- Formula Error / #REF! / #VALUE!
- Customer Master 내 Login ID/PW/Key 혼재

Formula Error가 있는 Commercial Policy Cell은 자동 Official Policy로 승격하지 않는다.

---

## 27. Document / File Policy

Quote PDF, Contract, E-sign, Installation Photo, Customer Confirmation, AS Evidence는 Source Entity와 연결한다.

최소 속성 Candidate:

- Document Type
- Source Entity
- Revision
- Generated/Uploaded
- Signed Status
- Access Scope
- Retention
- File Reference

전자서명 Provider는 별도 Integration Decision Pending이다.

---

## 28. Schedule / Reminder / Notification / Queue Policy

- Schedule = 고객약속/방문/설치 시간
- Reminder = 특정시점 Action 상기 규칙
- Notification = 변화/주의 Signal
- Queue = 실제 처리해야 할 업무 Projection

네 개를 하나의 Entity로 합치지 않는다.

---

## 29. Non-Functional / Operational Requirements

- Reuse First: 기존 TMS/WDI에서 의미 있는 Capability는 재사용하되 Legacy 구조 전체를 복제하지 않는다.
- Idempotency: 중복 Command/Import로 중복 계약·재고·Event가 생성되지 않아야 한다.
- Auditability: 중요 Business 변경은 Actor/Source/Before/After/Reason 추적 가능해야 한다.
- Least Privilege: Restricted Domain은 최소권한.
- Regression Safety: 기능 변경 시 기존 동작 영향과 Side Effect를 검토한다.
- Test: 신규 기능은 의미 있는 테스트와 기존 Regression Test 통과 후 완료로 본다.
- Projection Consistency: Dashboard/Customer 360/Queue는 Source of Truth가 아니며 재생성 가능해야 한다.

---

## 30. Open Decision Queue / Pending

본 문서 작성 시점에도 아래는 최종 확정하지 않는다.

### Structural Pending

- Person Master 물리 위치 / Owner
- Merchant Account 최종 구조
- Shared IAM 물리 Architecture

### Existing Domain Pending

- Inventory/Supply 최종 Split
- Compensation 계산/승인 세부정책
- E-sign Provider/방식
- WDI Legacy 전사 데이터 Migration 범위
- Billing/Receivable 상세 경계
- Commercial Policy 세부 Approval Role/Threshold
- Marketing Subscription 1/2/3 상세 재기획

Pending은 이 문서의 업무정의와 정책기준을 무효화하지 않지만 Physical Schema/IAM/Development Ready 최종 Gate는 계속 차단한다.

---

## 31. Final Documentation Status

**PASS — DETAILED REQUIREMENTS & BUSINESS POLICIES FINAL CANDIDATE COMPLETE WITH PENDINGS**

본 문서는 `user-and-operations-flows.md`와 함께 PayPlay OC의 최종 Recovery Documentation Set을 구성한다.

---

→ 관련 문서: [user-and-operations-flows.md](../04_FLOWS/user-and-operations-flows.md)
→ Audit: [OC_TRACEABILITY_GAP_AUDIT_v1.md](../10_AUDIT/OC_TRACEABILITY_GAP_AUDIT_v1.md)
