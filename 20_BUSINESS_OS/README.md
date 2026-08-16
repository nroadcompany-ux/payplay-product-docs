# PayPlay Business OS (비즈니스 운영체계)

| 항목 | 내용 |
|------|------|
| Document ID | PP-BOS-README-001 |
| Product / Service | PayPlay Business OS |
| 내부 공식 약칭 | PPOS |
| Document Type | Service Overview |
| Status | WORKING |
| Source of Truth | NO (WORKING 단계) |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-15 |
| Development Use | ❌ 개발 확정 기준 사용 불가 |

---

## 역할

매장 사장님·구성원의 **Store 운영 Surface**를 담당하는 비즈니스 운영체계.

- 매장 운영 Surface
- Store Runtime 운영데이터와 Self-service 접점
- OC의 계약/상품/정책 결과 Projection 소비
- 마케팅 도구 / 데이터 / 리포트 / 성장 도구

> PPOS는 별도 최상위 Product가 아니며, PayPlay Business OS의 내부 공식 약칭이다.

---

## Connected Products

| Product | Product Owner / 소속 | Hosted In | Business OS 역할 |
|---------|---------------------|-----------|------------------|
| PayPoint | Marketing Play | PayPlay Business OS | 매장 운영 Surface 담당 |

### PayPoint 문서 입고 기준 (2026-08-15 변경)

PayPoint 상세 연구문서는 **이 Repository(`payplay-product-docs`)에도 입고 가능**하다.

단, 아래 원칙을 유지한다.

- Product Owner / 소속 = **Marketing Play** (변경 금지)
- Hosted In = PayPlay Business OS
- Business OS는 Hosted In 및 매장 운영 Surface 담당
- **Repository Location ≠ Product Ownership**

상세 관계 → [PAYPOINT_RELATIONSHIP.md](../40_CONNECTED_PRODUCTS/PAYPOINT_RELATIONSHIP.md)

---

## 경계 원칙

| 구분 | 내용 |
|------|------|
| Business OS가 담당하는 것 | 매장 운영 Surface, Store Runtime 데이터, Self-service, 성장 도구 |
| Business OS가 담당하지 않는 것 | 내부 운영 관리(OC), 외부 유입·Lead 확보(OSP) |

동일 Field의 Dual Master를 만들지 않는다.

---

## 상세 문서

작업 예정 — Business OS 세션 연구 결과를 Repository IA 기준에 맞춰 정식 입고 예정.
