# PayPlay OC Recovery Summary

| 항목 | 내용 |
|---|---|
| File Path | `10_OC/01_RECOVERY/RECOVERY_SUMMARY.md` |
| Document ID | PP-OC-RECOVERY-001 |
| Status | WORKING |
| Source of Truth | NO |
| Owner | PayPlay PM |
| Last Reviewed | 2026-08-16 |
| Development Use | Legacy TMS/WDI 자산을 OC Architecture에 승계하기 위한 Recovery 기준자료. 구현 확정문서 아님. |

## 1. Recovery Source
### TMS
실제 운영 Transaction 중심 Legacy Source. 고객/매장, Lead/상담/영업/방문, 견적/계약/전자계약, 설치/일정/현장, CS/AS, 배송/발주/재고/Vendor, 정산/비용/마진, Task/일정/미팅/프로젝트, 근태/휴가, 차량/주차/CCTV/회사정보, 사용자/보안, AI/팀채팅 자산이 확인됐다.

### WDI
재무·인사·경영·Decision 의미자산 중심 Legacy Source. `Decision → Reason → Expected Result → Actual Result → Review → Status` 및 재무/매출/거래/계좌/직원/거래처 개념이 확인됐다.

## 2. Recovery 원칙
- TMS/WDI를 독립 미래 Product로 복구하지 않는다.
- 유효 기능·업무 의미는 OC에 통합한다.
- Legacy DB/Table을 신규 공식 Entity로 자동 승격하지 않는다.
- Legacy 화면과 Capability를 1:1로 간주하지 않는다.
- 삭제 전 대체기능, 데이터 이력, Permission, Side Effect를 검증한다.

## 3. Primary Contribution
- TMS Primary: CUSTOMER / SALES / CONTRACT / INSTALLATION / SERVICE / PRODUCT / INVENTORY
- WDI Meaning Contribution: FINANCE / PEOPLE / COMPENSATION / MANAGEMENT / DECISION
- Merge: Quote / Finance / Vendor / People / Dashboard / Decision

## 4. Risk
- 자유형 상태값 및 Domain 혼재
- 권한/RLS 부족
- Customer/Store/Legal Entity 의미 혼합
- Login ID/PW/Key 일반 Master 혼재
- Commercial Policy Formula Error
- 단일 식별자 기반 자동 Merge 위험
- WDI 전사 데이터 이관범위 미확정

## 5. Structural Pending
- Person Master 물리 위치
- Merchant Account 최종 구조
- Shared IAM 물리 Architecture
