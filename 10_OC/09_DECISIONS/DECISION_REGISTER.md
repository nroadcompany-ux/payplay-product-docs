# PayPlay OC Decision Register

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/09_DECISIONS/DECISION_REGISTER.md` |
| Document ID | PP-OC-DEC-001 |
| Status | APPROVED |
| Source of Truth | YES |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Main PM/Owner 승인 OC 구조 Decision만 기록. Proposal/Working 항목 승격 금지. |

## D-OC-001 Customer Account
Customer Account = **동일 실질 운영관계로 PayPlay가 통합 관리하는 고객그룹**. 법적 계약/세금/PG/정산 주체가 아니다.

## D-OC-002 Store Transfer / Continuity
동일 장소에서 운영·장비·업무 연속성이 유지되면 기존 Store ID 유지 Candidate. 타지역 이동은 신규 Store 우선. 애매하면 Human Review.

## D-OC-003 Legal Entity Assignment History
Store에 단일 Legal Entity를 고정하지 않고 역할·기간 Assignment History를 보존한다.

## D-OC-004 Product / Commercial Policy Owner
OC가 Product / Commercial Policy Master Owner다. OSP는 Approved Offer Projection, Business OS는 Applied Result를 소비한다.

## D-OC-005 People / HR Scope
People / HR는 OC 공식 설계·구현 범위에 포함한다. 퇴사/해촉자 사후 행정요청은 Former Employee Service Desk로 처리한다.

## D-OC-006 Legacy Capability Preservation
기존 TMS 실제 Capability는 신규 설계에서 보이지 않는다는 이유만으로 삭제하지 않는다. 애매한 기능은 Owner 확인 전 삭제/Archive하지 않는다.

## Non-Decisions
Revenue Share 정확 요율, Compensation Formula/Threshold, Provider 선택, Physical Service split, Working Screen ID는 Decision으로 승격하지 않는다.
