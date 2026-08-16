# Shared Entity Decision Applied — PayPlay OC

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/06_ENTITY_DATA/SHARED_ENTITY_DECISION_APPLIED.md` |
| Document ID | PP-OC-ENTITY-DECISION-001 |
| Status | APPROVED |
| Source of Truth | YES |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Shared Entity Owner Decision을 OC Entity/Data Architecture에 적용하는 공식 기준. |

## Main PM Decision Result
| No. | 항목 | 판정 | OC 적용 |
|---|---|---|---|
| 1 | Customer Account | 승인 | Decision |
| 2 | Person Master | Common Infrastructure 검토 | Logical use / Physical Pending |
| 3 | Merchant Account | 수정 필요 | Final structure Pending |
| 4 | Store 양도양수 Identity | 승인 | Decision |
| 5 | Legal Entity 변경 이력 | 승인 | Decision |
| 6 | Shared IAM / Permission Owner | Common Infrastructure 검토 | Logical Permission only / Physical Pending |
| 7 | Product / Commercial Policy Owner | 승인 | OC Master Owner |

## Decision Guards
- Customer Account는 법적 주체가 아니다.
- Same-site continuity를 Store Identity 핵심 Signal로 사용하되 예외는 Human Review한다.
- Legal Entity는 역할·기간 Assignment History로 관리한다.
- Product / Commercial Policy Master Owner는 OC다.

## Pending Guards
- Person Master 물리 위치 미확정
- Merchant Account 기존 Working 정의를 최종 정의로 사용 금지
- Shared IAM Auth/Session/User/Membership 물리구조 확정 금지

## Migration Impact
가능: Customer Account Candidate, Store Candidate, Legal Entity Assignment Candidate.
금지: Person Master Import Target 확정, Merchant Account 자동생성, Shared IAM Physical Migration.
