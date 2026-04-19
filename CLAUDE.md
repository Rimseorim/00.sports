# sports — 운동 일기

개인용 러닝 + 크로스핏 기록 웹앱. 단일 `index.html`, 백엔드 없음, 브라우저 localStorage 로만 저장.

## 역할
- 러닝 / 크로스핏 운동 일기
- 월간 통계 + 달력
- PR / 1RM 관리 및 무게 추이 차트
- JSON 백업 / 복원

## 기술 스택
- HTML + CSS + JS 바닐라 단일 파일 (`index.html`)
- 외부 의존성: Google Fonts CDN (Roboto + Noto Sans KR) 만
- 저장소: localStorage (`sportslogs`, `prdata`)
- 서버: 없음. 파일 그대로 열거나 정적 호스팅

## 폴더 구조
```
sports/
├── index.html      -- 본체 (단일 파일 원칙)
├── favicon.svg     -- 파비콘
├── docs/           -- 기획 / 설계 문서
├── .claude/        -- Claude Code 설정
└── .superpowers/   -- brainstorm 산출물 (런타임 state는 .gitignore)
```

## 규칙
- 단일 `index.html` 원칙 유지. 외부 JS/CSS 파일 분리 금지.
- 이모지 사용 금지.
- 폰트: Roboto + Noto Sans KR, 굵기 400 / 700 만.
- 백엔드 추가 금지. localStorage 기반.
- 모든 `innerHTML` 사용 구간은 `escapeHtml()` 로 사용자 입력 이스케이프 필수.

## 로컬 실행
```bash
# 방법 1: 브라우저로 직접 열기
start index.html

# 방법 2: 간이 서버
python -m http.server 8000
```

## 데이터 스키마
- localStorage key `sportslogs`: `Array<Log>`
  - Running: `{id, type:'running', date, distance, time, place, diary}`
  - CrossFit: `{id, type:'crossfit', date, title, wods:[{content, record, weights:[{movement, weight, unit}]}], diary}`
- localStorage key `prdata`: `{movements:[{id, name, records:[{id, date, weight, unit, type, note}]}]}`
- 백업 JSON: `{version, sportslogs, prdata, exportedAt}`

## 배포
- GitHub Pages 또는 정적 파일 직접 전달. Railway 미사용.
