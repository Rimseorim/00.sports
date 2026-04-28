# HANDOFF - 2026-04-29 01:57

## 완료

- [x] 디자인 토큰화 (`:root` 18 변수, 컬러·spacing·radius)
- [x] 명언 XSS 보강 (`textContent` + DOM API)
- [x] Streak → 폐지 (사용자 요청)
- [x] 인바디형 트렌드 5종 SVG 꺾은선 + 점선 목표선
- [x] 5종 목표 모달 (주간 운동·월간 km·월간 cf·대표 1RM·주간 페이스) + % 달성률 pill
- [x] 5 페르소나(린아·준호·혜진·태현·김부장) 121건 피드백 → 30+건 반영
- [x] 시간 mm:ss 분리 + 페이스 자동 계산
- [x] inputmode·viewport-fit·safe-area·focus-visible
- [x] 영어 약어 한국어 보강 (PR→최고 기록, REST→휴식, Rx 풀이)
- [x] alert 5곳 → 인라인 폼 에러 (`.form-error`)
- [x] 백업 복원 confirm 역설 → 커스텀 모달 분기
- [x] 직전 기록 복제 (`cloneLog`)
- [x] 1RM % 계산기 토글 (Epley 공식)
- [x] 전체 기록 탭 + 검색·필터 (현재는 PR 화면 우선이라 사이드 액션에서 빠짐)
- [x] CSV 내보내기 (BOM, 7컬럼)
- [x] 모달 role=dialog + aria-modal + focus trap
- [x] 캘린더 cal-day → role=button + tabindex + Enter/Space
- [x] 명명 WOD 9종 벤치마크 (Fran/Helen/Cindy/Grace/Murph/Diane/Angie/Isabel/Karen)
- [x] WOD record type select + AMRAP/EMOM/For Time 템플릿
- [x] 동작명 200 프리셋 datalist (영문 + 한글 mix)
- [x] DOTS 점수 (M_COEFS / F_COEFS 4차 다항식)
- [x] 30일+ 백업 안 함 알림 → 사이드바 좌하단 컴팩트 위치
- [x] 메인 상단 탑바 제거 → 사이드바 사용자 칩·액션·로그아웃 통합
- [x] 사이드바 타이틀 중앙정렬 카드형 ("운동 일기 / 오늘도 한 줄 / 대시보드 보기 ›")
- [x] view-dashboard 1550px 강제
- [x] 월별 추이 통합 SVG (3 시리즈 한 차트, 정규화 비교)
- [x] 가상 데이터 시드 함수 (빠른 선택 user1/user2/user3 자동 시드)
- [x] 로그인 풀페이지 (currentUser 없으면 메인 가림)
- [x] localStorage namespace (5 키 자동 prefix `key:userN`)
- [x] 사용자별 데이터 완전 격리 (검증: user1 96건 vs user2 24건 vs user3 148건)
- [x] 사이드바 스크롤 절대 차단 (모든 영역 컴팩트화, daylist 폐지)
- [x] 러닝/크로스핏 좌우 2열 분할 (좌:폼 / 우:최근 표 row 12건) + 좌우 폭/시작 y 정확 대칭
- [x] 사이드바 액션 4→3 (러닝쓰기·크로스핏쓰기·기록적기), 단색 통일, 세로 1열
- [x] PR 화면 재디자인 (헤더·미니차트·날짜·diff·메모 위계 정리)

## 진행중

- 시각 디테일 마이크로 폴리시 — `index.html` 단일 파일 (3900줄+)

## 대기 (다음 라운드 후보 — 큰 외부 연동 또는 신규 기능)

- [ ] Garmin GPX 임포트 / Strava OAuth (외부 의존, 보존선 위반)
- [ ] Sinclair·Wilks 보정 점수 (DOTS는 적용됨)
- [ ] 인스타 공유용 Canvas PNG 카드
- [ ] 동작 패턴 분류 (Hinge/Squat/Push/Pull) + 주간 분포
- [ ] 에너지 시스템 태그 (Phosphagen/Glycolytic/Oxidative)
- [ ] 종목 변종 카테고리 필드 (Snatch / Power / Squat / Hang)
- [ ] 심박·VO2max·케이던스·고도 필드
- [ ] PR 카드 그리드가 좁은 화면에서 1열만 보임 (auto-fill minmax 330 → 카드 컨텐츠 폭 영향)

## 결정사항 / 주의

- **보존선** (절대 변경 금지): 단일 `index.html` / localStorage / 이모지 금지 / 그라디언트 금지 / Roboto+Noto Sans KR / "오늘도 수고했어요" 따뜻한 톤
- **사용자 격리**: localStorage monkey-patch (`window.__rawLS`로 raw 접근 노출), 5 키 `sportslogs/prdata/restPassState/lastBackupAt/profileSettings`만 namespace
- **KST 강제**: `Asia/Seoul` 타임존, todayStr·시계 모두 KST 기반
- **데모 시드**: 빠른 선택 user1/2/3만, 직접 입력은 시드 X
- **로그인 페이지 주소**: `http://localhost:8765/index.html` (currentUser 없을 때 자동 풀페이지)
- **로그아웃**: 사이드바 좌하단 row의 빨간 톤 버튼
- **레이아웃**: 사이드바 320px / 메인 가변, view-dashboard만 1550px 강제
- **트렌드 카드 4번**: 평균 1RM 폐기 → 대표 종목(가장 최근 갱신) 1RM 추이 (P2·P4 합의)

## 핵심 커밋 (최신 → 과거)

```
c5d0d0e feat: 기록 적기 (PR) 화면 재디자인 — 글자/내용/날짜 위계 정리
c639491 feat: 러닝/크로스핏 좌우 정렬·폭 정확히 대칭
a58ae47 feat: 사이드바 스크롤 절대 차단 — 모든 이격·padding 초컴팩트화
f1942b3 feat: 대시보드 컴팩트 + 좌우 2열 분할 + 표 형식 row + 단색 통일
92c5498 feat: 백업 알림 사이드바 하단 이동 + Streak 카드 삭제
74641ef feat: 메인 탑바 제거 + 사이드바 4 패널 + 최근 기록 → 월별 추이 꺾은선
ca71c6c feat: 사이드바 타이틀 중앙정렬·대시보드 카드 + view-dashboard 1550px + 월별 추이 통합 차트
62b481b feat: 트렌드 row 형식 + 페이지 스크롤 제거 + 명언 사이드바 하단 이동
5cfad62 feat: 사이드바 컴팩트 + KST 시계 + 5종 목표·달성률·차트 점선 목표선
4ee0b4e feat: 로그인 풀페이지화 — 메인 UI 완전 가림
032332b feat: 로그인 화면 + 사용자별 데이터 격리 (내부 테스트용)
4f3b5ae feat: 라운드 4 — 11개 추가 반영 (메타데이터·벤치마크·접근성·DOTS)
e6f00f1 feat: 미반영 핵심 11개 일괄 반영 (라운드 3)
dcf11fc feat: 5 페르소나 121건 피드백 우선순위 18건 반영
23fb8a2 feat: 디자인 토큰화 + Streak + 인바디형 트렌드 대시보드 + 빈상태 CTA + XSS 보강
```

## 다음 세션 권장 첫 프롬프트

`/resume`
