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
5. `04_FLOWS/USER_AND_OPERATIONS_FLOWS.md`
6. `05_REQUIREMENTS_POLICIES/DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md`
7. `07_ARCHITECTURE/`
8. `08_SPECIFICATIONS/`
9. `09_DECISIONS/`
10. `10_AUDIT/OC_TRACEABILITY_GAP_AUDIT_v1.md`

## Developer Package (2026-08-21 입고 · FREEZE READY / SOT NO)
공식 Reading Order `#1 → #2 → #3 → #4`. 안내는 `DEVELOPER_PACKAGE_GUIDE.md`.
- `#1` `07_ARCHITECTURE/SERVICE_ARCHITECTURE_MENU_DEPTH.md` — PP-OC-SVC-ARCH-MENU-001
- `#2` `04_FLOWS/USER_AND_OPERATIONS_FLOWS.md` — PP-OC-USER-OPS-FLOW-001
- `#3` `05_REQUIREMENTS_POLICIES/DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md` — PP-OC-REQ-BIZ-POLICY-001
- `#4` `08_SPECIFICATIONS/SCREEN_NAVIGATION_TRACEABILITY.md` — PP-OC-SCREEN-NAV-TRACE-001
- `09_DECISIONS/FINAL_PENDING_REGISTER.md` — PP-OC-FINAL-PENDING-REGISTER-001

Main PM 승인 전이므로 APPROVED / Source of Truth YES가 아니다.

## SUPERSEDED (2026-08-21 · 삭제하지 않음)
- `04_FLOWS/user-and-operations-flows.md` (PP-OC-FLOWS-001) → `04_FLOWS/USER_AND_OPERATIONS_FLOWS.md`
- `05_REQUIREMENTS_POLICIES/detailed-requirements-and-business-policies.md` (PP-OC-REQS-001) → `05_REQUIREMENTS_POLICIES/DETAILED_REQUIREMENTS_BUSINESS_POLICIES.md`

Header 표기만 변경했고 본문은 보존된다. 기존 `OC-FLOW-*` 식별자 추적용으로 계속 참조 가능하며 신규 개발 기준으로는 사용하지 않는다.

## APPROVED / SOT YES
- `06_ENTITY_DATA/ENTITY_DATA_ARCHITECTURE.md`
- `06_ENTITY_DATA/SHARED_ENTITY_DECISION_APPLIED.md`
- `09_DECISIONS/DECISION_REGISTER.md`
- `10_AUDIT/OC_TRACEABILITY_GAP_AUDIT_v1.md`

## WORKING / SOT NO
Recovery, Domain/Scope, Capability Inventory, Permission/Security/Credential, State/Transition, Commercial Policy implementation architecture, Migration/Identity/DQ, API/Service Boundary, People/HR Spec, Screen Traceability Summary.

## PENDING
`09_DECISIONS/PENDING_REGISTER.md` · `09_DECISIONS/FINAL_PENDING_REGISTER.md` (Developer Package Final Gate Index)

## Gate
Final Documentation = PASS WITH PENDINGS; Follow-up Architecture = APPROVED; Development Planning/Specification = CONDITIONALLY APPROVED; Development Ready/QA Ready = 아직 아님.

## Structural Pending
Person Master 물리 위치 / Merchant Account 최종 구조 / Shared IAM 물리 Architecture.

## Legacy Preservation
기존 TMS Capability는 신규 OC 화면에 보이지 않는다는 이유로 삭제하지 않는다. Development Gate 전에 Legacy Capability Loss Audit을 수행한다.
