# Customer State / Visit / Return / Loyal Customer / LTV
- **File Path:** `40_CONNECTED_PRODUCTS/PAYPOINT/04_CUSTOMER_STATE_VISIT_RETURN_LTV.md`
- **Document ID:** `MP-PP-DOC-CUSTOMER-STATE-LTV-001`
- **Status:** WORKING
- **Source of Truth:** NO
- **Owner:** Marketing Play / PayPoint
- **Last Reviewed:** 2026-08-16
- **Development Use:** Rule Design Reference / Threshold Pending

## Ownership
- **Product:** PayPoint
- **Product Owner / 소속:** Marketing Play
- **Hosted In:** PayPlay Business OS
- **Repository Location ≠ Product Ownership**


## State ≠ Grade
State = 현재 관계 상태 / Grade = 가치·중요도.

예: Grade = VIP, State = At Risk.

## State Candidate
Identified / First Visit / Second Visit / Repeat / Regular / At Risk / Dormant / Presumed Churn / Reactivated.

## Expected Visit Interval
Personal → Segment → Store → Industry 순으로 Fallback 검토.

## Risk Ratio Candidate
Days Since Last Visit ÷ Expected Visit Interval.

Threshold 숫자는 PENDING.

## Dormant Principle
`30일 미방문 = 휴면` 일괄 적용 금지. 개인 또는 매장 방문주기 대비 초과 정도 활용.

## LTV
Average Ticket / Visit Frequency / Retention / Churn / Active Period / Margin 고려 후보. 공식식은 PENDING.
