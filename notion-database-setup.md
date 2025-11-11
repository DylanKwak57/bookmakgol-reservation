# 북막골 예약 시스템 - Notion 데이터베이스 설정 가이드

## 1. Notion 데이터베이스 생성

### Database Name: 북막골 예약 관리

### Properties 설정

다음 속성들을 정확히 생성하세요:

| Property | Type | Options/Description |
|----------|------|---------------------|
| 예약번호 | Title | 자동 생성 ID (BOOK-YYYYMMDD-XXX) |
| 예약일시 | Date | 날짜와 시간 포함 |
| 지점 | Select | Ekamai, Phrom Phong |
| 공간유형 | Select | 룸, 홀 |
| 룸번호 | Select | 1번룸, 2번룸 (공간유형=룸일 때만) |
| 층 | Select | 1층, 2층 (공간유형=홀일 때만) |
| 인원 | Number | |
| 이름 | Text | |
| 전화번호 | Phone Number | |
| 이메일 | Email | 필수 항목 |
| 언어 | Select | Thai, Korean, English |
| 특별요청 | Text | Long text |
| 상태 | Select | 예약대기, 확정, 완료, 취소 |
| 리마인더발송 | Checkbox | 하루 전 리마인더 발송 여부 |
| **영수증** | **Files & media** | **입금 영수증 (Room 1: 800 THB, Room 2: 400 THB)** |
| 생성일시 | Created time | 자동 |
| 수정일시 | Last edited time | 자동 |

## 2. Views 생성

다음 뷰들을 생성하세요:

1. **📅 캘린더 뷰**: 예약일시 기준으로 달력 표시
2. **📋 전체 예약**: 테이블 뷰, 최신순 정렬
3. **📊 상태별 관리**: 보드 뷰 (상태별로 그룹화)
4. **⏰ 오늘 예약**: 필터(예약일시 = today)
5. **📬 예약대기**: 필터(상태 = 예약대기)

## 3. Integration 생성

1. Notion에서 Settings & Members → Integrations → Develop your own integrations
2. "New integration" 클릭
3. 이름: "북막골 예약 시스템"
4. Associated workspace 선택
5. Submit 후 Internal Integration Token 복사 및 저장
6. 생성된 데이터베이스에서 ... → Add connections → 방금 생성한 integration 연결

## 4. 데이터베이스 ID 확인

데이터베이스 URL에서 ID 추출:
`https://www.notion.so/your-workspace/DATABASE_ID?v=...`

DATABASE_ID 부분을 복사해서 저장하세요.

## 5. 예약금 관련 필드 설정 상세

### 예약금액 (Deposit Amount)
- **타입**: Number
- **설명**: Room 예약 시 자동으로 계산되어 저장
- **값**:
  - Room 1: 800
  - Room 2: 400  
  - Hall/Table: 0 또는 비어있음

### 예약금상태 (Deposit Status)
- **타입**: Select
- **옵션**:
  - `Unpaid` (기본값 - Room 예약 시 자동 설정)
  - `Paid` (관리자가 입금 확인 후 수동 변경)
- **색상 설정 권장**:
  - Unpaid: 🟡 Yellow
  - Paid: 🟢 Green

### 영수증 (Deposit Receipt)
- **타입**: Files & media
- **용도**: LINE에서 받은 영수증 이미지/PDF 업로드
- **장점**:
  - Notion에서 영수증 직접 확인 가능
  - LINE 메시지 찾을 필요 없음
  - 체계적 보관 및 관리
  - **입금 날짜, 시간, 금액, 입금자명 모두 영수증에 포함됨**
- **사용법**:
  - 드래그 앤 드롭으로 업로드
  - 여러 파일 업로드 가능

## 6. Views 추가 설정

기존 Views 외에 예약금 관리를 위한 View 추가:

### 6. **💰 예약금 미입금**
- **타입**: Table View
- **필터**:
  - 예약금상태 = Unpaid
  - 상태 ≠ 취소
- **정렬**: 예약일시 오름차순
- **표시 필드**: 예약번호, 예약일시, 지점, 룸번호, 이름, 전화번호, 예약금액, 예약금상태
- **용도**: 입금 대기 중인 예약 모니터링

**LINE 안내**:
- 고객이 입금 후 LINE (@853oabjm)으로 영수증 전송
- 링크: https://line.me/R/ti/p/@853oabjm (클릭 시 앱 자동 실행)

## 7. 테스트 데이터 생성 (선택사항)

다음과 같은 테스트 예약을 몇 개 생성해보세요:

**Room 예약 예시 (예약금 있음)**:
- 예약번호: BOOK-20251007-001
- 예약일시: 2025-10-08 18:00
- 지점: Ekamai
- 공간유형: 룸
- 룸번호: 1번룸
- 인원: 6
- 이름: 테스트 고객
- 전화번호: 010-1234-5678
- 이메일: test@example.com
- 언어: Korean
- 상태: 예약대기
- **예약금액: 800**
- **예약금상태: Unpaid**
- **영수증: (비어있음)**

**Hall 예약 예시 (예약금 없음)**:
- 예약번호: BOOK-20251007-002
- 예약일시: 2025-10-08 12:00
- 지점: Phrom Phong
- 공간유형: 홀
- 층: 1층
- 인원: 4
- 이름: 테스트 고객2
- 전화번호: 081-234-5678
- 이메일: test2@example.com
- 언어: Thai
- 상태: 예약대기
- **예약금액: (비어있음 또는 0)**
- **예약금상태: (비어있음)**
- **영수증: (비어있음)**

이제 Integration Token과 Database ID를 안전한 곳에 보관하고 다음 단계로 진행하세요.

