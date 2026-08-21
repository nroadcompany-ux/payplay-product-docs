# Legacy TMS Capability Preservation & Loss Audit

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/01_RECOVERY/TMS_CAPABILITY_PRESERVATION_LOSS_AUDIT.md` |
| Document ID | PP-OC-RECOVERY-AUDIT-001 |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | 기존 TMS Capability 상실 방지 Audit. Development Gate 전 전수 Trace 검증에 사용. |

## Audit Principle
- 기존 TMS 실제 구현 Capability는 신규 설계 문서에 없다는 이유로 삭제 금지.
- 중복은 의미·State Owner·사용자·이력 확인 후 통합.
- Archive 후보도 대체기능·Migration·Regression 검증 전 삭제 금지.
- 애매한 항목은 Owner 확인 전 유지.

## 보존 검수 대상
Lead/계약/판매기록/계약만료/마진계산, 가맹점신청/방문일정/배송/재고/수발주/제조사 AS/POS 청소, AI 업무도우미/할일/업무게시판/팀채팅/일정·미팅/프로젝트/전자계약, 근태/휴가, 차량/주차/CCTV/회사정보, 정산/지출결의/거래처/채널/광고, 사용자/보안.

## Attendance / Leave
Legacy `biz_attendance`, `biz_leave_requests` 기반 출퇴근·휴무/휴가·승인/반려/취소·Calendar·휴가자 업무배정 Guard를 People/HR에 유지·통합한다.

## Vehicle
차량 전용 관리 기능은 유지. Company Operations / Administrative Asset로 보고 Driver/Employee Assignment는 People/HR과 연계한다.

## Parking
정기주차, 방문주차, 차량등록, 주차유형, 월비용, 등록이력, 외부 주차사이트 연동을 유지한다.

## Deletion Guard
`Legacy 기능 → 실제 사용자/업무 → Source Data → 대체기능 → Migration/History → Permission → Regression/Side Effect → Owner Confirmation`
