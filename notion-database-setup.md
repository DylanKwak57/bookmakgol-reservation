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

## 5. 테스트 데이터 생성 (선택사항)

다음과 같은 테스트 예약을 몇 개 생성해보세요:

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

이제 Integration Token과 Database ID를 안전한 곳에 보관하고 다음 단계로 진행하세요.

