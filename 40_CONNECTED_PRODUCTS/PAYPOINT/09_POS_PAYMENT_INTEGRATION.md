# POS Event / Payment Integration
- **File Path:** `40_CONNECTED_PRODUCTS/PAYPOINT/09_POS_PAYMENT_INTEGRATION.md`
- **Document ID:** `MP-PP-DOC-POS-PAYMENT-001`
- **Status:** WORKING
- **Source of Truth:** NO
- **Owner:** Marketing Play / PayPoint
- **Last Reviewed:** 2026-08-16
- **Development Use:** Integration Architecture Reference / Commercial Terms Pending

## Ownership
- **Product:** PayPoint
- **Product Owner / 소속:** Marketing Play
- **Hosted In:** PayPlay Business OS
- **Repository Location ≠ Product Ownership**


## Boundary
Order ≠ Payment Transaction ≠ Point Event ≠ Settlement Ledger.
기존 POS 결제는 PayPoint/Business OS 장애와 분리.

## POS Strategy
UnionPOS 우선 연동 후보. 이후 POS사별 Adapter 확장.

Adapter Candidate:
Authentication / Store Mapping / Terminal Mapping / Order Push / Order Status / Payment Approved / Cancel / Partial Cancel / Receipt Data / Printer Dispatch / Health Check / Error / Audit.

## Reliability
Payment SUCCESS / Order CONFIRMED / POS Sync PENDING 상태 분리.
Retry / Pending Queue / Manual Attention 필요.

## PG Revenue Working Fact
예시: 기초 결제비용 0.6% + 추가 PG Margin 1.3% = 적용 1.9%.
1.3%는 Gross Margin 후보이며 실제 Net Margin은 PENDING.
