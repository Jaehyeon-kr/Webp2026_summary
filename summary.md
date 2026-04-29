# 웹 프로그래밍 과제 Summary

> Ctrl+F 로 파일명, 주제, 태그 검색 가능

---

## 전체 파일 현황

| 파일 | 경로 | 상태 | 주제 | 솔루션 |
|------|------|------|------|--------|
| mid.html | kimyoung/mid.html | ✅ 완성 | 과제 공지사항 HTML 구조 | 원본이 정답 |
| mid2.html | kimyoung/mid2.html | ✅ 완성 | 중첩 리스트 CSS (nth-last-of-type) | 원본이 정답 |
| mid3.html | kimyoung/mid3.html | ❌ 빈 파일 | - | - |
| mid4.html | kimyoung/mid4.html | ✅ 완성 | 테이블 CSS + rowspan/colspan | 원본이 정답 |
| mid5.html | kimyoung/mid5.html | ✅ 완성 | hover + transition + z-index | 원본이 정답 |
| exam/0.html | midterm2025제공/.../exam/0.html | ⬜ 문제 | HTML 기본 구조 작성 (CSS 없음) | → 0_sol.html |
| exam/1.html | midterm2025제공/.../exam/1.html | ⬜ 문제 | 중첩 리스트 CSS 스타일링 | → 1_sol.html |
| exam/2.html | midterm2025제공/.../exam/2.html | ⬜ 문제 | 테이블 CSS + rowspan | → 2_sol.html |
| exam/3.html | midterm2025제공/.../exam/3.html | ⬜ 문제 | 박스 겹침 + hover 이동 애니메이션 | → 3_sol.html |
| exam/4.html | midterm2025제공/.../exam/4.html | ✅ 완성 | CSS 그라디언트 배경 + 레이아웃 | 원본이 정답 |
| pre1/1.html | pre1/pre1/1.html | ✅ 완성 | 테이블 구조 (rowspan/colspan + 인라인 스타일) | 원본이 정답 |
| pre1/2.html | pre1/pre1/2.html | ⬜ 문제 | 테이블 CSS (nth-child 대각선 셀 채우기) | → 2_sol.html |
| pre1/3.html | pre1/pre1/3.html | ⬜ 문제 | 절대위치 + z-index + hover 회전 | → 3_sol.html |
| pre2/index.html | pre2/index.html | ✅ 완성 | JS 함수 연습 (수학, 문자열) | 원본이 정답 |
| pre3/pre3.html | pre3/pre3.html | ⬜ 골격 | JS DOM 쇼핑 리스트 (생성/삭제) | → pre3_sol.html |
| pre3/pre3_sol.html | pre3/pre3_sol.html | ✅ 완성 | JS DOM 쇼핑 리스트 솔루션 | 솔루션 |
| pre4/pre4.html | pre4/pre4.html | ✅ 완성 | JS DOM 조작 9문제 | 원본이 정답 |
| final/index.html | 21101929_김영환_final/index.html | ✅ 완성 | JS 고급 DOM 조작 8문제 | 원본이 정답 |
| 2024/0.html | 2024/0.html | ✅ 완성 | 시간표 rowspan/colspan | 원본이 정답 |
| 2024/1.html | 2024/1.html | ✅ 완성 | 골포스트+공 CSS 애니메이션 (rotate turn, border-radius) | 원본이 정답 |
| 2024/2.html | 2024/2.html | ✅ 완성 | qmenu 레이아웃 (relative+z-index+target) | 원본이 정답 |
| 2024/3.html | 2024/3.html | ✅ 완성 | calculateAverage 3가지 방식 (for/for...of/forEach) | 원본이 정답 |
| 2024/4.html | 2024/4.html | ✅ 완성 | 콜라츠 추측 while 루프 | 원본이 정답 |
| 2024/5.html | 2024/5.html | ✅ 완성 | 팩토리얼 누적합 (for+push) | 원본이 정답 |
| 2024/hw3.html | 2024/hw3.html | ✅ 완성 | JS quest0~9 (정규식, Math.random, dedup, 빈도수) | 원본이 정답 |

---

## 과제별 상세

### pre1 — HTML 기초 / CSS 기초

