# Receipt Review Integration
- **File Path:** `40_CONNECTED_PRODUCTS/PAYPOINT/08_RECEIPT_REVIEW.md`
- **Document ID:** `MP-PP-DOC-RECEIPT-REVIEW-001`
- **Status:** WORKING
- **Source of Truth:** NO
- **Owner:** Marketing Play / PayPoint
- **Last Reviewed:** 2026-08-16
- **Development Use:** Flow / Integration Research Reference

## Ownership
- **Product:** PayPoint
- **Product Owner / 소속:** Marketing Play
- **Hosted In:** PayPlay Business OS
- **Repository Location ≠ Product Ownership**


## Working Flow
QR Scan → PayPoint Store Page → [영수증 신청하기] → POS/Printer 요청 → 프린터 출력 → 직원이 영수증 전달 → [네이버에서 리뷰 작성하기] → NAVER 이동 → 고객 직접 리뷰.

## Printer Message Candidate
[PayPoint 고객 요청]
영수증 리뷰용 영수증을 고객에게 전달해주세요.
요청시각 / 테이블 / 주문번호는 필요 범위만 표시.

## Boundary
PayPoint: Review Intent / Receipt Request / Store Task / Printer Dispatch / NAVER Outbound.
NAVER: 방문 인증 / 리뷰 작성 / 게시 / 정책 판단.

## Completion
NAVER 이동 = 리뷰 완료로 간주 금지.
Review Completion은 검증 근거가 있을 때만 Verified.
