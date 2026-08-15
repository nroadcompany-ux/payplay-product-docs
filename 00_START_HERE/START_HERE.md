# START HERE

> 새 개발자·AI가 가장 먼저 읽어야 하는 문서입니다.
> 이 문서를 읽으면 PayPlay 전체 맥락을 빠르게 파악할 수 있습니다.

---

## Document Metadata
| 항목 | 내용 |
|------|------|
| Document ID | PP-DOC-START-001 |
| Product | PayPlay |
| Document Type | Navigation Guide |
| Status | WORKING |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-15 |
| Source of Truth | YES |
| Development Use | 진입점 안내 전용 |

---

## 1. PayPlay란 무엇인가

PayPlay는 외식업 사장님 대상 테이블오더, POS, 키오스크, 카드단말기, 마케팅 솔루션 등
풀라인업 결제·운영 솔루션을 제공하는 Business Growth Ecosystem이다.

2026-07-08 Genesis Day 기준으로 정체성을 "POS 회사"에서 "Business Growth Ecosystem"으로 전환했다.

---

## 2. 왜 만드는가

반복되는 고통을 줄이는 회사.
사장님의 운영 부담을 줄이고, 성장을 자동화하는 것이 PayPlay의 존재 이유다.

---

## 3. PayPlay 3축 구조

```
PayPlay
├─ PayPlay OSP     (Online Sales Platform / 온라인 영업 플랫폼)
├─ PayPlay OC      (운영 센터)
└─ PayPlay Business OS  (비즈니스 운영체계 / 내부 약칭: PPOS)
```

각 서비스 상세 → [PAYPLAY_OVERVIEW.md](./PAYPLAY_OVERVIEW.md)

---

## 4. Connected Products

| Product | Ownership | Hosted In | 관계 |
|---------|-----------|-----------|------|
| PayPoint | Marketing Play | PayPlay Business OS | Marketing Play 소유 / Business OS가 매장 운영 Surface 담당 / 문서: marketing-play-product-docs |
| SaengZone | SaengZone | 독립 | Connected / 문서: saengzone-product-docs |

> **중요:** Repository 위치 ≠ Product Ownership ≠ Documentation Ownership

---

## 5. 현재 개발 상태

| Gate | 판정 |
|------|------|
| Final Documentation Gate | PASS WITH PENDINGS |
| Follow-up Architecture Gate | APPROVED |
| Development Planning / Specification Gate | CONDITIONALLY APPROVED |
| Development Ready | ❌ 아직 아님 — 별도 Gate 재검수 필요 |
| QA Ready | ❌ 아직 아님 |

> ⚠️ Pending 항목 해소만으로 Development Ready가 자동 선언되지 않는다.
> Development Ready는 별도 Gate 재검수를 통해 판정한다.

---

## 6. Pending 항목 (임의 확정 금지)

- [ ] Person Master 물리 위치
- [ ] Merchant Account 최종 구조
- [ ] Shared IAM 물리 Architecture

---

## 7. 문서 읽는 순서

```
README.md
→ 00_START_HERE/START_HERE.md        ← 지금 여기
→ 00_START_HERE/PAYPLAY_OVERVIEW.md
→ 00_START_HERE/PRODUCT_VISION.md
→ 01_OWNER_INTENT/WHY_PAYPLAY.md
→ 02_SHARED_ARCHITECTURE/SERVICE_BOUNDARIES.md
→ 10_OC/ (OC 담당자)
→ 20_BUSINESS_OS/ (Business OS 담당자)
→ 30_OSP/ (OSP 담당자)
```

---

## 8. Code Repository 연결

| 항목 | 위치 |
|------|------|
| 이 문서 Repository | nroadcompany-ux/payplay-product-docs |
| 실제 개발 Repository | 별도 확인 필요 (Pending) |
