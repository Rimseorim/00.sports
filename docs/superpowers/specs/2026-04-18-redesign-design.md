# 운동일기 리디자인 스펙

## 개요

기존 운동일기 웹앱(`index.html`)의 CSS를 전면 교체해 20대 중반 여성 타깃의 어시 웰니스 스타일로 리디자인한다. HTML 구조와 JS 기능은 그대로 유지하고, CSS만 교체하는 방식으로 진행한다. 이번달 통계 카드를 신규 추가한다.

---

## 컬러 시스템

| 역할 | 컬러 | 용도 |
|------|------|------|
| 배경 | `#faf6f2` | body, 카드 배경 |
| 페이지 배경 | `#ede8e3` | 전체 배경 |
| 주 텍스트 | `#2c1f14` | 제목, 본문 |
| 보조 텍스트 | `#b08060` | 날짜, 메타 |
| 포인트 브라운 | `#7c5c3e` | 헤더, 주요 버튼, 오늘 날짜, 통계 카드 배경 |
| 테라코타 | `#c8956c` | 러닝 뱃지/점/카드 왼쪽 라인, 탭 활성 밑줄 |
| 크로스핏 레드 | `#d0604a` | 크로스핏 뱃지/점/카드 왼쪽 라인 |
| 카드 테두리 | `#ecddd3` | 모든 카드 border |

---

## 타이포그래피

- 폰트: 기존 유지 (`Apple SD Gothic Neo`, `Malgun Gothic`)
- 타이틀 (`h1`): `font-size: 22px`, `font-weight: 800`, `letter-spacing: -0.5px`
- 섹션 제목: `font-size: 14–16px`, `font-weight: 800`
- 본문: `font-size: 13–14px`, `font-weight: 400`
- 뱃지/라벨: `font-size: 10–11px`, `font-weight: 700`

---

## 컴포넌트 변경 사항

### 헤더
- 배경: `#faf6f2` (기존 흰색 유지)
- 하단 border: `#ecddd3`
- 탭 활성 밑줄: `#c8956c` (기존 `#222` → 테라코타)
- 탭 비활성 색: `#c4a48a`

### 통계 카드 (신규 추가)
- 달력 위에 삽입
- 배경: `#7c5c3e` (딥 브라운), 흰 텍스트
- 3개 항목: 이번달 운동 횟수 / 총 러닝 거리(km) / 크로스핏 횟수
- border-radius: `18px`
- 데이터는 `getLogs()`에서 현재 월 기준으로 실시간 계산

### 달력
- 전체 배경: `#fff`, border: `1px solid #ecddd3`, border-radius: `18px`
- 오늘 날짜: `background: #7c5c3e`, color: `#fff`, border-radius: `10px` (기존 원형 → 사각형)
- 기록 있는 날: 러닝 `#f0e6dc`, 크로스핏 `#fce8e0`
- 점(dot): 러닝 `#c8956c`, 크로스핏 `#d0604a`
- 요일 헤더: `#c4a48a`, 일요일 `#e07050`, 토요일 `#7090d0`
- 이전/다음 버튼: `background: #f5ede3`, `border-radius: 8px`
- 범례 점: 원형(5px) → 사각형(8px, border-radius 3px)

### 기록 카드 (log-item)
- 배경: `#fff`, border: `1px solid #ecddd3`, border-radius: `16px`
- 왼쪽 컬러 라인 추가: 러닝 `border-left: 3px solid #c8956c`, 크로스핏 `border-left: 3px solid #d0604a`
- 뱃지: 러닝 `background: #f5ede3, color: #7c5c3e` / 크로스핏 `background: #fce8e0, color: #b04030`
- 뱃지 border-radius: `6px` (기존 `20px` 원형 → 각진 형태)
- 일기 구분선: `#f0e6dc`

### 버튼
- `+ 기록 추가` (add-btn): `background: #7c5c3e`, `border-radius: 10px`
- `무게 추이` (outline-btn): `border: 1.5px solid #c8956c`, `color: #7c5c3e`, `border-radius: 10px`
- `저장하기` 러닝: `background: #c8956c`
- `저장하기` 크로스핏: `background: #d0604a`
- 모달 닫기/삭제 등 보조 버튼: 호버 색 `#fce8e0`

### 모달
- 배경 오버레이: `rgba(44, 31, 20, 0.5)` (기존 검정 → 브라운 계열)
- 모달 박스: `background: #faf6f2`, `border-radius: 20px`
- input/select/textarea: `border: 1.5px solid #ecddd3`, focus `border-color: #c8956c`
- label: `color: #7c5c3e`

### 백업 바 (기존)
- 버튼: `background: #fff`, `border: 1px solid #ecddd3`, `color: #7c5c3e`

---

## 신규 기능: 통계 카드

### 위치
달력 카드 바로 위 (`.calendar-card` 앞에 삽입)

### HTML 구조
```html
<div class="stats-card" id="stats-card"></div>
```

### JS 로직 (renderStats 함수 신규 추가)
- `getLogs()`로 전체 로그 조회
- 현재 표시 중인 월(`viewYear`, `viewMonth`) 기준 필터
- 러닝 로그: `distance` 합산 (km, 소수점 1자리)
- 크로스핏 로그: 횟수
- 총 운동 횟수 = 러닝 + 크로스핏
- `renderCalendar()` 호출 시 함께 갱신

---

## 구현 범위

- **변경**: `index.html` 내 `<style>` 블록 전면 교체
- **추가**: 통계 카드 HTML + `renderStats()` JS 함수
- **유지**: 모든 기존 JS 로직, HTML 구조, 백업/복원 기능
