# People / HR + Former Employee Service Desk Specification

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/08_SPECIFICATIONS/PEOPLE_HR_FORMER_EMPLOYEE_SERVICE_DESK.md` |
| Document ID | PP-OC-SPEC-HR-001 |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | OC People/HR 공식 범위를 상세화하는 Restricted Domain Specification. IAM/법정문서/Compensation 세부정책 Pending. |

## Scope Decision
People / HR는 PayPlay OC 공식 설계·구현 범위에 포함한다.

## Operating Flow
`Person Reference → Employee/Worker Relationship → Organization/Role → Onboarding → Contract/Documents → Attendance/Leave → Active Work/Performance → Compensation Handoff → Status Change → Resignation/Termination → Offboarding → IAM Access Revocation Handoff → Former Employee Service Desk → HR Queue → Issue/Reply → Audit`

## Identity Boundary
- Employee/Worker ≠ IAM User
- HR Organization/Job ≠ System Permission
- Employment Ended ≠ HR History Deleted
- Employment Ended ≠ IAM Account Deleted와 동일 Event

## Attendance / Leave
Legacy TMS에서 확인된 출퇴근, 근무시간, 근무유형/메모, 휴가/휴무 신청, 승인/반려/취소, Calendar, 승인 휴가자 업무배정 Guard를 유지·통합한다.

## Offboarding
`End Decision → 종료일 → 업무인계 → Open Work 확인 → Asset 회수 → Compensation/Expense Handoff → IAM Access Revocation Request → 최종서류 → Verification → Ended`

## Former Employee Service Desk
퇴사/해촉자의 사후 행정요청은 내부 OC 재로그인이 아니라 별도 최소권한 Self-service Channel로 처리한다.

요청 Candidate:
- 해촉증명서
- 경력증명서
- 근무/위촉 사실 확인
- 재직/퇴직 관련 증명
- 원천징수/지급 관련 서류 요청
- 개인정보/연락처 정정
- 기타 HR 요청

## Request Flow
`본인확인 → Request 제출 → HR Queue → 검토 → 보완요청 optional → Document Generation/Manual Processing → Approval when required → Secure Issue/Reply → 확인 → Complete → Audit`

## Pending
Person Master Physical Owner, Shared IAM/본인확인 방식, Worker Type/State, HR Document Template/법적요건, 보존/파기정책, SLA, Compensation Formula/Approval.