#### pre1/0.html — 과제 안내
- 제출 방법, 마감일, 이메일 제목 형식 안내

#### pre1/1.html — 테이블 구조
- `colspan`, `rowspan` 사용
- 인라인 스타일로만 스타일 적용 제약
- **핵심 태그**: table, th, td, tr, span

#### pre1/2.html — 테이블 CSS ⬜ → 2_sol.html
- 5×5 테이블, skyblue 배경, double border
- `nth-child` 선택자로 특정 셀 검은색 지정
- **핵심 CSS**: `nth-child(n)`, `double border`, `background-color`

#### pre1/3.html — 절대위치 + hover 효과 ⬜ → 3_sol.html
- 두 큰 박스 (div.left, div.right) + 각 안에 child 박스들
- z-index 계층 구조
- hover 시 z-index 최상단 이동 + child:hover 25도 회전 (2초)
- **핵심 CSS**: `position:absolute`, `z-index`, `transform:rotate`, `transition`

---

### pre3 — JS DOM 조작 (쇼핑 리스트)

#### pre3/pre3.html ⬜ 골격
- 쇼핑 리스트 추가/삭제/전체삭제 기능 골격 (미완성)
- `createElement`, `appendChild`, `removeChild`, `innerHTML = ""`
- `addEventListener("click", ...)`, 클로저로 `li` 캡처
- `input.focus()`, `autocomplete="off"`

---

### pre2 — JS 함수 기초

#### pre2/index.html ✅
| 함수 | 내용 |
|------|------|
| quest1 | 두 점 사이 거리 계산 (Math.sqrt, Math.pow) |
| quest2 | 문자열 대문자 변환 (toUpperCase) |
| quest3 | 문자열 역순 (for...of 반복) |
| quest4 | 숫자 각 자리 합계 (split + forEach) |
| quest5 | 각 단어 첫 글자 대문자화 (split + forEach) |

---

### pre4 — JS DOM 조작

#### pre4/pre4.html ✅
| sol | 내용 |
|-----|------|
| sol1 | 두 수 덧셈 → input에 결과 출력 |
| sol2 | 두 수 비교 → 더 큰 수 출력 |
| sol3 | 텍스트 입력에서 중복 없는 단어만 추출 |
| sol4 | 텍스트를 N번 반복 출력 (createElement, appendChild) |
| sol5 | 모든 input visibility 토글 (visible ↔ hidden) |
| sol6 | li 요소 색상 무지개색으로 순환 (color 배열 + % 연산) |
| sol7 | 공지사항 div 생성/삭제 토글 (insertBefore, removeChild) |
| sol8 | img 태그 생성 + 이미지 크기 읽기 |
| sol9 | 키보드 방향키로 이미지 이동 (keydown 이벤트, style.left/top) |

---

### midterm (중간고사 시험지)

#### exam/0.html ⬜ → 0_sol.html
- **문제**: CSS 없이 HTML 태그만으로 공지사항 페이지 구성
- **핵심 태그**: h1, ul, li, a, b, u, mark, hr, small, abbr

#### exam/1.html ⬜ → 1_sol.html
- **문제**: body 수정 없이 CSS style 태그만으로 중첩 리스트 스타일링
- 최상위 ul → square, ol → upper-alpha, 내부 ul → disc
- 홀수 li 빨간색: `nth-last-of-type(2n+1)`

#### exam/2.html ⬜ → 2_sol.html
- **문제**: 테이블에 CSS 추가 + rowspan 적용
- 같은 날짜 행 병합 (rowspan), zebra stripe, status 클래스 색상 지정
- **핵심 CSS**: `nth-child(odd)`, `.status-complete/accepted/not-accepted`

#### exam/3.html ⬜ → 3_sol.html
- **문제**: 글자 위에 박스 겹쳐 배치 + hover 시 박스 옆으로 이동
- `position:relative` + `position:absolute` 조합, `transition:transform`

#### exam/4.html ✅
- CSS 그라디언트 야구장 디자인 (완성된 참고 파일)
- `radial-gradient`, `box-shadow`, `inset`

---

### kimyoung (중간고사 연습 파일)

