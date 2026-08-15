# Entity Ownership Matrix (엔터티 소유권 매트릭스)

| 항목 | 내용 |
|------|------|
| Document ID | PP-SA-EOM-001 |
| Status | WORKING |
| Last Reviewed | 2026-08-15 |

> Pending 항목은 임의 확정 금지.
> Owner가 불확실한 항목은 근거 없이 배정하지 않고 Pending으로 유지한다.

| Entity | Owner Service | Shared With | Status | 비고 |
|--------|--------------|-------------|--------|------|
| Merchant (가맹점) | OC | OSP, Business OS | WORKING | |
| Person (사람) | TBD | 전체 | **PENDING** | Common Infrastructure 검토 후 결정 |
| Contract (계약) | OC | — | WORKING | |
| Device (단말기/장비) | TBD | OC, Business OS | **PENDING** | 기존 OC/Business OS Architecture 기준 재검토 필요. 근거 확정 전 배정 보류. |
| PayPoint | Marketing Play | Business OS | APPROVED | Marketing Play 소유 / Business OS Hosted |
| Merchant Account | TBD | — | **PENDING** | 최종 구조 미확정 |
| Commercial Policy | OC | OSP, Business OS | WORKING | OC Master Owner |
| Quote / Contract | OC | — | WORKING | |
| Case / CS | OC | — | WORKING | |

## 변경 이력

| 일자 | 항목 | 변경 내용 |
|------|------|-----------|
| 2026-08-15 | Device | Owner = OSP 삭제. 근거 없음 확인. OC/Business OS Architecture 기준 재검토 필요로 PENDING 전환. (Main PM REVISION 지시) |
