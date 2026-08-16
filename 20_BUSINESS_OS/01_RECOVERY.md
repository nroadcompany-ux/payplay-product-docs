# PayPlay Business OS Recovery Summary

| 항목 | 내용 |
|---|---|
| File Path | `20_BUSINESS_OS/01_RECOVERY.md` |
| Document ID | `PP-BOS-RECOVERY-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Recovery 근거용. Production Current 확정 기준으로 단독 사용 금지 |

## Recovery 기준
`기존 CSM/CSMM + PayPlay OS TEST Prototype + 현재 공식 방향 + 향후 사업장 운영 기능 → PayPlay Business OS`

Source Authority:
1. Owner Decision
2. Official Document
3. Existing Implementation
4. Existing Documentation
5. Inference

## CSM/CSMM 계승
### Reuse 우선
- FAQ
- Manual / Program Download
- POS / Device Knowledge
- 기존 신청 UX

### Modify / Merge
- A/S·소모품·매출자료·원격지원 요청
- 공지·지원 상태
- OC Handoff

### Refactor / Deprecated 후보
- localStorage 운영 Master 사용
- Browser direct DB access
- Mock Data 운영값 오인

## OS TEST
Historical Prototype. 운영 Production Source가 아님.
회수된 방향: Home, 매출·입금, 오늘 할 일, 매장 상태, 디지털 매장관리, 고객지원, 상품·서비스, AI 매니저, Quick Action.

## Gap
- 최신 CSMM Repository/Branch/Commit/DB Current
- Auth / Store Scope / Permission
- Runtime / Auto Launch
- 외부 Source 실제 연결
- OC Handoff Physical Contract
