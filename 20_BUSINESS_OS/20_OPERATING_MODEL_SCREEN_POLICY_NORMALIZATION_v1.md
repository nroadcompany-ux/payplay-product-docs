# PayPlay Business OS — Operating Model & Screen Architecture Policy Normalization v1

| 항목 | 내용 |
|---|---|
| File Path | `20_BUSINESS_OS/20_OPERATING_MODEL_SCREEN_POLICY_NORMALIZATION_v1.md` |
| Document ID | `PP-BOS-POLICY-NORM-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | R01~R11 Trace Working Baseline. Development Ready 아님 |

## R01~R11 정규화
- R01 Store Context: 모든 Screen/Action은 Store Context와 Scope 유지.
- R02 Owner/Staff/Permission: Role + Function Permission + Sensitive Permission + Shared POS Context.
- R03 Shared POS/Sensitive: Default Safe, View ≠ Execute, View ≠ Export.
- R04 Home: Task/Alert/Signal/Request 중심. 자동 Store State 전제 없음.
- R05 AI Manager: 사용자 권한 상속, 권한 밖 데이터 답변 금지, 중요 Action Preview 후보.
- R06 Employee/Work: Membership / Attendance / Task / Manual / Checklist / Work Time. 근무시간 ≠ 급여.
- R07 PayPoint: Owner=Marketing Play, Hosted In=Business OS, Routine/High-risk Action 분리, Payment Event Path PENDING.
- R08 OC Handoff/Remote Support: BOS Entry·Preview·Status / OC 실제 처리. Physical Contract PENDING.
- R09 Failure/Retry/Recovery: Confirmed / Pending / Failed / Unknown. Unknown을 성공으로 승격 금지.
- R10 POS Runtime/Launcher: Full / Compact / Widget 후보, 타사 POS 허용 방향, Launcher PENDING.
- R11 Audit/Privacy/Consent/Integration Health: Sensitive Action, Session/Cache, AI History, Export 위험 추적. Physical Ownership PENDING.

## 유지 PENDING
Primary Navigation / Owner-Staff Role Matrix / Store State Auto / PayPoint Event Path / Shared POS Re-auth·Session / Shared IAM / Person Master / Merchant Account / BOS→OC Physical Handoff / Runtime Launcher.
