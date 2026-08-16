# PayPlay OC Definition / Scope / Domain

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/02_DOMAIN_SCOPE/OC_DEFINITION_SCOPE.md` |
| Document ID | PP-OC-SCOPE-001 |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | OC 책임범위·Domain/Bounded Context 작업 기준. 일부 물리 책임은 후속 결정 가능. |

## OC Definition
PayPlay OC는 PayPlay 내부·외부 운영인력이 사용하는 운영체계다.

## Service Boundary
- OSP: 외부 유입·설명·신청·Lead 생성
- OC: Lead Handoff 이후 사람 중심 영업, 견적/승인, 계약, 설치, AS, 상품/정책, 내부 운영
- Business OS: 매장 사장님·구성원의 Store 운영 Surface / Self-service

동일 Business State를 여러 서비스가 Dual Master로 소유하지 않는다.

## Domain Set
1. CUSTOMER
2. SALES
3. CONTRACT
4. INSTALLATION
5. SERVICE / AS
6. PRODUCT
7. INVENTORY / SUPPLY
8. FINANCE
9. PEOPLE / HR
10. COMPENSATION
11. MANAGEMENT
12. DECISION
13. COMMON

## Restricted Context
FINANCE / PEOPLE-HR / COMPENSATION / MANAGEMENT / DECISION / Commercial Restricted Field.

## Customer 360
Customer 360은 Source Master가 아니라 Aggregate Projection / Workbench다.

## Pending
- Inventory/Supply physical split
- Finance/Billing/Receivable detail
- Person Master physical
- Merchant Account final
- Shared IAM physical
