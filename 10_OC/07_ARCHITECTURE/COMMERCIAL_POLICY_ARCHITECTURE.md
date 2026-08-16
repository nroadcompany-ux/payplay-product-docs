# Commercial Policy Architecture

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/07_ARCHITECTURE/COMMERCIAL_POLICY_ARCHITECTURE.md` |
| Document ID | PP-OC-ARCH-POLICY-001 |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | 승인된 OC Product/Commercial Policy Ownership Decision을 Version/Approval/Snapshot 구조로 구체화하는 Working Architecture. |

## Ownership Baseline
**APPROVED:** Product / Commercial Policy Master Owner = OC.

## Separation
Product Master는 정체성/Category/SKU/운영속성을 소유하고, Commercial Policy는 Price/Fee/PG/Revenue Share/Commission/CS-AS Fee/Contract Rule/Promotion/Offer를 소유한다.

## Lifecycle
`Policy Set → Version → Rule/Value/Formula → Validation → Approval → Effective → Applied Policy Snapshot`

## Guards
- Formula Error → Approval/Effective 차단
- `수정 중 / 미작성 / 확인 필요` Source → Effective 금지
- Effective Version 직접 수정 금지
- 과거 Quote/Contract/Case/Compensation Snapshot 불변
- 현재 Policy 변경으로 과거 Transaction 자동 재계산 금지

## Marketing Subscription
`PP1/PP2/PP3`는 마케팅 구독 1/2/3 계열로 재기획 중이며 정확 혜택/요율/PG 연계는 Pending. 월매출 1~3% Revenue Share 방향은 Proposal.
