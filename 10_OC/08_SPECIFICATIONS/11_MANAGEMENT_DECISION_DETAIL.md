# OC Restricted Domain Specification — Management Decision Detail v0.1

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/08_SPECIFICATIONS/11_MANAGEMENT_DECISION_DETAIL.md` |
| Document ID | `PP-OC-SPEC-DECISION-DETAIL-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Logical/Screen Specification. Physical implementation, authority thresholds, IAM structure are not finalized. |

> WDI Decision Engine에서 Recovery된 `Decision → Reason → Expected Result → Actual Result → Review` 의미자산과 OC-FLOW-008을 OC 운영용 Logical/Screen Specification으로 정규화한다. 기존 Owner Decision은 변경하지 않는다.

## 1. Phase Verdict

**PASS WITH POLICY / AUTHORITY PENDINGS — MANAGEMENT DECISION DETAIL SPEC COMPLETE**

Development Ready / QA Ready를 선언하지 않는다.

## 2. Core Lifecycle

```text
Problem / Situation
→ Decision Context
→ Alternatives / Options
→ Evidence / Rationale
→ Decision
→ Expected Result / Target / Success Criteria
→ Execution Handoff
→ Actual Result
→ Review / Retrospective
→ Learning
→ Follow-up Decision / Supersede when needed
```

## 3. Logical Entities

- Decision
- Decision Option
- Expected Result
- Execution Link
- Actual Result
- Decision Review
- Decision Relation

Expected Result는 결정 당시 기대를 별도로 보존한다.
Actual Result와 Review는 원 Decision과 Expected Result를 덮어쓰지 않고 후속 기록으로 보존한다.

## 4. Decision vs Approval

- **Decision**: 무엇을 선택했고 왜 선택했는지의 판단 기록.
- **Approval**: 특정 Source Business Action 실행 권한/예외에 대한 Workflow.

`Decision Recorded / Approved`가 곧바로 Contract, Finance, HR, Inventory 등의 Source State 변경을 의미하지 않는다.

필요 시:

```text
Decision
→ Approval Request
→ Authorized Domain Command
→ Execution Result
```

Approval이 필요한 Decision 유형은 PENDING이다.

## 5. Execution Handoff

Management Decision은 타 Domain DB를 직접 수정하지 않는다.

```text
Decision
→ Execution Plan / Work Link
→ Authorized Actor
→ Domain Command
→ Business / State / Approval Guard
→ Source Update
→ Activity / Audit
→ Execution Result Projection
```

## 6. Screen Architecture Candidate

### Decision Attention / Review Due
- Review Due
- Expected Result 측정시점 도달
- 실행 미착수/지연
- Actual Result 미기록
- Follow-up Decision 필요 후보

### Decision List
Filter candidates:
- Owner
- Domain / Context
- Decision date
- Review Due
- Active / Superseded / Archived candidate
- Restricted scope

### Decision Detail

```text
Context / Problem
Alternatives / Options
Evidence
Decision / Rationale
Expected Result
Execution Links
Actual Result
Review / Learning
Related / Parent / Superseded Decisions
Activity / Audit
```

### Outcome Review
Expected Result와 Actual Result를 병렬 비교한다.
Expected Result는 수정하지 않고 Actual / Variance / Review를 추가한다.

## 7. State Model Candidate

Decision Lifecycle:
`Draft / Under Review / Decided / Withdrawn / Superseded / Archived`

Outcome Tracking:
`Not Started / Execution Tracking / Review Due / Reviewed`

정확한 공식 State Name은 WORKING CANDIDATE이며 후속 State Matrix 정규화 전 확정하지 않는다.

## 8. Logical API Candidates

Query:
- `listDecisions`
- `getDecisionDetail`
- `getDecisionReviewDueProjection`
- `getDecisionExecutionProjection`

Command:
- `createDecisionDraft`
- `addDecisionOption`
- `updateDecisionDraft`
- `submitDecisionForReview`
- `recordDecision`
- `linkDecisionExecution`
- `recordActualResult`
- `submitDecisionReview`
- `supersedeDecision`
- `archiveDecision`

Generic status PATCH는 사용하지 않는다.

## 9. Permission / Security

`Role + Row Scope + Field Visibility + Action Permission + Approval Authority + Audit + AI Access`

- Restricted Evidence 접근권한이 없으면 Decision 화면에서도 원문을 노출하지 않는다.
- Search / Chat / AI도 같은 Authorization Ceiling을 따른다.
- Restricted Export / Reveal은 Audit 후보.

## 10. AI Guard

AI 가능:
- Evidence 요약
- 선택지 정리
- 장단점 비교
- Expected Result Draft
- Actual vs Expected 차이 요약
- Review Draft
- Follow-up Decision 후보 제안

AI 금지:
- 고위험 Decision 최종 확정
- Approval 권한 행사
- Finance / Contract / HR Source State 직접 변경
- Restricted Evidence 권한 우회

Pattern:
`Authorized Retrieve → Suggest / Draft → Human Confirm → Record / Authorized Domain Command → Audit`

## 11. WDI Reuse / Migration Boundary

Reuse:
- Decision
- Decision Reason
- Expected Result
- Actual Result
- Review

Do not reuse as canonical architecture:
- iframe prototype architecture
- global `app_state` JSON
- WDI standalone product structure
- assumption that all legacy WDI data belongs to PayPlay OC

Legacy WDI data migration scope remains `DQ-OC-WDI-001` PENDING.

## 12. Test Scenario Candidates

- Expected Result / Actual Result separate history
- Review cannot overwrite original rationale/expectation
- Restricted evidence access denial
- Decision cannot directly mutate Contract/Finance/HR/Inventory
- Superseded history preservation
- stale version conflict
- AI cannot autonomously decide/approve/commit
- Review Due remains projection
- Management KPI / Team Chat / AI regression
- Legacy WDI data cannot auto-migrate without scope approval

## 13. Pending

- Decision Authority / role authority
- Mandatory Reviewer
- Approval-required Decision types
- Confidentiality / Sensitivity classification
- official Decision State names
- Review Due rule / SLA
- KPI Metric Source detail
- DQ-OC-WDI-001
- Official Screen ID
- Person Master physical location
- Shared IAM physical Architecture

## 14. Next

**Cross-Service Integration Contract — OSP / Business OS ↔ OC v0.1**
