# Lead / Person / Store Relationship

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/13_ENTITY_RELATIONSHIPS/LEAD_PERSON_STORE_RELATIONSHIP.md` |
| Document ID | `PP-OSP-ENTITY-REL-001` |
| Status | APPROVED |
| Source of Truth | YES |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Logical Entity Separation 기준으로 사용 가능 / Physical Person Master 위치는 PENDING |

---

## 1. Core Rule

**Person ≠ Store ≠ Legal Entity**

동일 실운영자가 여러 Store를 운영하거나
Store별 법적 명의자가 다른 경우에도
임의 자동병합하지 않는다.

---

## 2. Lead Relationship

Lead는 특정 문의 / 상담 / 신청 의도 Event다.

Lead는 Person 또는 Prospect Context를 참조할 수 있으며,
확인 가능한 경우 Store Context Reference를 가질 수 있다.

```text
Person / Prospect
   ↓
 Lead
   ↓
Optional Store Context
```

Lead 생성이 Person Master 확정을 의미하지 않는다.

---

## 3. Store Rule

- 동일 장소라도 양도양수 시 법적·계약 Context가 달라질 수 있다.
- 동일 Person이 여러 Store를 운영할 수 있다.
- Store와 Legal Entity를 자동 동일시하지 않는다.

---

## 4. PENDING

- Person Master 물리 위치
- Merchant Account 최종 구조
- Shared IAM 물리 Architecture
