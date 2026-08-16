# PayPlay OSP Recovery Summary

| 항목 | 내용 |
|---|---|
| File Path | `30_OSP/01_RECOVERY/RECOVERY_SUMMARY.md` |
| Document ID | `PP-OSP-RECOVERY-001` |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay Main PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Recovery 근거 확인용 / 구현 확정 기준으로 단독 사용 금지 |

---

## 1. Recovery 목적

기존 PayPlay Website, OSP 관련 문서, 구현 자산, Owner Decision을 복원하여
현재 공식 OSP Architecture 기준선을 만든다.

---

## 2. Recovery 결과

### Fact

- 공식명은 **PayPlay OSP — Online Sales Platform**이다.
- OSP는 Website 중심 온라인 영업 플랫폼이다.
- Website는 OSP의 주요 Surface이지만 OSP 전체와 동일하지 않다.
- OSP는 온라인 유입·탐색·전환·Lead 생성·Attribution·Marketing Decision을 담당한다.
- PayPlay OC는 사람 상담·공식 Quote·Contract·설치·AS 등 내부 Sales/Operations 실행을 담당한다.
- Product / Commercial Policy Master는 현재 PayPlay OC이다.
- POS / 키오스크 / 테이블오더 / 카드단말기는 OSP 하위 Product가 아니다.

### Recovered Implementation Evidence

기존 OSP Website 구현에서는 다음 범주가 확인되었다.

- Public Website
- Product / Service presentation
- Contact / Inquiry / Request
- Signup / Login / MyPage
- Support / Ticket / Onboarding
- Admin CMS
- Marketing performance prototype
- 외부 내부운영시스템 전달 Adapter
- 기본 Meta Pixel / Lead·Contact Event

---

## 3. Legacy 처리 원칙

과거 코드·Repository·파일·Endpoint에 남아 있는 `TMS` 표기는
현재 Business / Architecture 용어로 사용하지 않는다.

필요 시 **Legacy Technical Identifier**로만 보존하고,
현재 공식 업무 명칭은 **PayPlay OC (Operations Center)**를 사용한다.

---

## 4. Recovery에서 확인된 Gap

- Runtime DB 참조와 관리 `schema.sql` 간 Drift
- 민감 Onboarding 문서 Storage의 Private 전제와 Public-read Schema 충돌
- 실제 OSP → OC `Accepted` Physical Interface 미확정
- OC → OSP Contract / Revenue Outcome Physical Interface 미확정
- Marketing Performance Admin의 MOCK 데이터
- UTM / Campaign / Creative / Click ID 기반 Closed-loop Attribution 미구현
- Automated Regression Test Evidence 부재

---

## 5. Recovery 판정

Recovery는 Business / Architecture 기준선을 만들기에는 충분하나
Physical API·DB·IAM·Runtime 상태까지 완결된 것은 아니다.

따라서 본 문서는 WORKING 상태를 유지한다.
