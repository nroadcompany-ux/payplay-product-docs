# PayPlay Business OS Service Architecture

| 항목 | 내용 |
|---|---|
| File Path | `20_BUSINESS_OS/06_SERVICE_ARCHITECTURE.md` |
| Document ID | `PP-BOS-SVC-ARCH-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Service 구조 Working Baseline. Navigation 최종안 아님 |

## APPROVED
- 매장관리
- 고객·마케팅 통합
- 상품·서비스 독립
- AI 매니저 전역

## WORKING
- 직원·업무
- 매출·정산
- 도움·지원
- 성장·혜택
- SaengZone 진입

## Relation Types
Own / Hosted In / Connected / Reads From / Handoff

PayPoint = Hosted In.
OC = Handoff / Reads From.
SaengZone = Hosted In / Uses 연구.
Marketing Play = Connected / Reads From 연구.
