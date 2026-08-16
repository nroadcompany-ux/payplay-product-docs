# PayPlay Business OS — Store Operating Model v1 + Screen Architecture v1

| 항목 | 내용 |
|---|---|
| File Path | `20_BUSINESS_OS/19_STORE_OPERATING_MODEL_SCREEN_ARCHITECTURE_v1.md` |
| Document ID | `PP-BOS-ARCH-OPERATING-SCREEN-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Working Architecture. PENDING 항목을 구현 확정 근거로 사용 금지 |

## Store Operating Model
`Store Context → Daypart Context → Operating State Candidate → Signal / Task / Alert / Request → User Action → Result / Pending / Handoff`

Daypart는 시간·영업 흐름 Context이며 자동 Mode로 확정하지 않는다.
Operating State는 단일 Label보다 Business Availability / Workforce / Device-Service / Task-Request / Customer-Money-Marketing Signal의 Layered State 후보로 다룬다.

## Home / 오늘의 매장
`현재 상태 → 놓치면 안 되는 것 → 꼭 해야 할 일 → 즉시 실행`
초기 버전은 Task / State / Alert 중심이며 AI 자동 우선순위 판정은 필수조건이 아니다.

## Owner / Staff Use Case
Owner: `Home → 직원/업무 → 매장/장비/지원 → 매출/입금/정산 → 고객·마케팅/PayPoint → Action → OC 처리상태 → 미완료 확인`

Staff: `본인 식별 → 출근 → 오늘 내 업무 → 매뉴얼/Checklist → 허용된 PayPoint/지원 Action → 완료/보류 → 퇴근 → 근무시간 기록`

Working Principle: `동일 Business OS + Store Context + Permission + Shared POS Context = 사용자별 다른 Surface`

## Screen Architecture v1
- BOS-SCR-001 Home / 오늘의 매장
- BOS-SCR-010 매장: 요약 / 장비·디지털서비스 / 운영 이슈
- BOS-SCR-020 직원·업무: 직원현황 / 출퇴근 / 업무 / Private Manual·Checklist / 근무시간
- BOS-SCR-030 매출·입금·정산: 매출요약 / 입금·정산 / 자료·이상확인
- BOS-SCR-040 고객·마케팅: 고객요약 / Marketing Signal / PayPoint Hosted Entry
- BOS-SCR-050 도움·Self Service: 검색·FAQ / Manual / Troubleshooting / 지원요청 / 요청상태
- BOS-SCR-060 상품·서비스: 이용중 / 추가 / 신청·진행상태
- BOS-SCR-070 PayPoint Hosted Surface: 고객식별 / 적립·사용 Preview / Pending·Retry·Reversal / 고객자산·Mission Candidate
- BOS-SCR-080 AI Manager: Global Entry / Contextual Answer / Action Preview·Handoff
- BOS-SCR-090 BOS → OC Handoff: Request Preview / Submit·Handoff Pending / Received·In Progress·Completed

본 Screen Tree는 Primary Navigation 최종안을 의미하지 않는다.

## Cross-Screen Execution
`Home / Domain Signal → Domain Screen → Action → Permission / Context → Local | Hosted | OC Handoff | Read Projection | AI Assisted → Confirmed | Pending | Failed | Unknown → 화면 갱신`

외부 결과가 불명확하면 성공으로 자동 처리하지 않는다.

## Sensitive Data Visibility Candidate
Shared POS 기본 노출 후보: 오늘 업무, 본인 출퇴근, 매뉴얼, 장비/A/S 상태, 공지, 허용된 PayPoint Routine Action, 도움/지원.

제한/비노출 후보: 상세 매출, 입금/정산, 고객 연락처, 시급/예상급여, 민감 계약, 권한설정, PayPoint 수동 조정/취소/회수.

## PayPoint 관계
- Product Owner / 소속: Marketing Play
- Hosted In: PayPlay Business OS
- Payment Event Path: PENDING

## OC 관계
Business OS = 요청 Entry / 상태 View / Self Service / Handoff Surface.
OC = 계약 / 설치 / AS / 재고 / 내부 Workflow 실제 처리 Owner.
Physical Handoff Contract는 PENDING.

## 유지 PENDING
- Primary Navigation 최종안
- Owner / Staff Role Matrix
- Store State 자동판정 Rule
- PayPoint Payment Event Path
- Shared POS Re-auth / Session
- Shared IAM
- Person Master 물리 위치
- Merchant Account 최종 구조

## Gate
Documentation: PASS WITH PENDINGS Candidate / Architecture: WORKING / Specification: NOT YET / Development Ready: NO / QA Ready: NO
