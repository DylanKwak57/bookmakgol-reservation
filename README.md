# 북막골 예약 시스템 (Bookmakgol Reservation System)

태국 전통 한식당 북막골의 온라인 예약 시스템입니다. 3개 언어(한국어/태국어/영어)를 지원하며, 실시간 예약 관리와 자동 이메일 알림 기능을 제공합니다.

## 🎯 주요 기능

- **다국어 지원**: 한국어, 태국어, 영어 실시간 전환
- **실시간 예약**: 중복 예약 방지 및 즉시 처리
- **자동 알림**: 예약 확정 및 리마인더 이메일 자동 발송
- **모바일 최적화**: 라인 앱 내 브라우저 완벽 지원
- **관리자 대시보드**: Notion 기반 예약 관리 시스템

## 🏪 지점 정보

### 에까마이 지점
- **주소**: 에카마이 BTS 4번 출구, 수쿰윗 병원 맞은편
- **전화**: 095-868-6826
- **룸**: 1번룸(최대 16명), 2번룸(최대 6명)
- **홀**: 1층 8테이블, 2층 7테이블

### 프롬퐁 지점
- **주소**: 수쿰윗 소이 24, 아리스톤 호텔 1층
- **전화**: 02-115-5500
- **룸**: 1번룸(최대 16명), 2번룸(최대 4명)
- **홀**: 1층 7테이블, 2층 8테이블

**영업시간**: 11:00-15:00, 16:00-22:00 (Break: 15:00-16:00)

## 🛠 기술 스택

- **프론트엔드**: HTML5, CSS3, JavaScript (Vanilla)
- **백엔드**: n8n 워크플로우 자동화
- **데이터베이스**: Notion Database
- **이메일**: Gmail API
- **배포**: GitHub Pages
- **연동**: LINE Official Account

## 📁 프로젝트 구조

```
bookmakgol-reservation/
├── index.html                           # 메인 예약 폼
├── location.html                        # 길찾기 페이지
├── README.md                           # 프로젝트 문서
├── notion-database-setup.md            # Notion 설정 가이드
├── integration-test-guide.md           # 통합 테스트 가이드
├── deployment-guide.md                 # 배포 가이드
├── workflow-1-reservation-intake.json  # 예약 접수 워크플로우
├── workflow-2-confirmation-email.json  # 확정 이메일 워크플로우
└── workflow-3-reminder-system.json     # 리마인더 워크플로우
```

## 🚀 설치 및 배포

### 1. Notion 데이터베이스 설정
```bash
# notion-database-setup.md 참고
1. Notion에서 데이터베이스 생성
2. Properties 설정 (16개 필드)
3. Views 생성 (5개 뷰)
4. Integration API 키 발급
```

### 2. n8n 워크플로우 배포
```bash
# 3개 워크플로우 JSON 파일을 n8n에 import
1. workflow-1-reservation-intake.json
2. workflow-2-confirmation-email.json  
3. workflow-3-reminder-system.json

# 환경 변수 설정
YOUR_NOTION_DATABASE_ID=실제_데이터베이스_ID
RESTAURANT_ADMIN_EMAIL=관리자_이메일
```

### 3. GitHub Pages 배포
```bash
# Repository 생성 후 파일 업로드
git clone https://github.com/username/bookmakgol-reservation.git
cd bookmakgol-reservation
git add .
git commit -m "Initial deployment"
git push origin main

# GitHub Pages 활성화
# Settings > Pages > Deploy from branch: main
```

### 4. 프론트엔드 설정
```javascript
// index.html에서 Webhook URL 설정
const response = await fetch('https://your-n8n-instance.com/webhook/bookmakgol-reservation', {
```

## 📱 사용 방법

### 고객 예약 프로세스
1. **언어 선택**: 한국어/태국어/영어 중 선택
2. **지점 선택**: 에까마이 또는 프롬퐁
3. **날짜/시간**: 영업시간 내 30분 단위 선택
4. **공간 선택**: 룸(개별공간) 또는 홀(일반테이블)
5. **연락처 입력**: 이름, 전화번호, 이메일
6. **예약 완료**: 예약번호 발급 및 대기 상태

