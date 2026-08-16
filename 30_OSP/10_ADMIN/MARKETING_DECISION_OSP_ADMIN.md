# Marketing Decision / OSP Admin

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/10_ADMIN/MARKETING_DECISION_OSP_ADMIN.md` |
| Document ID | `PP-OSP-ADMIN-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Admin / Decision Support Working Specification |

---

## Purpose

OSP Admin은 단순 관리자 페이지가 아니라
PayPlay 온라인 영업의 관제·분석·의사결정 지원 영역이다.

---

## Screen Families

1. Marketing Performance Dashboard
2. Campaign / Channel Performance
3. Landing / Content Operations
4. Product / Offer Presentation Manager
5. Lead Capture & OC Handoff Monitor
6. Lead Detail / Attribution Trace
7. Funnel / Attribution Analytics
8. Experiment / Learning — WORKING
9. Marketing Decision Center

---

## Decision Loop

```text
Spend / Traffic
→ Lead
→ OC Accepted
→ Contract / Revenue
→ Attribution
→ KPI
→ Marketing Decision
→ Next Execution
```

---

## Guardrails

- 담당자 배정·상담·견적·계약 실행 기능을 OSP Admin에 중복 구현하지 않는다.
- MOCK 데이터를 실제 KPI처럼 표시하지 않는다.
- Revenue / Contract 관련 데이터는 최소권한으로 조회한다.
- Lead PII는 역할별 Masking 대상이다.
- 외부 영향 실행은 Human Approval을 기본으로 한다.

---

## PENDING

- Shared IAM Role Scope
- Automated Budget / Campaign Execution
- AI Execution Authority
- Physical Spend / Outcome Data Sources
