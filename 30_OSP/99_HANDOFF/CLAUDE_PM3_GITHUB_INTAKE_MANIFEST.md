# Claude PM3 GitHub Intake Manifest — PayPlay OSP

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/99_HANDOFF/CLAUDE_PM3_GITHUB_INTAKE_MANIFEST.md` |
| Document ID | `PP-OSP-GH-INTAKE-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | GitHub 입고 작업용 |

---

## 1. Repository

`nroadcompany-ux/payplay-product-docs`

## 2. Target

`30_OSP/`

---

## 3. Existing GitHub File

### `30_OSP/README.md`

**Action: UPDATE REQUIRED**

기존 README는 존재함.
현재 공식 OSP 정의와 Boundary는 대체로 보정되어 있으나
본 패키지 README 기준으로 Documentation Index / Pending / Development Use를 정합화한다.

---

## 4. New Files

- `01_RECOVERY/RECOVERY_SUMMARY.md`
- `02_DEFINITION_SCOPE/OSP_DEFINITION_VISION_SCOPE.md`
- `03_DOMAIN_ARCHITECTURE/OSP_DOMAIN_ARCHITECTURE.md`
- `04_CAPABILITIES/OSP_CAPABILITY_INVENTORY.md`
- `05_WEBSITE_SALES/WEBSITE_ARCHITECTURE.md`
- `05_WEBSITE_SALES/SALES_CONTENT_STRUCTURE.md`
- `06_ACQUISITION/TRAFFIC_ACQUISITION.md`
- `07_DISCOVERY_CONVERSION/DISCOVERY_SALES_EXPERIENCE.md`
- `07_DISCOVERY_CONVERSION/CONVERSION_LEAD_CAPTURE.md`
- `08_HANDOFF/OSP_OC_HANDOFF.md`
- `09_ATTRIBUTION_ANALYTICS/ATTRIBUTION_ANALYTICS.md`
- `10_ADMIN/MARKETING_DECISION_OSP_ADMIN.md`
- `11_FLOWS/user-and-operations-flows.md`
- `12_REQUIREMENTS_POLICIES/detailed-requirements-and-business-policies.md`
- `13_ENTITY_RELATIONSHIPS/LEAD_PERSON_STORE_RELATIONSHIP.md`
- `14_COMMERCIAL/OFFER_QUOTE_COMMERCIAL_POLICY.md`
- `15_DECISIONS/DECISION_QUEUE_PENDING.md`
- `16_AUDIT/OSP_TRACEABILITY_GAP_AUDIT_v0.1.md`

---

## 5. APPROVED Documents

- `02_DEFINITION_SCOPE/OSP_DEFINITION_VISION_SCOPE.md`
- `03_DOMAIN_ARCHITECTURE/OSP_DOMAIN_ARCHITECTURE.md`
- `08_HANDOFF/OSP_OC_HANDOFF.md`
- `13_ENTITY_RELATIONSHIPS/LEAD_PERSON_STORE_RELATIONSHIP.md`
- `14_COMMERCIAL/OFFER_QUOTE_COMMERCIAL_POLICY.md`

---

## 6. WORKING Documents

- README
- Recovery
- Capability Inventory
- Website Architecture
- Sales Content
- Traffic / Acquisition
- Discovery / Conversion
- Attribution / Analytics
- Marketing Decision / OSP Admin
- User & Operations Flows
- Detailed Requirements & Business Policies
- Decision Queue
- Traceability / Gap Audit

---

## 7. PENDING Items

### Mandatory Shared Architecture Pending
- Person Master 물리 위치
- Merchant Account 최종 구조
- Shared IAM 물리 Architecture

### Additional Working / Pending
- OSP → OC Physical API
- OC → OSP Outcome Physical Interface
- Advertising Spend Source / API
- Attribution Model / Window
- KPI 최종 공식 산식
- Nurture / Messaging 최종 운영구조
- AI Recommendation / Execution Authority
- Smart Ground Naming / Advanced Scope

---

## 8. OSP → OC Boundary Check

**PASS**

OSP:
온라인 유입·탐색·전환·Lead 생성·Handoff·Attribution

PayPlay OC:
Accepted 이후 담당자 배정·사람 상담·공식 Quote·Contract·운영

Received ≠ Accepted.

---

## 9. GitHub 입고 후 Claude PM3 회신 요청

- 실제 입고 파일 목록
- 신규 / 변경 구분
- Commit SHA
- 기존 문서 충돌 / 중복 여부
- APPROVED / WORKING / PENDING 보존 여부
- 추가 Main PM 검토 필요사항
