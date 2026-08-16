# OSP Domain Architecture

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/03_DOMAIN_ARCHITECTURE/OSP_DOMAIN_ARCHITECTURE.md` |
| Document ID | `PP-OSP-DOMAIN-001` |
| Status | APPROVED |
| Source of Truth | YES |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Logical Domain 분해 기준으로 사용 가능 |

---

## 1. Official Domains

1. **Acquisition & Traffic**
2. **Website & Sales Content**
3. **Discovery & Sales Experience**
4. **Conversion & Lead Capture**
5. **Lead & OC Handoff**
6. **Campaign & Attribution**
7. **Sales Analytics & Optimization**
8. **Marketing Decision & OSP Admin**

---

## 2. Domain Responsibility

### D1 Acquisition & Traffic
온라인 유입 Source와 Session Context를 확보한다.

### D2 Website & Sales Content
Website, Landing, Product / Service Content, Sales Content를 운영한다.

### D3 Discovery & Sales Experience
상품·서비스 탐색, 비교, 승인 Offer Presentation, 추천 경험을 제공한다.

### D4 Conversion & Lead Capture
상담·견적·신청 Entry, Validation, Consent, Lead 생성까지 담당한다.

### D5 Lead & OC Handoff
생성된 Lead를 PayPlay OC로 전달하고 Handoff Transport State를 관리한다.

### D6 Campaign & Attribution
Campaign / Ad / Creative / Landing / Touch와 Lead·Outcome을 연결한다.

### D7 Sales Analytics & Optimization
Traffic → Lead → Accepted → Contract → Revenue Funnel을 분석한다.

### D8 Marketing Decision & OSP Admin
성과를 관제하고 다음 Marketing Action 의사결정을 지원한다.

---

## 3. Cross-Service Boundary

### PayPlay OC
Lead Assignment / Consultation / Quote / Contract / Installation / AS / Commercial Policy Master

### Business OS
계약 이후 매장 운영 Surface / Self-Service / Store Operation

### Shared
IAM / Notification / Audit / Document / Integration / Common Entity Reference

---

## 4. Prohibition

OSP Domain Architecture는
Marketing Play / PayPoint를 임의로 OSP 하위 Entity로 편입하지 않는다.
