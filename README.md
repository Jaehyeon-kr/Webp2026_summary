# Webp2026_summary

웹 프로그래밍 과제 정리 뷰어 — HTML/CSS, JavaScript, 패턴, 에러 참고자료를 버튼 한 번으로 검색

## 바로 보기
👉 https://Jaehyeon-kr.github.io/Webp2026_summary/

---

## 실행 방법

### 1. VS Code Live Server (권장)

1. VS Code에서 이 폴더 열기
2. 확장 탭(`Ctrl+Shift+X`)에서 **Live Server** 검색 후 설치
3. `index.html` 우클릭 → **Open with Live Server**
4. 브라우저에서 자동으로 열림

> `viewer.html`을 직접 열면 동작하지 않습니다. 반드시 `index.html`을 여세요.

### 2. 기타 로컬 서버

```bash
# Python
python -m http.server 5500

# Node.js
npx serve .
```

브라우저에서 `http://localhost:5500` 접속

---

## 파일 구조

```
├── index.html       # 메인 뷰어 (사이드바 + iframe)
├── viewer.html      # md 렌더링 + 섹션 점프 (index에서 사용)
├── html.md          # HTML 태그 / CSS 속성 정리
├── js.md            # JavaScript 정리
├── pattern.md       # 자주 나오는 패턴 20개
├── error.md         # 주의해야 할 에러 25개
├── summary.md       # 전체 파일 현황 요약
└── pre3_sol.html    # 쇼핑 리스트 DOM 솔루션 (뷰어에서 직접 실행)
```

---

## 기능

| 기능 | 설명 |
|------|------|
| 탭 전환 | HTML/CSS · JS · 패턴 · 에러 4개 탭 |
| 버튼 클릭 | 해당 섹션으로 즉시 이동 |
| 섹션 강조 | 이동된 헤딩 3초간 노란 테두리 강조 |
| 검색 필터 | 사이드바 검색창으로 버튼 실시간 필터 |
| 코드 하이라이팅 | JS / CSS / HTML 코드블록 자동 색상 |
| 솔루션 직접 실행 | pre3 쇼핑 리스트를 iframe에서 바로 실행 |

---

## 의존성 (CDN, 인터넷 연결 필요)

| 라이브러리 | 용도 |
|-----------|------|
| [marked.js](https://github.com/markedjs/marked) | 마크다운 → HTML 파싱 |
| [highlight.js](https://highlightjs.org/) | 코드블록 색상 |
