# Service Boundaries (서비스 경계)

| 항목 | 내용 |
|------|------|
| Document ID | PP-SA-001 |
| Document Type | Shared Architecture — Service Boundary |
| Status | WORKING |
| Source of Truth | NO (WORKING 단계) |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | ❌ 개발 확정 기준 사용 불가. Logical Boundary 참조용. |

> 2026-08-16 — OC / Business OS / OSP / PayPoint 4개 세션 정식 입고 결과를 기준으로 재정합성.

---

## 1. PayPlay 3축 + Connected Product

```
PayPlay
├─ PayPlay OSP           Online Sales Platform / 온라인 영업 플랫폼
├─ PayPlay OC            운영 센터
└─ PayPlay Business OS   Store Operating Surface (내부 약칭: PPOS)
     └─ PayPoint         Hosted In / Product Owner: Marketing Play
```

---

## 2. 서비스별 책임 경계

### PayPlay OSP (Online Sales Platform / 온라인 영업 플랫폼)

| 구분 | 내용 |
|------|------|
| 담당 | Traffic / Acquisition, Website / Sales Content, Discovery, Conversion, Lead Capture, OSP → OC Handoff, Attribution / Analytics, Marketing Decision / OSP Admin |
| 담당하지 않음 | 사람 상담 실행, 계약 실행 State, 설치·CS·AS 운영, Product / Commercial Policy Master |

- OSP는 **Lead Source / Creation Owner**다.
- OSP는 승인된 Offer를 외부에 **표현**하며 Master를 소유하지 않는다.
- POS / 키오스크 / 테이블오더 / 카드단말기를 OSP 하위 Product로 정의하지 않는다.

### PayPlay OC (운영 센터)

| 구분 | 내용 |
|------|------|
| 담당 | Lead Accepted 이후 Sales 실행, Quote, Contract, Fulfillment, Installation, CS / AS, Inventory, Approval, People/HR, Internal Operation |
| 담당하지 않음 | 외부 유입·Lead 확보, 매장 사장님 Self-service Surface |

- OC는 **Product / Commercial Policy Master Owner**다.

### PayPlay Business OS (Store Operating Surface)

| 구분 | 내용 |
|------|------|
| 담당 | Store Operating Surface, Self Service / Knowledge, 근태·업무·Task·Checklist, 요청/지원 상태 View, 매출·입금·정산 View, 고객·마케팅 Summary, AI Manager, PayPoint Hosted Surface, OC Handoff Entry |
| 담당하지 않음 | Contract / Installation / AS / Inventory / Product Commercial Master 직접 소유, 외부 Product Logic 소유 |

---

## 3. Connected Product 경계

| Product | Product Owner / 소속 | Hosted In | Documentation |
|---------|---------------------|-----------|---------------|
| PayPoint | **Marketing Play** | PayPlay Business OS | `40_CONNECTED_PRODUCTS/PAYPOINT/` (이 Repository에 입고 완료) |
| SaengZone | SaengZone | 독립 | saengzone-product-docs (예정) |

> **Implementation Location ≠ Product Ownership ≠ Documentation Ownership**
> PayPoint 상세 문서가 이 Repository에 입고되어 있으나, Ownership은 Marketing Play로 유지된다.
> Business OS는 PayPoint의 **Merchant Operating Surface**를 담당한다.

---

## 4. Handoff 기준

### OSP → OC

```
Validated Intake → Required Consent → Official Lead Created
→ Handoff Pending → Submitted → Received / ACK → Accepted → OC Sales Process
```

- **Received ≠ Accepted** (Owner Decision)
- Received / ACK = 기술적 수신
- Accepted = OC가 Lead 업무 책임을 인수 → **책임 이전 기준**

→ 상세: [30_OSP/08_HANDOFF/OSP_OC_HANDOFF.md](../30_OSP/08_HANDOFF/OSP_OC_HANDOFF.md)

### Business OS ↔ OC

```
Business OS Request → Context → OC → 상태 → Business OS
```

- Business OS: 사용자 Entry, 상태 View, Self Service, 최소 Context Handoff
- OC: 계약·설치·AS·재고·Service Request/Case·Product/Commercial Policy·내부 Workflow

→ 상세: [20_BUSINESS_OS/15_OC_INTEGRATION.md](../20_BUSINESS_OS/15_OC_INTEGRATION.md)

### PayPoint ↔ Business OS

→ 상세: [20_BUSINESS_OS/14_PAYPOINT_HOSTED_IN.md](../20_BUSINESS_OS/14_PAYPOINT_HOSTED_IN.md)
→ 상세: [40_CONNECTED_PRODUCTS/PAYPOINT/12_BUSINESS_OS_HOSTED_IN.md](../40_CONNECTED_PRODUCTS/PAYPOINT/12_BUSINESS_OS_HOSTED_IN.md)

---

## 5. 공통 원칙

- 동일 Field의 **Dual Master**를 만들지 않는다.
- 한 Entity의 최종 Business State를 여러 Service가 직접 수정하지 않는다.
- Repository 위치를 Product Ownership 근거로 사용하지 않는다.
- Physical API Contract는 확정하지 않는다 (PENDING).

---

## 6. 관련 문서

| 서비스 | 진입점 |
|--------|--------|
| PayPlay OC | [10_OC/README.md](../10_OC/README.md) |
| PayPlay Business OS | [20_BUSINESS_OS/README.md](../20_BUSINESS_OS/README.md) |
| PayPlay OSP | [30_OSP/README.md](../30_OSP/README.md) |
| PayPoint | [40_CONNECTED_PRODUCTS/PAYPOINT/README.md](../40_CONNECTED_PRODUCTS/PAYPOINT/README.md) |
| Shared Entity Decision | [10_OC/06_ENTITY_DATA/SHARED_ENTITY_DECISION_APPLIED.md](../10_OC/06_ENTITY_DATA/SHARED_ENTITY_DECISION_APPLIED.md) |
