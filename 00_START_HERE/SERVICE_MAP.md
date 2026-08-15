# Service Map

| 항목 | 내용 |
|------|------|
| Document ID | PP-DOC-SERVICEMAP-001 |
| Status | WORKING |
| Last Reviewed | 2026-08-15 |

## 전체 서비스 맵

```
PayPlay Ecosystem
│
├─ [OSP] PayPlay OSP (Online Sales Platform / 온라인 영업 플랫폼)
│   ├─ Traffic / Website / Discovery
│   ├─ Lead / Conversion / Attribution
│   ├─ Analytics / Marketing Decision
│   └─ → OC에 Lead Handoff
│
├─ [OC] PayPlay OC (운영 센터)
│   ├─ 영업 실행 / Quote / Contract
│   ├─ Fulfillment / Installation / AS
│   ├─ CS / Case 관리
│   └─ 가맹점 내부 운영 전반
│
├─ [BOS] PayPlay Business OS (비즈니스 운영체계 / 내부 약칭: PPOS)
│   ├─ 사장님 매장 운영 Surface
│   ├─ 마케팅 도구 / 데이터 / 리포트
│   └─ PayPoint (Hosted / Owned by Marketing Play / 매장 운영 Surface 담당)
│
└─ [Connected]
    ├─ Marketing Play (PayPoint Owner)
    └─ SaengZone (독립 연결)
```

## 서비스 경계 원칙

| 서비스 | 역할 | 아닌 것 |
|--------|------|---------|
| OSP | Traffic·Lead·Conversion·Attribution·Marketing Decision | 사람 상담·계약 실행 State의 Master |
| OC | Lead Handoff 이후 영업·계약·설치·CS 실행 | 외부 유입 채널 관리 |
| Business OS | 사장님 매장 운영 Surface·성장 도구 | 하드웨어 제어·내부 운영 관리 |

> OSP 하위에 POS·테이블오더·키오스크·카드단말기를 배치하지 않는다.
> 해당 하드웨어 제품은 별도 Product 체계로 관리하며 OSP 구조와 혼합하지 않는다.
