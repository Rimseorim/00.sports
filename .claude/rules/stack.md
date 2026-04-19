# STACK — sports

## 서비스 식별
프로젝트: sports -- 개인용 운동 일기 (러닝 + 크로스핏)
GitHub: Rimseorim/00.sports
프로덕션: 정적 파일 (GitHub Pages 또는 로컬)
로컬: file:///.../index.html 또는 localhost:8000 (python -m http.server)
프로덕션 브랜치: master

---

## 알려진 지뢰
| 증상 | 원인 | 확인할 곳 |
|------|------|----------|
| 복원 후 PR 뷰 화면 안 바뀜 | restoreBackup()에서 renderPRList() 호출했으나 존재하는 함수는 renderPRView() | index.html restoreBackup |
| 일기 본문 `<script>` 삽입 가능 (XSS) | renderLogs가 textContent 대신 innerHTML 사용 | index.html renderLogs |
| localStorage 한도 초과 시 저장 실패 조용함 | 브라우저 5~10MB 한도. try/catch 없음 | index.html save |
| 데이터 전손실 | 브라우저 청소 / 기기 변경 시. 자동 백업만 sessionStorage 복사 | index.html save |

---

## 환경변수
없음 (정적 파일)

---

## DB
localStorage 만 사용.
- `sportslogs`: 운동 기록 배열
- `prdata`: PR / 1RM 데이터
- `sportslogs_prev`: sessionStorage 자동 백업 (save 직전 스냅샷)
- `lastBackupAt`: localStorage, 마지막 수동 백업 일자

---

## 외부 연동
| 서비스 | 용도 | 엔드포인트 | 장애 시 영향 |
|--------|------|-----------|-------------|
| Google Fonts | Roboto + Noto Sans KR | fonts.googleapis.com | 시스템 폰트로 폴백 |

---

## 서버 구성
프레임워크: 없음
엔트리포인트: index.html
정적 파일: favicon.svg
템플릿: 없음
포트: 정적 호스팅 시에만

---

## 인증 / 세션
없음 (개인 로컬 저장)

---

## 리소스 / 제한
localStorage: ~5MB (브라우저별 상이)

---

## 로컬 실행
브라우저 더블클릭 또는 `python -m http.server 8000`

---

## 핵심 함수 맵
| 함수 | 위치 | 책임 |
|------|------|------|
| `escapeHtml` | index.html 스크립트 상단 | XSS 방어 |
| `getLogs / save / deleteLog` | 운동 기록 CRUD | localStorage 쓰기 시 자동백업 |
| `renderCalendar / renderStats` | 달력 + 통계 | |
| `renderLogs` | 기록 목록 (render) | |
| `renderPRView` | PR 탭 전체 | |
| `exportBackup / restoreBackup` | JSON 파일 백업 복원 | 버전필드 검증 |
| `parseWeightsFromText` | 자유 텍스트에서 무게 감지 | |
