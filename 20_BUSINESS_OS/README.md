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
