# PayPlay OC (운영 센터)

| 항목 | 내용 |
|------|------|
| Document ID | PP-OC-README-001 |
| Status | WORKING |
| Last Reviewed | 2026-08-15 |

## 역할
PayPlay 내부 운영팀이 사용하는 관리 시스템.
설치, CS, 계약, 가맹점 관리 등 운영 전 영역 담당.

## 문서 읽는 순서 (신규 개발자·AI 필독)

```
1. 이 README
2. 04_FLOWS/user-and-operations-flows.md          ← 전체 업무흐름 기준선
3. 05_REQUIREMENTS_POLICIES/detailed-requirements-and-business-policies.md  ← 기능요구사항·정책
4. 10_AUDIT/OC_TRACEABILITY_GAP_AUDIT_v1.md       ← Traceability·Gap 검수 결과
5. 07_ARCHITECTURE/ (추후 입고)
6. 08_SPECIFICATIONS/ (추후 입고)
```

> ⚠️ Audit부터 읽으면 전체 맥락을 거꾸로 파악하게 됩니다. 반드시 위 순서를 따르세요.

## 현재 개발 상태

| Gate | 판정 |
|------|------|
| Final Documentation Gate | PASS WITH PENDINGS |
| Follow-up Architecture Gate | APPROVED |
| Development Planning / Specification Gate | CONDITIONALLY APPROVED |
| Development Ready | ❌ 아직 아님 |
| QA Ready | ❌ 아직 아님 |

## Pending (임의 확정 금지)

- [ ] Person Master 물리 위치
- [ ] Merchant Account 최종 구조
- [ ] Shared IAM 물리 Architecture

## 폴더 구조

| 폴더 | 내용 | 상태 |
|------|------|------|
| 01_RECOVERY | 기존 문서 복원 자료 | 예정 |
| 02_DOMAIN_SCOPE | 도메인 범위 정의 | 예정 |
| 03_CAPABILITIES | 기능 목록 | 예정 |
| 04_FLOWS | User & Operations Flow | ✅ 입고 완료 |
| 05_REQUIREMENTS_POLICIES | 상세 요구사항·비즈니스 정책 | ✅ 입고 완료 |
| 06_ENTITY_DATA | 엔터티·데이터 모델 | 예정 |
| 07_ARCHITECTURE | 아키텍처 | 예정 |
| 08_SPECIFICATIONS | 상세 명세 | 예정 |
| 09_DECISIONS | OC 의사결정 | 예정 |
| 10_AUDIT | Traceability & Gap Audit | ✅ 입고 완료 |
