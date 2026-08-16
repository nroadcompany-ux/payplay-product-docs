# PayPlay Business OS

| 항목 | 내용 |
|---|---|
| File Path | `20_BUSINESS_OS/README.md` |
| Document ID | `PP-BOS-README-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | 개발 확정 기준 사용 불가. 승인된 Decision만 참조 가능 |

## 정의
PayPlay Business OS는 사업장 대표자와 구성원이 일상적인 운영·확인·문제 해결·업무 실행·전문 서비스 연결을 수행하는 **사업장 운영 Surface / Operating Layer**다.

## APPROVED
- 누구나 무료 사용 가능
- PayPlay POS 사용 필수 아님
- 타사 POS 사용자도 사용 가능
- 무료 근태관리 = 핵심 Acquisition Hook
- `매장관리` 1차 카테고리
- `고객·마케팅` 통합
- `상품·서비스` 독립
- `AI 매니저` 전역 Interface

## 관계
- PayPlay OC: 계약·설치·AS·재고·본사 운영 Owner
- PayPlay OSP: 외부 유입·Landing·온라인 영업
- PayPoint: Product Owner / 소속 = Marketing Play / Hosted In = PayPlay Business OS
- SaengZone: 독립 Product Owner, Hosted In / Uses 연구
- Marketing Play: Connected / Reads From 연구

## 공통 PENDING
- Person Master 물리 위치
- Merchant Account 최종 구조
- Shared IAM 물리 Architecture

## Business OS PENDING
- Primary Navigation 최종안
- Store Operating State 자동 판정 Rule
- Owner / Staff Role Matrix
- PayPoint 자동 적립 Event 실제 기술 경로

---

## Documentation Map

| 문서 | 내용 | Status | Source of Truth |
|---|---|---|---|
| `01_RECOVERY.md` | Recovery | WORKING | NO |
| `02_DEFINITION_VISION_SCOPE.md` | Definition / Vision / Scope | WORKING | NO |
| `03_DOMAIN_ARCHITECTURE.md` | Domain Architecture | WORKING | NO |
| `04_CAPABILITY_INVENTORY.md` | Capability Inventory | WORKING | NO |
| `05_CSM_CSMM_INHERITANCE.md` | 기존 CSM/CSMM 계승 구조 | WORKING | NO |
| `06_SERVICE_ARCHITECTURE.md` | Service Architecture | WORKING | NO |
| `07_NAVIGATION_IA.md` | Navigation / IA | WORKING | NO |
| `08_HOME_TODAYS_STORE_BLUEPRINT.md` | Home / 오늘의 매장 Blueprint | WORKING | NO |
| `09_DAYPART_STORE_OPERATING_STATE.md` | Daypart / Store Operating State | WORKING | NO |
| `10_OWNER_STAFF_OPERATING_MODEL.md` | Owner / Staff Operating Model | WORKING | NO |
| `11_USER_OPERATIONS_FLOWS.md` | User & Operations Flows | WORKING | NO |
| `12_REQUIREMENTS_BUSINESS_POLICIES.md` | Requirements & Business Policies | WORKING | NO |
| `13_STORE_OPERATIONS_SELF_SERVICE_AI.md` | Store Operations / Self Service / AI | WORKING | NO |
| `14_PAYPOINT_HOSTED_IN.md` | PayPoint Hosted In / Merchant Operating Surface | WORKING | NO |
| `15_OC_INTEGRATION.md` | Business OS ↔ OC Integration | WORKING | NO |
| `16_CONNECTED_PRODUCTS.md` | Connected Products | WORKING | NO |
| `17_DECISIONS_PENDING_RISKS.md` | Decisions / Pending / Risks | WORKING | NO |
| `18_TRACEABILITY_GAP_AUDIT.md` | Traceability / Gap Audit | WORKING | NO |
| **`19_STORE_OPERATING_MODEL_SCREEN_ARCHITECTURE_v1.md`** | **Store Operating Model v1 + Screen Architecture v1** | **WORKING** | **NO** |
| **`20_OPERATING_MODEL_SCREEN_POLICY_NORMALIZATION_v1.md`** | **R01~R11 Policy Normalization** | **WORKING** | **NO** |
| **`21_PHASE_REPORT_STORE_OPERATING_MODEL_SCREEN_ARCH_v1.md`** | **Phase Report** | **WORKING** | **NO** |

---

## Reading Order

```
1. 이 README                              ← 지금 여기
2. 02_DEFINITION_VISION_SCOPE             정의·비전·범위
3. 03_DOMAIN_ARCHITECTURE                 도메인 구조
4. 06_SERVICE_ARCHITECTURE                서비스 구조
5. 11_USER_OPERATIONS_FLOWS               업무 흐름
6. 12_REQUIREMENTS_BUSINESS_POLICIES      요구사항·정책
7. 19_STORE_OPERATING_MODEL_SCREEN_ARCHITECTURE_v1   Operating Model / Screen Architecture
8. 20_OPERATING_MODEL_SCREEN_POLICY_NORMALIZATION_v1 R01~R11 Trace
9. 14_PAYPOINT_HOSTED_IN / 15_OC_INTEGRATION         연계 관계
10. 17_DECISIONS_PENDING_RISKS            Decision / Pending 확인
11. 18_TRACEABILITY_GAP_AUDIT             Gap Audit
12. 21_PHASE_REPORT_...                   Phase 기록
```

> ⚠️ Audit이나 Phase Report부터 읽으면 전체 맥락을 거꾸로 파악하게 된다.

---

## 문서 등재의 의미

> ⚠️ **본 Documentation Map / Reading Order 등재는 아래 어느 것도 의미하지 않는다.**
>
> - 해당 문서의 **APPROVED 승격 아님**
> - **Source of Truth 승격 아님**
> - **Development Ready 아님**
> - **QA Ready 아님**
> - Primary Navigation 확정 아님
> - Physical API / DB / IAM 확정 아님
>
> 각 문서의 Status와 Source of Truth 표기를 개별 확인한다.
> 등재된 전 문서는 현재 `WORKING / Source of Truth NO` 상태다.
