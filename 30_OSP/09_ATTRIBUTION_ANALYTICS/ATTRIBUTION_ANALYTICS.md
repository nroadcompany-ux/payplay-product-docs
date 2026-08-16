# Attribution / Analytics

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/09_ATTRIBUTION_ANALYTICS/ATTRIBUTION_ANALYTICS.md` |
| Document ID | `PP-OSP-ATTR-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Analytics Working Baseline / 공식 산식·Window 확정 전 Production 기준 사용 금지 |

---

## Closed Loop

```text
Traffic / Touch
→ Valid Lead
→ OC Accepted
→ Consultation
→ Quote
→ Contract
→ Contract Amount / Recognized Revenue
→ Attribution
→ KPI
→ Marketing Decision
```

---

## Data Principles

- Contract Amount ≠ Recognized Revenue
- Outcome Pending ≠ Lost
- Spend Missing ≠ 0
- Advertising Platform Conversion ≠ PayPlay Real Contract
- Cancellation / Void는 과거 Event를 삭제하지 않고 Reversal로 보존
- Raw Touch History 보존
- OC 상담·견적·계약 Ledger가 Source of Truth
- OSP는 필요한 Outcome Projection만 소비

---

## Working KPI Family

- CTR
- CPC
- CPL
- Accepted Lead Cost / CPAL Candidate
- Contract Acquisition Cost
- CAC
- ROAS

---

## PENDING

- 공식 Attribution Model
- Attribution Window
- Multi-touch Rule
- Spend Source / API
- Revenue Recognition Physical Source
- KPI 최종 공식 명칭·산식
