# PayPlay OC

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/README.md` |
| Document ID | PP-OC-README-001 |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | `10_OC` 문서 진입점 및 상태/읽기순서 안내. 개별 APPROVED 문서의 SOT 상태를 대체하지 않음. |

## 역할
PayPlay 내부·외부 운영인력이 사용하는 운영체계. 고객, 영업, 견적, 계약, 설치, AS, 재고, 상품, 정책, 재무, HR, 경영, Decision, 회사 운영을 다룬다.

## 읽기 순서
1. `01_RECOVERY/`
2. `02_DOMAIN_SCOPE/`
3. `03_CAPABILITIES/`
4. `06_ENTITY_DATA/`
5. `04_FLOWS/user-and-operations-flows.md`
6. `05_REQUIREMENTS_POLICIES/detailed-requirements-and-business-policies.md`
7. `07_ARCHITECTURE/`
8. `08_SPECIFICATIONS/`
9. `09_DECISIONS/`
10. `10_AUDIT/OC_TRACEABILITY_GAP_AUDIT_v1.md`

## APPROVED / SOT YES
- `04_FLOWS/user-and-operations-flows.md`
- `05_REQUIREMENTS_POLICIES/detailed-requirements-and-business-policies.md`
- `06_ENTITY_DATA/ENTITY_DATA_ARCHITECTURE.md`
- `06_ENTITY_DATA/SHARED_ENTITY_DECISION_APPLIED.md`
- `09_DECISIONS/DECISION_REGISTER.md`
- `10_AUDIT/OC_TRACEABILITY_GAP_AUDIT_v1.md`

## WORKING / SOT NO
Recovery, Domain/Scope, Capability Inventory, Permission/Security/Credential, State/Transition, Commercial Policy implementation architecture, Migration/Identity/DQ, API/Service Boundary, People/HR Spec, Screen Traceability Summary.

## PENDING
`09_DECISIONS/PENDING_REGISTER.md`

## Gate
Final Documentation = PASS WITH PENDINGS; Follow-up Architecture = APPROVED; Development Planning/Specification = CONDITIONALLY APPROVED; Development Ready/QA Ready = 아직 아님.

## Structural Pending
Person Master 물리 위치 / Merchant Account 최종 구조 / Shared IAM 물리 Architecture.

## Legacy Preservation
기존 TMS Capability는 신규 OC 화면에 보이지 않는다는 이유로 삭제하지 않는다. Development Gate 전에 Legacy Capability Loss Audit을 수행한다.
