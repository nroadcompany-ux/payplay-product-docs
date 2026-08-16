# Point / Coupon / Benefit
- **File Path:** `40_CONNECTED_PRODUCTS/PAYPOINT/05_POINT_COUPON_BENEFIT.md`
- **Document ID:** `MP-PP-DOC-POINT-COUPON-BENEFIT-001`
- **Status:** WORKING
- **Source of Truth:** NO
- **Owner:** Marketing Play / PayPoint
- **Last Reviewed:** 2026-08-16
- **Development Use:** Policy Research Reference

## Ownership
- **Product:** PayPoint
- **Product Owner / 소속:** Marketing Play
- **Hosted In:** PayPlay Business OS
- **Repository Location ≠ Product Ownership**


## Concept
Point = 누적·차감 자산 / Coupon = 제한적 사용 권리 / Benefit = 상위 혜택 / Reward = Action 결과 보상 / Prize = 이벤트 경품.

## Ledger Principle
Customer Activity Record ≠ Point Transaction Ledger ≠ Payment Transaction ≠ Settlement Ledger ≠ Marketing Event.

잔액 직접 덮어쓰기보다 Event Append + Balance Projection 방향을 우선 연구.

## Point Event Candidate
EARN / USE / EXPIRE / CANCEL / REVERSAL / ADJUST / BONUS / REFERRAL / EVENT_REWARD.

## Reversal
Payment Cancel → Point Reversal Event. 부분취소는 해당 부분만 반전 처리 검토.

## Store vs Shared Point
Store Point 우선. Shared / Network Point는 Future Research / PENDING.
Shared Point는 Settlement / Clearing / Liability가 필요.
