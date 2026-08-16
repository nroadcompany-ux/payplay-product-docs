# PayPlay OC Capability Inventory

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/03_CAPABILITIES/CAPABILITY_INVENTORY.md` |
| Document ID | PP-OC-CAP-001 |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | TMS/WDI Recovery를 OC Domain과 연결하는 Capability Coverage 기준. Working ID는 공식 확정 ID가 아님. |

## Status
Recovery에서 총 64개 Working Capability가 식별되었다. `OC-CAP-*`는 추적용 Working ID다.

## Domain Summary
| Domain | 주요 Capability |
|---|---|
| CUSTOMER | 등록·검색·연락관계·운영이력 |
| SALES | Lead Handoff·배정·상담·방문·영업 Stage |
| CONTRACT | 계약·전자계약·승인·변경/해지·증빙·설치인계 |
| INSTALLATION | 설치대상·일정·배정·실행·검수 |
| SERVICE / AS | 문의·장애·원격·현장·Vendor/제조사 AS |
| PRODUCT | Product/Service Master·Option·Alias |
| INVENTORY / SUPPLY | 재고·Asset·PO·Shipment·Vendor |
| FINANCE | 매출·비용·정산·원가·마진·계좌 |
| PEOPLE / HR | 직원/외부인력·조직·근태·휴가·Lifecycle·퇴사자 요청 |
| COMPENSATION | 급여·수당·Commission·Incentive |
| MANAGEMENT | 운영/재무/성과 KPI |
| DECISION | Decision·Reason·Expected·Actual·Review·Guard |
| COMMON | Permission 요구·File·Notification·Audit·Search |

## Legacy Loss Trace 추가
차량, 주차, CCTV, 회사정보, POS청소, 제조사AS입고, 계약만료, 판매기록, 일정/미팅/프로젝트, 업무게시판, 채널/광고, 사용자/보안 Legacy UX를 별도 보존 추적한다.

## Guard
`Legacy Capability → OC Domain → Screen/Queue/Service → API/Data → Permission → Test`