### 관리자 예약 관리
1. **알림 확인**: 새 예약 시 이메일 알림 수신
2. **Notion 확인**: 예약 세부사항 검토
3. **상태 변경**: "예약대기" → "확정" 변경
4. **자동 발송**: 고객에게 확정 이메일 자동 발송
5. **리마인더**: 하루 전 자동 리마인더 발송

## 🧪 테스트

### 통합 테스트 실행
```bash
# integration-test-guide.md 참고
1. 3개 언어별 예약 테스트
2. 중복 예약 방지 테스트
3. 이메일 발송 테스트
4. 모바일 반응형 테스트
5. 리마인더 시스템 테스트
```

### 테스트 시나리오
- ✅ 한국어 룸 예약 (정상 플로우)
- ✅ 태국어 홀 예약
- ✅ 영어 중복 예약 (오류 테스트)
- ✅ 예약 확정 이메일 발송
- ✅ 리마인더 자동 발송

## 📊 시스템 아키텍처

```
손님 웹 예약 (index.html)
    ↓
n8n Webhook (중복 체크)
    ↓
Notion Database (저장)
    ↓
식당 이메일 알림 (예약대기)
    ↓
관리자 Notion에서 확정
    ↓
Notion Webhook 트리거
    ↓
n8n 워크플로우 (언어별 템플릿)
    ↓
손님 이메일 발송 (확정 알림)
    ↓
n8n 스케줄러 (매일 오전 9시)
    ↓
내일 예약 조회 → 리마인더 발송
```

## 🔒 보안 및 개인정보

- **HTTPS 통신**: 모든 데이터 암호화 전송
- **최소 정보 수집**: 예약에 필요한 정보만 수집
- **자동 삭제**: 완료된 예약 데이터 정기 정리
- **접근 권한**: 관리자만 Notion 데이터베이스 접근

## 📈 성능 지표

- **응답 시간**: 예약 처리 5초 이내
- **가용성**: 99.9% 업타임 목표
- **동시 접속**: 최대 100명 동시 예약 지원
- **모바일 최적화**: 모든 기기에서 완벽 작동

## 🛠 유지보수

### 정기 점검 (주간)
- [ ] 예약 데이터 정확성 확인
- [ ] 이메일 발송 상태 확인
- [ ] 웹사이트 접속 상태 확인

### 월간 관리
- [ ] Notion 데이터베이스 정리
- [ ] 완료된 예약 아카이빙
- [ ] 시스템 성능 검토

## 🆘 문제 해결

### 자주 묻는 질문

**Q: 예약이 안 들어가요**
A: 영업시간(11:00-15:00, 16:00-22:00) 내 시간을 선택했는지 확인하세요.

**Q: 확정 이메일을 못 받았어요**
A: 스팸 폴더를 확인하고, 이메일 주소가 정확한지 확인하세요.

**Q: 중복 예약이 들어갔어요**
A: 룸 예약만 중복 체크되며, 홀 테이블은 선착순입니다.

### 긴급 연락처
- **시스템 오류**: [개발자 연락처]
- **예약 문의**: 095-868-6826 (에까마이) / 02-115-5500 (프롬퐁)

## 👥 기여자

- **개발자**: Dylan Kwak (@dylankwak57)
- **기획**: 북막골 운영팀
- **디자인**: 북막골 브랜드 가이드라인

## 📄 라이선스

이 프로젝트는 북막골 전용으로 개발되었습니다.

## 📞 연락처

- **GitHub**: [@dylankwak57](https://github.com/dylankwak57)
- **이메일**: [개발자 이메일]
- **북막골 공식**: [공식 연락처]

---

**마지막 업데이트**: 2025-10-06  
**버전**: 1.0.0  
**상태**: 프로덕션 준비 완료

