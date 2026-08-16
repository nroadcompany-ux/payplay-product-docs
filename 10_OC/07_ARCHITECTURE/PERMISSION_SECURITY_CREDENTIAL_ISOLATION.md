# Permission / Security / Credential Isolation Architecture

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/07_ARCHITECTURE/PERMISSION_SECURITY_CREDENTIAL_ISOLATION.md` |
| Document ID | PP-OC-ARCH-SEC-001 |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | OC 논리 권한·민감정보·Credential 격리 설계 기준. Shared IAM 물리구현 확정문서 아님. |

## Permission Model
`Role + Row Scope + Field Visibility + Action Permission + Approval Authority + Temporary/Delegated Grant + Audit + AI Access`

메뉴 숨김만으로 보안을 구현하지 않는다.

## Row Scope
Working Scope: `ALL / ORG / TEAM / OWNED / ASSIGNED / PARTICIPATING / EXPLICIT_SHARED / NONE`.
외부 영업·기사·Vendor는 Assigned / Explicit Shared 최소범위를 기본으로 한다.

## Field Sensitivity
- General
- Personal
- Commercial Restricted
- Finance Restricted
- HR Restricted
- Executive Restricted

## Action Separation
View와 Action, Approval Authority를 분리한다.

## AI Security
`Authorized Retrieve → Suggest → Prepare → Human Confirm → Re-Authorization → Domain Command → Audit`.
AI는 사용자의 권한 Ceiling을 넘거나 Source DB를 직접 수정하지 않는다.

## Credential Isolation
- 일반 Customer/Store Master에 Secret Payload 저장 금지
- Core에는 Credential Reference/Metadata만
- Secret은 별도 Secret Store/Vault 후보
- Reset/Rotate/Reissue 우선
- Search/AI/일반 Export/Activity Log에 Secret 원문 금지
- Reveal/Copy/Rotate/Delete/Import/Export 시도 Audit
- 외부인력 기본 Secret Access 금지

## Physical Pending
- Shared IAM 물리 Architecture
- Auth/Session/User/Membership Schema
- Vault Provider
- Person Master 물리 Owner
