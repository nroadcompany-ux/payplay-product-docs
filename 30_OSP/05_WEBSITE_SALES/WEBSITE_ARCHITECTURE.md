# Website Architecture

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/05_WEBSITE_SALES/WEBSITE_ARCHITECTURE.md` |
| Document ID | `PP-OSP-WEB-ARCH-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Website IA / Surface Planning 기준으로 사용 가능 |

---

## 1. Relationship

```text
PayPlay OSP
└─ PayPlay Website
   ├─ Homepage
   ├─ Landing
   ├─ Product / Service Pages
   ├─ Content / Insight
   ├─ Customer Center
   ├─ Smart Ground — WORKING / Naming Pending
   └─ Conversion UI
```

Website는 OSP의 주요 구현 Surface이지만 OSP 전체와 동일하지 않다.

---

## 2. Customer-facing Screen Families

- OSP Home / Sales Gateway
- Product / Service Discovery
- Product / Service Detail & Offer
- Compare / Bundle / Recommendation
- Smart Ground Sales Experience — WORKING
- Consultation / Quote / Application Form
- Submission Complete / Handoff Status
- My Request / Customer Status
- Customer Center / Support Entry

---

## 3. Current Implementation Evidence

현재 Website 구현에서는 다음 Surface가 확인되었다.

- Public Website
- Product / Service Page
- Contact
- Support
- Ticket
- Onboarding
- Signup / Login / MyPage
- Admin CMS
- Marketing Prototype

실제 Route / Component 구조는 구현 Repository Snapshot 기준 재검증이 필요하다.
