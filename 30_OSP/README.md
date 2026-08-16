# PayPlay OSP — Online Sales Platform / 온라인 영업 플랫폼

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/README.md` |
| Document ID | `PP-OSP-README-001` |
| Product / Service | PayPlay OSP |
| Document Type | Service Overview / Documentation Index |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Architecture·Boundary 참고 가능 / Physical API·DB·IAM 구현 확정 기준으로 사용 금지 |

---

## 1. Official Name

**PayPlay OSP — Online Sales Platform / 온라인 영업 플랫폼**

PayPlay OSP는 단순 홈페이지가 아니다.

검색·광고·콘텐츠·소개·제휴 등에서 온라인 고객 유입을 만들고,
PayPlay Website를 중심으로 고객이 상품·서비스를 탐색·이해·비교한 뒤
상담·견적·신청으로 전환하도록 하며,
유효한 Lead를 생성하여 **PayPlay OC(Operations Center)**로 인계하는
온라인 영업 플랫폼이다.

---

## 2. Vision

> 사람이 먼저 설명하지 않아도 PayPlay가 온라인에서 고객을 유입하고,
> 상품·서비스를 이해시키고, 구매·상담 의도를 확보하며,
> 실제 영업조직으로 연결한 뒤 그 결과를 다시 마케팅 의사결정에 활용하는 구조를 만든다.

```text
Traffic / Acquisition
↓
Website / Sales Content
↓
Discovery / Sales Experience
↓
Conversion
↓
Lead Capture
↓
OSP → PayPlay OC Handoff
↓
OC Sales / Contract Outcome
↓
Attribution / Analytics
↓
Marketing Decision
↓
Next Execution
```

---

## 3. Official Responsibility Boundary

### OSP Responsibility

- Traffic / Acquisition
- Website
- Landing
- Sales Content
- Product / Service Discovery
- Approved Offer Presentation
- Conversion
- Consultation / Quote / Application Entry
- Required Consent Capture
- Lead Creation
- Lead Source / Attribution Context
- OSP → OC Handoff
- Handoff Monitoring
- Attribution / Analytics
- Marketing Decision Support
- OSP Admin

### PayPlay OC Responsibility

- Lead Assignment
- 사람 상담 실행
- Sales Activity
- 공식 Quote
- Contract
- Contract / Revenue Master
- Installation
- AS
- Inventory 및 내부 운영 Process

---

## 4. Product Ownership Guardrail

다음 제품을 OSP 하위 Product로 정의하지 않는다.

- POS
- 키오스크
- 테이블오더
- 카드단말기

OSP는 이들 Product를 온라인에서 소개·탐색·전환시키는 Sales Platform일 수 있으나,
해당 Product 자체의 Owner는 아니다.

---

## 5. Product / Commercial Policy Boundary

**Product / Commercial Policy Master Owner = PayPlay OC**

OSP는 Product, 판매가격, Package, Promotion,
Commercial Condition의 Master를 자체 생성하지 않는다.

OSP는 PayPlay OC에서 승인된 Product / Offer 정보를
Website·Landing·Product Page·Comparison·Recommendation·Conversion UI에 표현한다.

실제 고객별 공식 Quote와 Contract Price는
PayPlay OC의 Quote / Contract 영역이 Source of Truth이다.

---

## 6. Website Relationship

```text
PayPlay OSP
└─ PayPlay Website
   ├─ Homepage
   ├─ Landing
   ├─ Product / Service Pages
   ├─ Content / Insight
   ├─ Customer Center
   ├─ Smart Ground — WORKING / Naming Pending
   └─ Conversion UI
```

Website는 OSP의 주요 구현 Surface이지만 OSP 전체와 동일하지 않다.

---

## 7. Official Domain Architecture

1. Acquisition & Traffic
2. Website & Sales Content
3. Discovery & Sales Experience
4. Conversion & Lead Capture
5. Lead & OC Handoff
6. Campaign & Attribution
7. Sales Analytics & Optimization
8. Marketing Decision & OSP Admin

---

## 8. Shared Architecture Pending

다음 3건은 Pending을 유지한다.

- Person Master 물리 위치
- Merchant Account 최종 구조
- Shared IAM 물리 Architecture

OSP 문서가 위 사항을 임의 확정하지 않는다.

---

## 9. Documentation Map

| 폴더 | 내용 |
|---|---|
| 01_RECOVERY | Recovery Summary |
| 02_DEFINITION_SCOPE | OSP Definition / Vision / Scope |
| 03_DOMAIN_ARCHITECTURE | Domain Architecture |
| 04_CAPABILITIES | Capability Inventory |
| 05_WEBSITE_SALES | Website Architecture / Sales Content 구조 |
| 06_ACQUISITION | Traffic / Acquisition |
| 07_DISCOVERY_CONVERSION | Discovery / Sales Experience, Conversion / Lead Capture |
| 08_HANDOFF | OSP → PayPlay OC Handoff |
| 09_ATTRIBUTION_ANALYTICS | Attribution / Analytics |
| 10_ADMIN | Marketing Decision / OSP Admin |
| 11_FLOWS | User & Operations Flows |
| 12_REQUIREMENTS_POLICIES | Detailed Requirements & Business Policies |
| 13_ENTITY_RELATIONSHIPS | Lead / Person / Store Relationship |
| 14_COMMERCIAL | Offer / Quote / Commercial Policy |
| 15_DECISIONS | Decision Queue / Pending |
| 16_AUDIT | Traceability & Gap Audit |
| **17_SPECIFICATION** | **Sales Funnel / Attribution / Conversion / Admin Specification** |
| 99_HANDOFF | Claude PM3 GitHub Intake Manifest |

---

## 10. Reading Order

신규 개발자·AI는 아래 순서로 읽는다.

```
1. 이 README                         ← 지금 여기
2. 02_DEFINITION_SCOPE                 정의·범위
3. 03_DOMAIN_ARCHITECTURE              도메인 구조
4. 11_FLOWS                            업무 흐름
5. 12_REQUIREMENTS_POLICIES            요구사항·정책
6. 08_HANDOFF                          OC 인계 기준 (APPROVED)
7. 13_ENTITY_RELATIONSHIPS             Entity 관계 (APPROVED)
8. 17_SPECIFICATION                    Funnel/Attribution/Conversion/Admin 상세
9. 15_DECISIONS                        Decision / Pending 확인
10. 16_AUDIT                           Gap Audit
```

> ⚠️ Audit이나 Specification부터 읽으면 전체 맥락을 거꾸로 파악하게 된다.

### 주요 Specification

| 문서 | 경로 | Status | Source of Truth |
|---|---|---|---|
| Sales Funnel / Attribution / Conversion / Admin Specification | [17_SPECIFICATION/SALES_FUNNEL_ATTRIBUTION_CONVERSION_ADMIN_SPEC.md](./17_SPECIFICATION/SALES_FUNNEL_ATTRIBUTION_CONVERSION_ADMIN_SPEC.md) | WORKING | NO |

> ⚠️ **본 Documentation Map / Reading Order 등재는 해당 Specification 또는 OSP 전체를
> APPROVED / Source of Truth로 승격하는 의미가 아니다.**
> 각 문서의 Status와 Source of Truth 표기를 개별 확인한다.

---

## 11. Development Use Rule

Development Ready 및 QA Ready는 별도 Gate 승인 전까지 미승인 상태를 유지한다.