#### mid2.html ✅ — 1번 문제 솔루션
- `list-style-type: square / upper-alpha`
- `nth-last-of-type(2n+1)` → 홀수 번째 li 빨간색

#### mid4.html ✅ — 2번 문제 솔루션
- 테이블 + rowspan + `nth-of-type(2n+1)` zebra stripe
- `.status-complete`, `.status-not-accepted`, `.status-Accepted` 클래스

#### mid5.html ✅ — 3번 문제 솔루션
- `position:relative` wrapper + `position:absolute` box
- `transition: transform 0.5s` + `:hover { transform: translateX(250px) }`

---

### final (기말 과제)

#### 21101929_김영환_final/index.html ✅
| sol | 내용 |
|-----|------|
| sol1 | 텍스트 역순 변환 (for 루프) |
| sol2 | 버튼 ul DOM 위치 이동 (remove + appendChild / insertBefore) |
| sol3 | 실시간 텍스트 추적 (setInterval 1ms, mark 태그) |
| sol4 | submit 버튼 float 토글 (right ↔ none) |
| sol5 | 카운터 div 생성 + 100ms 간격 카운트업 + 3초 후 정지 |
| sol6 | range 슬라이더로 폰트 크기 10~50px 실시간 조절 |
| sol7 | #list div innerHTML 비우기 |
| sol8 | hotpink 오버레이 5초간 height 0→100% 상승 + 클릭 시 역순 |

---

### 2024 과제

#### 2024/0.html ✅ — 시간표 (Timetable)
- rowspan/colspan으로 연속 수업·다중 열 수업 병합
- `border-collapse: collapse`, `th` 배경색 gainsboro

#### 2024/1.html ✅ — 골포스트 + 공 CSS 애니메이션
- **핵심 CSS**: `border-top/left/right-style` (3면만 테두리 → 골대), `border-radius:100%` (원형)
- `transform: translateX(-100px) translateY(-250px) rotate(2turn)` → 2바퀴 회전하며 날아가기
- `transition: 2s`, `position:fixed`, `z-index`

#### 2024/2.html ✅ — qmenu 레이아웃
- `position:relative` + `z-index`로 링크가 이미지 위에 배치
- `a target="_blank"`: 새 탭으로 외부 링크 열기

#### 2024/3.html ✅ — calculateAverage 3가지 방식
- `for` (인덱스), `for...of` (요소), `forEach` (콜백) 동일 결과
- `forEach`에서 외부 변수에 누적하는 패턴

#### 2024/4.html ✅ — 콜라츠 추측 (Collatz)
- `while (num !== 1)` + 짝수/홀수 분기
- 종료 조건 미리 알 수 없을 때 while 루프 사용

#### 2024/5.html ✅ — 팩토리얼 누적합
- `last = last * i` 누적 곱 패턴 (i! 계산)
- `paclist.push(last)` 배열 누적 → 두 번째 루프에서 합산

#### 2024/hw3.html ✅ — quest0~9
| quest | 내용 |
|-------|------|
| quest0 | 초→분/초 변환 (Math.floor, %) |
| quest1+getDist | 두 점 거리 계산 (배열 파라미터, Math.sqrt) |
| quest2 | 대문자 변환 + 정규식 아포스트로피 제거 (`.replace(/'/g, "")`) |
| quest3+operate | switch 계산기 (Math.floor 정수 나눗셈) |
| quest4 | 가위바위보 (Math.random×3+1, ⚠️ 체이닝 비교 버그) |
| quest5+myReverse | 문자열 역순 (인덱스 역순 누적) |
| quest6 | 양의 홀수만 출력 while+break 패턴 |
| quest7 | 단어 이니셜 (split+" "+[0].toUpperCase) |
| quest8 | 중복 없는 단어 정렬 (nested for dedup + array.sort) |
| quest9 | 문자 빈도수 (object{} 카운터 + for...in) |

---

## 파일 상태 요약

- ✅ 완성 (솔루션 있음): 17개
- ⬜ 문제/골격 파일 → 솔루션 생성됨: 5개 (0_sol ~ 3_sol, 2_sol, 3_sol) + pre3 미완성 골격
- ❌ 빈 파일: 1개 (mid3.html)
