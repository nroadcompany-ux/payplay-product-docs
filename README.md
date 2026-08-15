# PayPlay Product Docs

> **공식 Product Documentation Repository**
> PayPlay OSP / OC / Business OS의 Owner Intent, Architecture, Specification 기준선을 관리합니다.

## 진입 순서
1. 이 README를 읽는다
2. [00_START_HERE/START_HERE.md](./00_START_HERE/START_HERE.md)로 이동한다

## Repository 역할
| 항목 | 내용 |
|------|------|
| 목적 | 개발자·AI가 따라야 하는 승인된 Product / Architecture / Specification 기준선 |
| 대상 | PayPlay OSP, OC, Business OS |
| 제외 | Notion 중간 메모, 미승인 Draft, Implementation Code |

## PayPlay 3축 구조
```
PayPlay
├─ PayPlay OSP (Online Sales Platform / 온라인 영업 플랫폼)
├─ PayPlay OC  (운영 센터)
└─ PayPlay Business OS  (비즈니스 운영체계 / 내부 약칭: PPOS)
```

## Connected Products
| Product | Ownership | Hosted In | 문서 위치 |
|---------|-----------|-----------|-----------|
| PayPoint | Marketing Play | PayPlay Business OS | marketing-play-product-docs (예정) |
| SaengZone | SaengZone | 독립 | saengzone-product-docs (예정) |

## Source of Truth 정책
- **Notion** = Recovery / 분석 / Working / Discussion / 중간 보고
- **이 Repository** = 승인된 Product / Architecture / Specification 기준선
- **Code Repository** = Implementation / DB / Test / Commit / PR

_Last Updated: 2026-08-15 | Status: WORKING_
