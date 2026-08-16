# QR / NFC Order & Customer Entry
- **File Path:** `40_CONNECTED_PRODUCTS/PAYPOINT/06_QR_NFC_ORDER_AND_ENTRY.md`
- **Document ID:** `MP-PP-DOC-QR-NFC-ORDER-001`
- **Status:** WORKING
- **Source of Truth:** NO
- **Owner:** Marketing Play / PayPoint
- **Last Reviewed:** 2026-08-16
- **Development Use:** Strategic Expansion Architecture Reference

## Ownership
- **Product:** PayPoint
- **Product Owner / 소속:** Marketing Play
- **Hosted In:** PayPlay Business OS
- **Repository Location ≠ Product Ownership**


## Store Gateway
QR은 주문기능 하나가 아니라 PayPoint Store Gateway의 Entry Channel 후보.

Entry Channel: QR / NFC / Link / POS.

Capability: Point / Coupon / Event / Roulette / Receipt Review / Dine-in Order / Takeout / Pre-order / Payment / Future Delivery.

## Order Types
DINE_IN / TAKEOUT / PRE_ORDER_DINE_IN / PRE_ORDER_TAKEOUT / DELIVERY(Future).

## External Order Rule
매장 밖 주문은 선결제 완료 후에만 Confirmed Order로 처리.

Order Draft → Payment Pending → Payment Success → Order Confirmed.

## Preparation Time
매장이 최소 준비시간 설정. 예: 현재 13:00, 최소 30분 → 최초 선택 가능 13:30.

고객은 13:30 / 13:45 / 14:00 등 허용된 Slot 중 선택.

## Identity Boundary
Order ≠ Customer. 익명 주문 세션을 허용하고 이후 식별 시 연결하는 구조 검토.
