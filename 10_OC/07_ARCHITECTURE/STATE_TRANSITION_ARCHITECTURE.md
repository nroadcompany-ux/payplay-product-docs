# State / Transition Architecture

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/07_ARCHITECTURE/STATE_TRANSITION_ARCHITECTURE.md` |
| Document ID | PP-OC-ARCH-STATE-001 |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | OC Business State와 Workflow State 충돌 방지 및 Command Guard 설계 기준. |

## Principle
서로 다른 Domain State를 하나의 범용 `status`로 합치지 않는다.

## State Families
Customer Relationship, Sales Stage, Quote/Revision, Approval, Contract, Contract Item/Fulfillment, Work Item, Installation Verification, Case/Waiting, Inventory/Reservation/Shipment/Asset, Policy Version, Finance/Settlement/Compensation, Queue Condition.

## Confirmed Guards
- Quote Accepted ≠ Contract Signed
- Contract Signed ≠ Fulfillment Complete
- Work Item Complete ≠ Contract Item Verified Complete
- Case Closed ≠ Contract Item / Asset Recovery Complete
- Approval Approved ≠ Source Domain State Changed
- Shipment Delivered ≠ Installation Complete
- Queue Overdue / Blocked ≠ Business State

## Transition Rule
`Current State Read → Authorization → Business Guard → State Guard → Approval Guard → Version Check → Domain Command → Source Update → Audit/Event`

Generic status PATCH는 금지한다.
