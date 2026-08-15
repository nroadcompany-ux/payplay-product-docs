# Development Guardrails (개발 가드레일)

| 항목 | 내용 |
|------|------|
| Document ID | PP-DEV-GUARD-001 |
| Status | WORKING |
| Last Reviewed | 2026-08-15 |

## 핵심 원칙

1. **WORKING / REVIEW 문서를 개발 확정 기준으로 사용 금지**
2. **Pending 항목 임의 확정 금지**
3. **Proposal을 Decision으로 임의 승격 금지**
4. **기존 Owner Decision 변경 금지**
5. **Pending 해소만으로 Development Ready 자동 선언 금지 — 별도 Gate 재검수 필요**

## Document Status 기준

| Status | 개발 사용 가능 여부 |
|--------|-------------------|
| DRAFT | ❌ 불가 |
| WORKING | ❌ 불가 |
| REVIEW | ❌ 불가 |
| APPROVED | ✅ 가능 |
| SUPERSEDED | ❌ 구버전 — 사용 금지 |
| ARCHIVED | ❌ 불가 |

## 현재 개발 상태

| Gate | 판정 |
|------|------|
| Final Documentation Gate | PASS WITH PENDINGS |
| Follow-up Architecture Gate | APPROVED |
| Development Planning / Specification Gate | CONDITIONALLY APPROVED |
| Development Ready | ❌ 아직 아님 |
| QA Ready | ❌ 아직 아님 |

## Development Ready 판정 기준

Development Ready는 아래 조건을 모두 충족한 후 **별도 Gate 재검수**를 통해 판정한다.
Pending 3개 해소만으로 자동 Development Ready가 선언되지 않는다.

- [ ] Person Master 물리 위치 확정
- [ ] Merchant Account 최종 구조 확정
- [ ] Shared IAM 물리 Architecture 확정
- [ ] 위 항목 해소 후 **Main PM Gate 재검수 통과**
