# Conversion / Lead Capture

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/07_DISCOVERY_CONVERSION/CONVERSION_LEAD_CAPTURE.md` |
| Document ID | `PP-OSP-CONVERSION-LEAD-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Conversion Flow / Lead Logical Model 기준 |

---

## Conversion Entry

- Consultation
- Quote Request Entry
- Application
- Contact / Inquiry
- Campaign-specific CTA

---

## Official Lead Creation Condition

Required Validation과 필요한 Consent가 충족된 후
Official Lead를 생성한다.

---

## Lead Candidate Fields

- lead_id
- lead_type
- prospect / person context
- contact
- store_context_ref — optional
- interest product / service
- source / channel
- campaign / ad / creative / landing reference
- UTM / Click ID
- consent snapshot
- consent version
- consent timestamp
- request context
- quality signal — optional
- created_at

---

## Rules

- Support Ticket을 자동으로 Sales Lead로 간주하지 않는다.
- Consent 없이 Official Lead를 생성하지 않는다.
- 동일 신청 Retry로 중복 OC Lead를 만들지 않는다.
- Person / Store / Legal Entity를 자동 병합하지 않는다.
