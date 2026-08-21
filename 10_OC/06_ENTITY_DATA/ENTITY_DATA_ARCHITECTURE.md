# PayPlay OC Entity / Data Architecture

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/06_ENTITY_DATA/ENTITY_DATA_ARCHITECTURE.md` |
| Document ID | PP-OC-ENTITY-001 |
| Status | APPROVED |
| Source of Truth | YES |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Main PM Shared Entity Decision을 반영한 OC Logical Entity/Data 기준선. Pending 물리구조 확정에는 사용 금지. |

## Core Backbone
```text
Customer Account
└─ Store N
    ├─ Opportunity / Quote / Contract / Case / Asset / Activity N
    ├─ Legal Entity Assignment N
    ├─ Person Relationship N [logical]
    └─ Merchant access/account relationship [pending]

Product / Service
└─ Commercial Policy
    └─ Policy Version
        └─ Applied Policy Snapshot
```

## Customer Account — APPROVED
정의: **동일 실질 운영관계로 PayPlay가 통합 관리하는 가맹점그룹**.
- 법적 계약주체가 아니다.
- 사업자등록번호의 주체가 아니다.
- Store와 동일하지 않다.
- 계약/PG/정산은 해당 시점 Legal Entity Assignment를 따른다.

## Store — APPROVED
실제 서비스·설치·운영·AS가 발생하는 사업장 단위다.
- 동일 장소 + 운영/장비 연속성 유지 → 기존 Store ID 유지 Candidate
- 타지역 이동 → 신규 Store 우선
- 동일 상호/동일 실질 운영자만으로 Store 유지 금지
- 애매하면 Human Review

## Legal Entity Assignment — APPROVED
Store에 단일 `legal_entity_id`를 고정하지 않는다.
- BUSINESS_REGISTRATION_HOLDER
- CONTRACTING_PARTY
- BILLING_PARTY
- PG_MERCHANT_PARTY
- SETTLEMENT_PARTY

역할별 기간·Source·Evidence를 보존한다.

## Person — Logical / Physical PENDING
Person Reference/Relationship은 필요하나 Physical DB 위치, 최종 Owner, Shared Identity와의 물리관계는 확정하지 않는다.

## Merchant Account — PENDING
Customer Account/Store/User Identity와 동일 Entity로 선확정하지 않으며 독립 `merchant_account` Table을 선생성하지 않는다.

## Shared IAM — Logical Requirement / Physical PENDING
OC 권한 요구: `Role + Row Scope + Field Visibility + Action + Approval + Audit + AI Access`.
Auth/Session/User/Membership Physical Schema는 확정하지 않는다.

## Product / Commercial Policy — APPROVED
OC가 Product / Commercial Policy Master Owner다.
OSP는 승인된 Offer/Price/Promotion Projection을 소비하고 Business OS는 Store Applied Result를 조회한다.
