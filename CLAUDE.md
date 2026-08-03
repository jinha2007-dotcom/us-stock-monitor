# CLAUDE.md

이 파일은 Claude Code가 이 저장소에서 작업할 때 참고하는 프로젝트 가이드입니다.

## 프로젝트 개요

**미국주식 볼린저 추세 전략 — 실시간 모니터**

- 미국 주식(SPY 등)의 볼린저 밴드 + EMA 추세 전략 신호를 실시간으로 보여주는 웹앱
- 빌드 도구 없는 **단일 파일 정적 웹앱** — 모든 코드(HTML/CSS/JS)가 `index.html` 하나에 들어 있음
- 차트: [lightweight-charts 4.2.0](https://github.com/tradingview/lightweight-charts) (unpkg CDN 로드)
- 시세 데이터: Massive.com API (사용자가 브라우저에서 API 키 입력, localStorage에만 저장)
- UI 언어: 한국어

## 실행 방법

빌드/설치 과정 없음. 로컬 서버로 열면 됨:

```bash
# 방법 1: Python
python -m http.server 8000

# 방법 2: Node
npx serve .
```

이후 브라우저에서 `http://localhost:8000` 접속.
(`서버시작.bat`, `*.log` 는 로컬 전용 파일이라 .gitignore 처리됨)

## 코드 구조 (index.html 내부)

| 영역 | 내용 |
|------|------|
| `<style>` | 다크 테마 CSS. 색상은 `:root` CSS 변수로 관리 (`--bg`, `--green`, `--red` 등) |
| `<body>` 상단 | 헤더(시장상태/지연/알림 배지), API 키 입력 박스(`#keyBox`), 툴바(심볼·분봉·전략 파라미터) |
| 카드 그리드 | 현재가, 신호 상태, 밴드 상/중/하단, EMA, ATR, 손절가 |
| `#chart` | lightweight-charts 캔들 차트 |
| 하단 패널 | 신호 로그(ET 기준), 기간 시뮬레이션 테이블 |
| `<script>` | 데이터 fetch, 지표 계산(BB/EMA/ATR), 신호 판정, 렌더링 로직 |

## 전략 기본 파라미터

- 볼린저 밴드: 기간 23, 편차 2.96
- 추세 EMA: 194
- 손절: ATR × 3.19
- 기본 분봉: 30분

파라미터 기본값을 바꿀 때는 툴바 input의 `value` 속성을 수정.

## 작업 시 주의사항

- **파일을 분리하지 말 것** — 단일 index.html 구조를 유지하는 것이 이 프로젝트의 의도 (파일 하나만 옮기면 어디서든 실행됨)
- API 키를 코드에 하드코딩하지 말 것 (localStorage 방식 유지)
- UI 텍스트는 한국어 유지, 시간 표기는 미국 동부시간(ET) 기준
- 외부 의존성 추가는 CDN 방식만 사용 (npm 빌드 도입 금지)
- 커밋 메시지는 기존 스타일대로 간결한 한 줄 요약
