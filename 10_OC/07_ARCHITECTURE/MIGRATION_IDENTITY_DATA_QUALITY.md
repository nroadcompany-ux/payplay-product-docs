# Migration / Identity Resolution / Data Quality Architecture

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/07_ARCHITECTURE/MIGRATION_IDENTITY_DATA_QUALITY.md` |
| Document ID | PP-OC-ARCH-MIG-001 |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Legacy TMS/Sheet/WDI 데이터를 OC Core로 이관하기 위한 DQ·Identity·Migration Working Architecture. |

## Pipeline
`Raw → Snapshot → Staging → Normalize/Parse → DQ → Entity Candidate → Conflict Queue → Human Review → Core Import → Legacy Link → Reconciliation`

## Principles
- Legacy 거대 Row를 그대로 신규 Master로 복사하지 않는다.
- Customer Account / Store / Legal Entity / Person Relationship을 의미적으로 분리한다.
- 사업자번호/TID/전화/상호/주소 한 Signal로 자동 Merge하지 않는다.
- Import는 Idempotent해야 한다.
- Ambiguous는 Human Review.

## Confirmed Source Facts
Legacy B에서 약 2,913 Row × 122 Column, Store Candidate 약 1,112, 중복/Collision Candidate, Login ID/PW/Key 혼재, 다수 공급품목 표현, Commercial Policy Formula Error가 확인됐다.

## Identity Cases
동일 실질운영자-다중Store-다른명의, 동일사업자-다중Store, 같은 장소 양도양수, 타지역 이전, 법인명≠상호, 계약자≠PG/정산 명의, Identifier 재사용/이동.

## Product Alias
`P{n}/T{n}/K{n}/NFC{n}/QR{n}/CC{n}`는 수량. `인8`은 인터넷 월 8,000원, `배4`는 배달앱 4개. 숫자 suffix의 일괄 의미 추정 금지.

## Pending
Person Master Import Target, Merchant Account Migration Rule, Shared IAM Migration Target.
