# HTML 태그 & CSS 기능 정리

> Ctrl+F 로 태그명, 속성명, CSS 속성 검색

---

## HTML 태그

### 문서 구조

| 태그 | 설명 | 사용 파일 |
|------|------|-----------|
| `<!DOCTYPE html>` | HTML5 문서 선언 | 모든 파일 |
| `<html lang="ko">` | 최상위 요소, 언어 설정 | 모든 파일 |
| `<head>` | 메타데이터 컨테이너 | 모든 파일 |
| `<meta charset="UTF-8">` | 문자 인코딩 설정 | 모든 파일 |
| `<meta name="viewport">` | 반응형 뷰포트 설정 | kimyoung/mid*.html |
| `<title>` | 브라우저 탭 제목 | 대부분 파일 |
| `<body>` | 화면에 표시되는 내용 | 모든 파일 |
| `<link rel="stylesheet">` | 외부 CSS 파일 연결 | pre4.html, final/index.html |
| `<style>` | 내부 CSS 정의 | 대부분 파일 |
| `<script>` | JavaScript 코드 삽입 | pre2, pre4, final |

---

### 텍스트 / 인라인 요소

| 태그 | 설명 | 사용 파일 |
|------|------|-----------|
| `<h1>` ~ `<h3>` | 제목 (크기순) | mid.html, 0_sol.html |
| `<p>` | 문단 | mid.html, exam/3.html |
| `<b>` | 굵은 텍스트 (의미 없음) | mid.html |
| `<strong>` | 중요 텍스트 (굵게) | pre4/sol7 |
| `<u>` | 밑줄 | 0_sol.html |
| `<span>` | 인라인 그룹화 | pre1/1.html, mid.html |
| `<mark>` | 형광펜 하이라이트 | mid.html, final/sol3 |
| `<small>` | 작은 텍스트 | 0_sol.html |
| `<abbr title="...">` | 약어 (툴팁) | 0_sol.html |
| `<q>` | 인라인 인용문 | 0_sol.html |
| `<br>` | 줄바꿈 | mid.html |
| `<hr>` | 수평선 구분선 | mid.html |

---

### 목록

| 태그 | 설명 | 속성 | 사용 파일 |
|------|------|------|-----------|
| `<ul>` | 순서 없는 목록 (•) | - | mid.html, exam/1.html, mid2.html |
| `<ol>` | 순서 있는 목록 (1, 2...) | - | exam/1.html, mid2.html |
| `<li>` | 목록 항목 | `onclick` | pre4.html, final/index.html |

#### CSS list-style-type 값
```
square       → ■ 사각형 불릿
disc         → • 원형 불릿 (기본)
circle       → ○ 빈 원
upper-alpha  → A, B, C...
lower-alpha  → a, b, c...
decimal      → 1, 2, 3... (기본 ol)
none         → 불릿 없음
```
- 사용 파일: [mid2.html](kimyoung/mid2.html), [1_sol.html](midterm2025제공/midterm2025제공/exam/1_sol.html)

---

### 링크 / 미디어

| 태그 | 설명 | 주요 속성 | 사용 파일 |
|------|------|-----------|-----------|
| `<a>` | 하이퍼링크 | `href`, `title` | mid.html, exam/2.html |
| `<img>` | 이미지 삽입 | `src`, `width` | pre4/sol8, pre4/sol9, exam/4.html |

```html
<!-- 이메일 링크 -->
<a href="mailto:example@email.com">이메일 주소</a>

<!-- 앵커 (페이지 내 이동) -->
<a href="#">더미 링크</a>
```

---

### 테이블

| 태그 | 설명 | 사용 파일 |
|------|------|-----------|
| `<table>` | 테이블 컨테이너 | pre1/1,2.html, exam/2.html, mid4.html |
| `<thead>` | 테이블 헤더 그룹 | exam/2_sol.html, mid4.html |
| `<tbody>` | 테이블 본문 그룹 | exam/2_sol.html, mid4.html |
| `<tr>` | 테이블 행 | 모든 테이블 파일 |
| `<th>` | 헤더 셀 (굵게, 가운데 정렬) | pre1/1.html, exam/2.html |
| `<td>` | 데이터 셀 | 모든 테이블 파일 |

#### rowspan / colspan
```html
<!-- 여러 행 병합 -->
<td rowspan="2">Apr 11, 2025</td>

<!-- 여러 열 병합 -->
<th colspan="2">서울특별시 노원구...</th>
<td colspan="7" style="text-align:center">Summary</td>
```
- 사용 파일: [pre1/1.html](pre1/pre1/1.html), [mid4.html](kimyoung/mid4.html), [2_sol.html](midterm2025제공/midterm2025제공/exam/2_sol.html)

---

### 폼 (Form)

#### form 컨테이너
```html
<form name="폼이름" action="처리URL" method="get|post" target="_blank|_self">
  ...
</form>
```

| 속성 | 설명 |
|------|------|
| `name` | 폼 이름 (JS에서 접근 시 사용) |
| `action` | 폼 데이터를 전송할 URL (서버 프로그램 경로) |
| `method` | 전송 방식: `get`(URL에 데이터 포함, 보안 낮음) / `post`(body에 포함, 보안 높음) |
| `target` | 응답을 표시할 창: `_blank`(새 창), `_self`(현재 창, 기본값) |

**GET vs POST**
- GET: URL에 `?name=value&name2=value2` 형태로 붙음, 주소창에 노출, 길이 제한 있음
- POST: HTTP body에 숨겨서 전송, 주소창에 미노출, 길이 제한 없음

#### fieldset / legend
```html
<fieldset>
  <legend>인적사항</legend>
  <!-- 관련 입력 요소들 -->
</fieldset>
```
- `<fieldset>`: 관련 입력 요소를 묶는 테두리 박스
- `<legend>`: fieldset의 제목 (테두리 위에 표시)

#### label
```html
<!-- 방법 1: for + id 연결 -->
<label for="sName">성명</label>
<input type="text" id="sName">

<!-- 방법 2: label로 감싸기 -->
<label>성명 <input type="text"></label>
```
- `for` 속성값과 input의 `id` 속성값이 일치해야 연결됨
- label 클릭 시 연결된 input에 포커스

---

### input 태그

```html
<input type="입력형식" name="이름" [속성=속성값]...>
```

#### input type — 글자 관련

| type | 설명 | 결과 |
|------|------|------|
| `text` | 일반 텍스트 입력 | 텍스트 박스 |
| `password` | 비밀번호 입력 | 입력 내용이 `*`/`•`로 표시 |
| `search` | 검색어 입력 | 텍스트 박스 (X 버튼 있음) |
| `url` | URL 입력 | 형식 체크 (http:// 형식) |
| `email` | 이메일 입력 | 형식 체크 (`@` 포함 여부) |
| `tel` | 전화번호 입력 | 텍스트 박스 (모바일에서 숫자 키패드) |

```html
<fieldset>
  <legend>인적사항</legend>
  <label for="sName">성명</label>
  <input type="text" name="stuName" id="sName" autofocus required>
  <label for="sFirst">첫사랑</label>
  <input type="password" name="stuFirst" id="sFirst">
  <label for="sHome">홈페이지</label>
  <input type="url" name="stuHome" id="sHome" value="http://">
  <label for="sMail">이메일</label>
  <input type="email" name="stuMail" id="sMail" placeholder="x@y.z">
  <label for="sTel">전화번호</label>
  <input type="tel" name="stuNTel" id="sTel" autocomplete="on">
</fieldset>
```

#### input type — 숫자 관련

| type | 설명 | 결과 |
|------|------|------|
| `number` | 숫자 입력 | 스핀 박스 (위아래 화살표) |
| `range` | 슬라이더로 숫자 입력 | 슬라이드 바 |

```html
<label for="sGrade">학년</label>
<input type="number" name="stuGrade" id="sGrade">

<label for="sGPA">성적 평점</label>
0 <input type="range" name="stuGPA" id="sGPA" min="0" max="4.5" step="0.5"> 4.5
```

#### input type — 선택 관련

| type | 설명 | 특징 |
|------|------|------|
| `radio` | 단일 선택 (라디오 버튼) | 같은 `name`끼리 묶임, 하나만 선택 가능 |
| `checkbox` | 다중 선택 (체크박스) | 같은 `name`끼리 묶임, 여러 개 선택 가능 |

```html
<!-- radio: name 동일 → 한 개만 선택 -->
<label class="inline"><input type="radio" name="stuLang" value="C">C</label>
<label class="inline"><input type="radio" name="stuLang" value="Java">Java</label>

<!-- checkbox: name 동일 → 여러 개 선택 가능 -->
<label class="inline"><input type="checkbox" name="stuJob" value="web">웹</label>
<label class="inline"><input type="checkbox" name="stuJob" value="mobile">모바일</label>
```
- 폼 전송 시 `value` 속성의 값이 서버로 전달됨

#### datalist (드롭다운 후보 목록)
```html
<input type="text" name="stuLocation" id="sLocation" list="loclist">
<datalist id="loclist">
  <option value="서울">
  <option value="경기">
  <option value="강원">
</datalist>
```
- `<input>`의 `list` 속성값 = `<datalist>`의 `id` 속성값으로 연결

#### input type — 날짜/시간 관련

| type | 설명 | 형식 |
|------|------|------|
| `date` | 날짜 선택 | YYYY-MM-DD |
| `month` | 월/연도 선택 | YYYY-MM |
| `week` | 주/연도 선택 | YYYY-WNN |
| `time` | 시간 선택 | HH:MM |
| `datetime-local` | 날짜+시간 선택 | YYYY-MM-DDTHH:MM |

```html
<input type="date" name="stuBirth" id="sBirth">
<input type="time" name="stuSleep" id="sSleep">
```

#### input type — 기타

| type | 설명 |
|------|------|
| `color` | 색상 선택 (RGB 값 전달) |
| `file` | 파일 선택 |
| `hidden` | 화면에 보이지 않는 숨겨진 값 전달 |
| `submit` | 폼 제출 버튼 (`value`로 버튼 이름 지정) |
| `reset` | 폼 초기화 버튼 |
| `image` | 이미지 제출 버튼 (`src`로 이미지 경로 지정) |
| `button` | 일반 버튼 (`onclick`으로 JS 연결) |

```html
<input type="submit" value="전송">
<input type="reset" value="초기화">
<input type="image" src="logo.png">
<input type="button" value="경고" onclick="alert('누르지 말 것!')">
<input type="hidden" name="hidden" value="숨겨진 값">
```

#### input 보조 속성

| 속성 | 설명 | 적용 type |
|------|------|-----------|
| `value` | 초기값 설정 | 모든 type |
| `readonly` | 읽기 전용 (수정 불가) | 모든 type |
| `autofocus` | 페이지 로딩 시 자동 포커스 | 모든 type |
| `required` | 필수 입력 (비어있으면 제출 불가) | text, search, url, tel, email, password, date, number, checkbox, radio, file |
| `placeholder` | 힌트 텍스트 (회색으로 표시, 입력 시 사라짐) | text, search, url, tel, email, password |
| `autocomplete` | 자동완성 (`on`/`off`) | text, search, url, tel, email, password, range, color 등 |
| `disabled` | 사용 불가 모드 | 모든 type |
| `min` | 최솟값 | number, range, date, datetime-local, month, time, week |
| `max` | 최댓값 | number, range, date, datetime-local, month, time, week |
| `step` | 값의 간격 | number, range, date, datetime-local, month, time, week |
| `size` | input 박스 크기 (문자 수 단위) | text 계열 |
| `minlength` | 최소 입력 길이 | text 계열 |
| `maxlength` | 최대 입력 길이 | text 계열 |
| `list` | datalist id 연결 | text |

```html
<!-- 보조 속성 예시 -->
<input type="text" name="stuName" id="sName" autofocus required>
<input type="email" name="stuMail" placeholder="x@y.z">
<input type="tel" name="stuNTel" autocomplete="on">
<input type="text" name="stuUniv" minlength="3" maxlength="7">
<input type="range" name="stuGPA" min="0" max="4.5" step="0.5">
```

---

### iframe — 외부 페이지/콘텐츠 삽입

```html
<iframe src="URL" width="너비" height="높이" [속성...]></iframe>
```

| 속성 | 설명 | 예시 |
|------|------|------|
| `src` | 삽입할 페이지 URL | `src="https://..."` |
| `width` | 가로 크기 (px 또는 %) | `width="560"` |
| `height` | 세로 크기 (px 또는 %) | `height="315"` |
| `title` | 접근성 설명 텍스트 | `title="YouTube video player"` |
| `frameborder` | 테두리 유무 (`0`=없음, `1`=있음) | `frameborder="0"` |
| `allowfullscreen` | 전체화면 허용 (값 없는 불리언 속성) | `allowfullscreen` |
| `allow` | 허용할 기능 목록 (세미콜론 구분) | `allow="autoplay; fullscreen"` |
| `referrerpolicy` | Referrer 헤더 정책 | `referrerpolicy="strict-origin-when-cross-origin"` |
| `name` | iframe 이름 (a 태그 target으로 연결) | `name="myFrame"` |

#### YouTube 영상 삽입 (hw_1.html)

```html
<!-- YouTube 공유 → 퍼가기 코드에서 복사한 형태 -->
<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/영상ID?si=..."
  title="YouTube video player"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
  referrerpolicy="strict-origin-when-cross-origin"
  allowfullscreen>
</iframe>
```

- `src`의 URL 형식: `youtube.com/embed/영상ID` (watch?v= 가 아닌 embed/ 경로)
- `allow`: 영상 재생에 필요한 권한 목록. autoplay, 클립보드, PiP 등 허용
- `allowfullscreen`: 이것 없으면 전체화면 버튼이 동작하지 않음

#### 페이지 내 앵커 + iframe 조합 패턴 (hw_1.html)

```html
<!-- 상단 목차: 앵커 링크 -->
<ol>
  <li><a href="#homework01">과제 1</a></li>
  <li><a href="#homework02">과제 2</a></li>  ← 클릭 시 iframe 섹션으로 이동
</ol>

<!-- 해당 섹션 -->
<h1 id="homework02">두 번째 과제</h1>
<iframe src="https://www.youtube.com/embed/..."></iframe>

<a href="#Menu">뒤로</a>  ← 상단으로 돌아가기
```

- `href="#id"` → 같은 페이지 내 해당 id를 가진 요소로 스크롤 이동
- `<br>`을 여러 개 넣어 섹션 간 간격 확보 (CSS 없이 공간 만드는 방법)

#### a 태그 target으로 iframe에 페이지 열기

```html
<!-- iframe에 name 지정 -->
<iframe name="content" width="800" height="400"></iframe>

<!-- 링크 클릭 시 iframe 안에서 열림 -->
<a href="page1.html" target="content">페이지 1</a>
<a href="page2.html" target="content">페이지 2</a>
```

- `target` 값과 `iframe`의 `name` 값이 일치하면 해당 iframe 안에서 링크 열림
- `target="_blank"`: 새 탭, `target="_self"`: 현재 탭 (기본값)

```
[시각적 구조]

┌─ 현재 페이지 ────────────────────────┐
│  <a href="a.html" target="f">링크</a>│
│                                      │
│  ┌─ iframe name="f" ───────────────┐ │
│  │  a.html 내용이 여기에 표시됨    │ │
│  │  (독립적인 브라우징 컨텍스트)   │ │
│  └─────────────────────────────────┘ │
└──────────────────────────────────────┘
```

#### 주의사항

| 상황 | 설명 |
|------|------|
| 동일 출처 정책 (Same-Origin Policy) | 다른 도메인의 iframe 내부 DOM은 JS로 접근 불가 |
| `X-Frame-Options` | 일부 사이트는 iframe 삽입 자체를 차단 (예: Google) |
| 반응형 크기 | `width="100%"` + CSS `aspect-ratio` 또는 래퍼 div로 처리 |

---

### 레이아웃 / 컨테이너

| 태그 | 설명 | 사용 파일 |
|------|------|-----------|
| `<div>` | 블록 컨테이너 | 거의 모든 파일 |
| `<ul id="buttons">` | 버튼 목록 컨테이너 | final/index.html |

---

## CSS 속성 정리

### 선택자 우선순위 (Specificity)

```
!important  →  가장 높음 (모든 것을 무시)
인라인 style  →  <p style="color:red">
#id 선택자  →  #header
.class / [attr] / :pseudo-class 선택자  →  .active, [type="text"], :hover
태그(tag) 선택자  →  p, div, h1
```

> 동일 우선순위면 나중에 정의된 것이 적용됨

---

### 색상 / 배경

| 속성 | 예시 | 설명 |
|------|------|------|
| `color` | `color: red` | 글자 색상 |
| `background-color` | `background-color: skyblue` | 배경 색상 |
| `background` | `background: radial-gradient(...)` | 그라디언트 배경 |

```css
/* 방사형 그라디언트 (exam/4.html) */
background: radial-gradient(circle at center, #8bc34a 40%, #4caf50 60%);
```

---

### 텍스트 스타일

| 속성 | 예시 | 사용 파일 |
|------|------|-----------|
| `font-size` | `font-size: 2em` | pre4/sol7 |
| `font-weight` | `font-weight: bold` | mid4.html |
| `text-align` | `text-align: center` | pre1/2.html |
| `text-decoration` | `text-decoration: underline` | mid.html (인라인) |
| `font-family` | `font-family: Arial` | exam/2.html |

---

### 박스 모델

```
┌─────────────── margin ───────────────┐
│  ┌──────────── border ─────────────┐ │
│  │  ┌──────── padding ───────────┐ │ │
│  │  │         content            │ │ │
│  │  └────────────────────────────┘ │ │
│  └─────────────────────────────────┘ │
└──────────────────────────────────────┘
```

- `width` / `height`: **content 영역**만의 크기 (기본값)
- `box-sizing: border-box`: padding + border 포함한 전체 크기를 width/height로 설정

| 속성 | 설명 | 예시 |
|------|------|------|
| `width` / `height` | 크기 | `width: 500px` |
| `padding` | 안쪽 여백 (content ↔ border) | `padding: 10px` |
| `border` | 테두리 | `border: solid 1px black` |
| `margin` | 바깥 여백 (border 바깥) | `margin: 40px auto` |
| `box-sizing: border-box` | 패딩/보더 포함 크기 계산 | - |
| `box-shadow` | 그림자 | `box-shadow: 0 0 0 3px #795548 inset` |
| `overflow` | 내용 넘침 처리 | `overflow: auto` |

#### padding / margin 단축 표기

```css
padding: 10px;              /* 상하좌우 모두 10px */
padding: 10px 20px;         /* 상하 10px, 좌우 20px */
padding: 10px 20px 30px;    /* 상 10px, 좌우 20px, 하 30px */
padding: 10px 20px 30px 40px; /* 상 우 하 좌 (시계방향) */
```

#### margin collapse (마진 겹침)
- 인접한 블록 요소의 **상하 마진**은 겹침 (두 마진 중 **큰 값**만 적용)
- 좌우 마진은 겹치지 않고 합산됨

---

### CSS 단위

| 단위 | 설명 | 예시 |
|------|------|------|
| `px` | 픽셀 (절대 단위) | `font-size: 16px` |
| `%` | 부모 요소 기준 비율 | `width: 50%` |
| `em` | 현재 요소의 font-size 기준 배수 | `padding: 1.5em` |

---

### display 속성

| 값 | 설명 |
|----|------|
| `block` | 줄 전체 차지, width/height/margin 설정 가능 (`div`, `p`, `h1` 기본값) |
| `inline` | 내용만큼 차지, width/height 설정 불가, 상하 margin 무시 (`span`, `a`, `img` 기본값) |
| `inline-block` | 인라인처럼 줄 나란히, block처럼 width/height 설정 가능 |
| `none` | 요소 숨기기 (공간도 사라짐, `visibility:hidden`은 공간 유지) |

---

### position 속성

```
[static / relative]                [absolute]

┌─ body ──────────────────┐        ┌─ body ──────────────────┐
│  ┌──────┐               │        │  ┌─ relative 부모 ─────┐ │
│  │ div1 │ ← 자리 차지    │        │  │  ┌──────┐           │ │
│  └──────┘               │        │  │  │absolu│ top:10px  │ │
│  ┌──────┐               │        │  │  │te box│ left:20px │ │
│  │ div2 │               │        │  │  └──────┘ ↑부모기준  │ │
│  └──────┘               │        │  └───────────────────── ┘ │
└─────────────────────────┘        └─────────────────────────┘

relative: 원래 자리 유지하면서 top/left 만큼 시각적 이동
absolute: 부모(non-static) 기준. normal flow에서 완전히 빠짐 → 다른 요소와 겹침

[fixed]
┌─ viewport ──────────────┐
│  ┌────────────────────┐  │
│  │ fixed header       │  │  ← 스크롤해도 항상 같은 자리
│  └────────────────────┘  │
│  (스크롤되는 내용)         │
│  ...                     │
└─────────────────────────┘
```

| 값 | 설명 | top/left 기준 |
|----|------|---------------|
| `static` | 기본값, 문서 흐름 그대로 | 무시됨 |
| `relative` | 자기 원래 위치 기준으로 이동 | 원래 위치 기준 |
| `absolute` | 가장 가까운 **non-static 부모** 기준으로 절대 위치 | 부모 기준 |
| `fixed` | 뷰포트(브라우저 창) 기준 고정 (스크롤해도 안 움직임) | 뷰포트 기준 |
| `sticky` | 스크롤 시 특정 위치에 고정 | 스크롤 위치 기준 |

```css
/* 겹침 배치 기본 패턴 (mid5.html, 3_sol.html) */
.wrapper {
  position: relative;
  width: 300px;
  height: 80px;
}
.box {
  position: absolute;
  z-index: 1;
}
.text {
  position: absolute;
  z-index: 2;
}
```

---

### z-index (쌓임 순서)

```
화면 앞 ↑
        z-index: 999  ← hover 시 최상단
        z-index: 3
        z-index: 2
        z-index: 1
화면 뒤 ↓

[side view]
  ___________  z:3 (가장 앞)
 ___________   z:2
___________    z:1 (가장 뒤)
```

- `z-index` 값이 클수록 위에 표시됨
- **`position`이 `static`이 아닌 요소에만 적용됨**
- 같은 부모 안에서의 상대적 순서만 의미 있음

```css
div.left  { z-index: 1; }
div.right { z-index: 2; }   /* right가 위에 표시 */
div:hover { z-index: 999; } /* hover 시 최상단 */
```

---

### 테이블 CSS

| 속성 | 예시 | 설명 |
|------|------|------|
| `border-collapse: collapse` | - | 셀 간격 제거, 테두리 합치기 |
| `border-spacing` | `border-spacing: 0` | 셀 간격 (collapse 시 무효) |

```css
/* 기본 테이블 스타일 패턴 */
table {
  border-collapse: collapse;
  width: 100%;
}
th, td {
  border: 1px solid #ccc;
  padding: 10px 8px;
}
```

---

### 선택자

#### 기본 선택자
```css
div           /* 태그 선택자 */
.class-name   /* 클래스 선택자 */
#id-name      /* ID 선택자 */
div.child     /* 태그 + 클래스 */
```

#### 자식/후손 선택자
```css
tbody > tr          /* tbody의 직접 자식 tr */
tr > td:first-child /* tr의 첫 번째 td */
ol ul li            /* ol 안의 ul 안의 li (후손) */
```

#### 의사 클래스 (pseudo-class)
| 선택자 | 설명 | 사용 파일 |
|--------|------|-----------|
| `:hover` | 마우스 올렸을 때 | pre1/3.html, mid5.html |
| `:nth-child(n)` | n번째 자식 | pre1/2.html |
| `:nth-child(odd)` | 홀수 번째 | 2_sol.html |
| `:nth-child(2n+1)` | 홀수 번째 (동일) | mid4.html |
| `:nth-of-type(n)` | 같은 타입 중 n번째 | mid4.html |
| `:nth-last-of-type(2n+1)` | 뒤에서 홀수 번째 | mid2.html, 1_sol.html |
| `:first-child` | 첫 번째 자식 | mid4.html |

```css
/* zebra stripe 패턴 */
tbody > tr:nth-child(odd) { background-color: #e3efff; }

/* 첫 번째 열은 흰색 유지 */
tbody > tr > td:first-child { background-color: white; }

/* 홀수 항목 빨간색 */
ol ul li:nth-last-of-type(2n+1) { color: red; }
```

---

### 애니메이션 / 트랜지션

---

#### transform — 요소 변형

`transform: 함수(값)` 형태로 사용. 레이아웃에 영향을 주지 않고 시각적으로만 변형.

##### transform 함수 목록

| 함수 | 파라미터 | 설명 | 예시 |
|------|----------|------|------|
| `translateX(x)` | 픽셀 또는 % | X축 이동 (양수 → 오른쪽) | `translateX(250px)` |
| `translateY(y)` | 픽셀 또는 % | Y축 이동 (양수 → 아래) | `translateY(-50px)` |
| `translate(x, y)` | X, Y 값 | X/Y 동시 이동 | `translate(100px, 50px)` |
| `rotate(angle)` | 각도 (deg) | 회전 (양수 → 시계방향, 음수 → 반시계) | `rotate(-25deg)` |
| `scaleX(n)` | 배율 숫자 | X축 크기 배율 | `scaleX(2)` → 가로 2배 |
| `scaleY(n)` | 배율 숫자 | Y축 크기 배율 | `scaleY(0.5)` → 세로 반 |
| `scale(x, y)` | X배율, Y배율 | X/Y 동시 크기 변경 | `scale(1.5, 1.5)` |
| `skewX(angle)` | 각도 (deg) | X축 기울이기 | `skewX(20deg)` |
| `skewY(angle)` | 각도 (deg) | Y축 기울이기 | `skewY(10deg)` |

```css
/* 여러 transform 함수 동시 적용 (공백으로 나열) */
transform: translateX(100px) rotate(45deg) scale(1.2);
```

---

#### transition — 변화 애니메이션

`transition: 속성명 지속시간 타이밍함수 지연시간`

| 구성요소 | 설명 | 예시 |
|----------|------|------|
| `속성명` | 애니메이션 적용할 CSS 속성 (`all` → 전체) | `transform`, `color`, `all` |
| `지속시간` | 변화에 걸리는 시간 (s 또는 ms) | `0.5s`, `300ms` |
| `타이밍함수` | 변화 속도 곡선 (생략 가능) | `ease`(기본), `linear`, `ease-in`, `ease-out`, `ease-in-out` |
| `지연시간` | 이벤트 후 몇 초 뒤에 시작 (생략 가능, 기본 0s) | `0.2s` |

**타이밍 함수**
| 값 | 설명 |
|----|------|
| `ease` | 처음 빠르게, 끝 느리게 (기본값) |
| `linear` | 일정한 속도 |
| `ease-in` | 처음에 천천히 시작 |
| `ease-out` | 끝에 천천히 끝남 |
| `ease-in-out` | 처음과 끝 모두 천천히 |

```css
/* 기본 패턴: 초기 상태에 transition 정의 → 변화 상태에 transform 정의 */
.box {
  transition: transform 0.5s ease;   /* 여기에 transition 설정 */
}
.box:hover {
  transform: translateX(250px);       /* 여기에 변화할 값 설정 */
}

/* 여러 속성 동시 transition */
.box {
  transition: transform 0.5s ease, background-color 0.3s linear;
}

/* 모든 속성에 적용 */
.box {
  transition: all 0.5s ease;
}
```

---

#### transform + transition 조합 패턴

```css
/* 패턴 1: hover 시 옆으로 슬라이드 (mid5.html) */
.box {
  transition: transform 0.5s ease;  /* 평소: transition만 */
}
.wrapper:hover .box {
  transform: translateX(250px);     /* hover: transform 적용 → 애니메이션 */
}

/* 패턴 2: hover 시 회전, 2초 (pre1/3_sol.html) */
div.child:hover {
  transform: rotate(-25deg);
  transition: transform 2s;         /* hover 상태에 같이 써도 동작함 */
}

/* 패턴 3: hover 시 크기 + 색상 동시 변화 */
.card {
  transition: transform 0.3s ease, background-color 0.3s ease;
  background-color: white;
}
.card:hover {
  transform: scale(1.05);
  background-color: #f0f0f0;
}

/* 패턴 4: z-index + hover 최상단 (pre1/3_sol.html) */
div:hover {
  z-index: 999;
}
div.child:hover {
  transform: rotate(-25deg);
  transition: transform 2s;
}
```

> **핵심 규칙**: `transition`은 **원래 상태** 요소에 쓰고, `transform`은 **변화 상태** (`:hover` 등)에 씀

---

### 기타 CSS

| 속성 | 예시 | 설명 | 사용 파일 |
|------|------|------|-----------|
| `float` | `float: right` | 요소 부유 | final/sol4 |
| `visibility` | `visibility: hidden` | 숨기기 (공간 유지) | pre4/sol5 |
| `margin` | `margin: 40px auto` | 바깥 여백 / 중앙 정렬 | exam/4.html |

---

## 인라인 스타일

```html
<!-- 인라인 스타일 예시 (pre1/1.html 제약 조건) -->
<td rowspan="2" style="text-align: none">없음</td>
<span style="text-decoration: underline;">밑줄 텍스트</span>
<p style="font-size: 9px;">작은 텍스트</p>
<td colspan="7" style="text-align:center; background-color: #f4f4f4;">Summary</td>
```

---

## 솔루션 해법 해설

> 각 과제 솔루션이 **왜 그렇게 짜여졌는지** 의도와 핵심 기법 설명

---

### exam/0_sol.html — CSS 없이 HTML 태그만으로 공지사항 구성

**결과 화면 (브라우저 렌더링)**
```
과제명 : 웹 프로그래밍 중간고사          ← <h1> 큰 제목
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• 제출일 : 2025년 4월 19일 (월요일)
• 제출 방법 : 이메일 (jinw.jeong@...)로
  zip 으로 압축하여 제출                  ← <abbr>: 마우스 올리면 툴팁
• 주의사항 : 제출 마감 30분 전까지       ← <b>: 굵게
  제출해야 하며,                          ← <br>: 여기서 줄바꿈
  이메일 제목은 반드시 "2025웹중간 홍길동"← <u>: 밑줄
  으로 작성할 것

파일명 : hw2.final.html                  ← <small>: 작은 글씨
제목 : 2025웹중간_홍길동

Tip: Ctrl+S로 저장하고, 제출 전 파일 누락← <mark>: 형광펜 하이라이트
여부를 꼭 확인하세요.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ ← <hr>
추가 공지사항                            ← <h3> 작은 제목
• "기한을 지키는 습관은..."               ← <q>: 자동으로 따옴표 추가
```

**문제 조건**: CSS 완전 금지, HTML 시맨틱 태그만 사용

```html
<h1>과제명 : 웹 프로그래밍 중간고사</h1>
<ul>
  <li>제출일 : ...</li>
  <li>제출 방법 : 이메일 (<a href="mailto:...">주소</a>)로
    <abbr title="zip archive">zip</abbr>으로 압축하여 제출</li>
  <li>주의사항 : 제출 마감 <b>30분 전까지</b> 제출해야 하며,<br>
    이메일 제목은 반드시 <u>"2025웹중간 홍길동"</u>으로 작성할 것</li>
</ul>
<p><small>파일명 : hw2.final.html</small></p>
<p>Tip: ... <mark>파일 누락</mark> 여부를 꼭 확인하세요.</p>
<hr>
<h3>추가 공지사항</h3>
<ul>
  <li><q>기한을 지키는 습관은...</q> - 김교수</li>
</ul>
```

**핵심 선택 이유**

| 태그 | 왜 이 태그를 썼는가 |
|------|-------------------|
| `<h1>`, `<h3>` | CSS 없이 제목 크기 차이를 표현하는 유일한 방법 |
| `<ul>` + `<li>` | 항목 나열 → 순서 없는 목록이 자연스러움 |
| `<a href="mailto:...">` | 클릭하면 메일 앱 열리는 이메일 링크 |
| `<abbr title="zip archive">` | zip 약어에 마우스 올리면 툴팁으로 설명 표시 |
| `<b>` | CSS 없이 굵게 강조 (의미보다 시각 강조 목적) |
| `<u>` | CSS 없이 밑줄 표현 |
| `<br>` | 줄바꿈 (CSS margin 없이 개행하는 유일한 방법) |
| `<small>` | CSS 없이 작은 글씨 표현 |
| `<mark>` | CSS 없이 형광펜 하이라이트 |
| `<hr>` | CSS 없이 구분선 표현 |
| `<q>` | 인용문 → 브라우저가 자동으로 `"` 따옴표 추가 |

---

### exam/1_sol.html — 중첩 리스트 CSS 스타일링

**결과 화면 (브라우저 렌더링)**
```
■ 서울시                     ← ul: square 불릿
  A. 노원구                  ← ol: upper-alpha 번호
     • 상계동  ← 빨간색      ← ol ul: disc 불릿, nth-last-of-type 홀수=빨강
     • 중계동
     • 하계동  ← 빨간색
     • 공릉동
     • 월계동  ← 빨간색
■ 서울시
  A. 강남구
     • 논현동  ← 빨간색
     • 압구정동
     • 삼성동  ← 빨간색
     • 대치동
     • 역삼동  ← 빨간색

※ 뒤에서 세서 홀수 (5번째=역삼, 3번째=삼성, 1번째=논현) → 빨간색
```

**문제 조건**: body 수정 불가, `<style>` 태그만 추가 가능

```css
/* 최상위 ul: 사각형 불릿 */
ul { list-style-type: square; }

/* ol (구 단위): 알파벳 대문자 */
ol { list-style-type: upper-alpha; }

/* ol 안의 ul (동 단위): 원형 불릿 */
ol ul { list-style-type: disc; }

/* 동 목록 중 홀수 번째만 빨간색 */
ol ul li:nth-last-of-type(2n+1) { color: red; }
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `ul` → `square` | 최상위 레벨 강조, 기본값(disc)과 구분 |
| `ol` → `upper-alpha` | 구 단위 = 순서 있는 목록 → 알파벳 번호 |
| `ol ul` → `disc` | 후손 선택자로 `ol` 안의 `ul`만 타겟. `ul` 전체에 square를 이미 적용했으므로 **덮어써야** 함 |
| `:nth-last-of-type(2n+1)` | **뒤에서** 홀수 번째. `nth-child(odd)`가 아닌 이유: 5개 항목 기준으로 뒤에서 세야 1,3,5번째(상계,하계,월계)가 빨간색이 되는 문제 요구사항을 만족 |

> **`nth-child` vs `nth-last-of-type` 선택 이유**: `nth-child(odd)`는 앞에서 세므로 1,3,5번째가 빨간색. `nth-last-of-type(2n+1)`은 뒤에서 세므로 항목 수가 달라도 "마지막 기준 홀수"를 선택. 문제 요구사항이 뒤에서 홀수이므로 후자 사용.

---

### exam/2_sol.html — 테이블 rowspan + zebra stripe

**결과 화면 (브라우저 렌더링)**
```
┌──────────────┬───────────────┬────────────┬──────┬───────────────┬──────┬─────────────┐
│Submission    │Status         │Title       │ID    │Actions        │Note  │Category     │
│Deadline      │               │            │      │               │      │             │
├──────────────┼───────────────┼────────────┼──────┼───────────────┼──────┼─────────────┤
│              │complete       │MyPaper 01  │1052  │See submission │      │Conference 01│ ← 1행 파란배경
│Apr 11, 2025  ├───────────────┼────────────┼──────┼───────────────┼──────┼─────────────┤
│  (rowspan=2) │complete       │MyPaper 02  │2257  │See submission │      │Conference 01│ ← 2행 흰배경
├──────────────┼───────────────┼────────────┼──────┼───────────────┼──────┼─────────────┤
│              │complete       │MyPaper 03  │2421  │See submission │      │Conference 02│ ← 3행 파란배경
│Apr 09, 2025  ├───────────────┼────────────┼──────┼───────────────┼──────┼─────────────┤
│  (rowspan=2) │complete       │MyPaper 04  │3206  │See submission │      │Conference 02│ ← 4행 흰배경
├──────────────┼───────────────┼────────────┼──────┼───────────────┼──────┼─────────────┤
│              │accepted  ←녹색│MyPaper 05  │...   │...            │      │Conference 03│ ← 5행 파란배경
│Jan 23, 2025  ├───────────────┼────────────┼──────┼───────────────┼──────┼─────────────┤
│  (rowspan=4) │not accepted←적│MyPaper 06  │...   │...            │      │Conference 03│ ← 6행 흰배경
│              ├───────────────┼────────────┼──────┼───────────────┼──────┼─────────────┤
│              │...            │...         │...   │...            │      │...          │
├──────────────┴───────────────┴────────────┴──────┴───────────────┴──────┴─────────────┤
│              Summary: 12 papers submitted ...   (colspan=7, 중앙 정렬)                 │
└─────────────────────────────────────────────────────────────────────────────────────────┘

날짜 열: rowspan으로 병합, 항상 흰색
홀수 행: #e3efff 파란 배경 (zebra)
짝수 행: 흰색 배경
```

**문제 조건**: 같은 날짜 행들을 rowspan으로 묶고, 줄무늬 + 상태별 색상 적용

```css
/* zebra stripe: tbody 홀수 행 */
tbody tr:nth-child(odd) { background-color: #e3efff; }

/* 날짜 열(첫 번째 td)은 zebra에서 제외 → 흰색 덮어쓰기 */
tbody tr td:first-child { background-color: white; }

/* 상태별 색상 클래스 */
.status-complete   { color: gray; }
.status-accepted   { color: green; font-weight: bold; }
.status-not-accepted { color: red; font-weight: bold; }
```

```html
<!-- rowspan: 같은 날짜가 2행이면 rowspan="2", 4행이면 rowspan="4" -->
<tr>
  <td rowspan="2">Apr 11, 2025</td>  <!-- 이 td가 2행을 차지 -->
  <td class="status-complete">complete</td>
  ...
</tr>
<tr>
  <!-- 날짜 td 없음 → rowspan으로 위 행의 td가 이미 차지 중 -->
  <td class="status-complete">complete</td>
  ...
</tr>
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `rowspan="N"` | 같은 날짜가 N개 행에 걸쳐 있으므로 첫 행 td에만 rowspan 지정, 이후 행에는 해당 td 생략 |
| `tbody tr:nth-child(odd)` | thead의 행은 제외하고 tbody 안에서만 홀수 행 색상 적용 |
| `td:first-child`에 white 덮어쓰기 | zebra stripe가 날짜 열에도 적용되면 rowspan된 셀 색상이 깨져 보이므로, 날짜 열은 항상 흰색 유지 |
| 클래스명으로 상태 구분 | 같은 상태가 여러 행에 반복되므로 인라인 스타일 대신 class 사용 → 유지보수 편리 |
| `colspan="7"` Summary 행 | 7개 열 전체를 하나로 합쳐 중앙 정렬 Summary 표시 |

---

### exam/3_sol.html — 글자 위 박스 겹침 + hover 슬라이드

**결과 화면 (브라우저 렌더링)**
```
[평소 상태]                        [hover 시]

┌─────────────────────┐            ┌──────────────────────────────────────┐
│░░░░░░░░░░░░░(skyblue)│            │루비짱~~~~~ (하이!)    ░░░░░░░(skyblue)│
│    글자가 박스에 가려짐│            │글자가 보임!             →→→이동→→→   │
└─────────────────────┘            └──────────────────────────────────────┘
  .wrapper (position:relative)       translateX(250px) 로 오른쪽 이동


[DOM 구조 및 레이어]

.wrapper (position: relative) ─── 기준점
  ├── .box   (position: absolute, z-index:1) ── skyblue 박스, 글자 위 덮음
  └── .text  (position: absolute, z-index:2) ── 글자, 박스 뒤에 숨어있음
                                                 hover 시 박스 이동 → 글자 노출
```

**문제 조건**: 글자 위에 박스가 덮고 있다가 hover 시 박스가 오른쪽으로 이동해 글자 노출

```css
.wrapper {
  position: relative; /* absolute 자식의 기준점이 됨 */
  width: 300px;
  height: 80px;
}

.box {
  position: absolute; /* wrapper 기준으로 절대 위치 */
  width: 200px;
  height: 60px;
  background-color: skyblue;
  z-index: 1;           /* 글자보다 위에 */
  transition: transform 1s ease; /* 이동 애니메이션 설정 */
}

.wrapper:hover .box {
  transform: translateX(250px); /* hover 시 오른쪽으로 이동 */
}

.text {
  position: absolute; /* wrapper 기준 절대 위치 */
  z-index: 2;         /* 주의: z-index 높아도 box 뒤에 있는 것처럼 보임
                         → box가 이동하면 글자 보임 */
  top: 15px;
  left: 10px;
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `wrapper: position: relative` | `absolute` 자식들이 "이 wrapper를 기준"으로 배치되게 하려면 부모에 반드시 `relative` (또는 non-static) 필요 |
| `.box: position: absolute` | normal flow에서 벗어나 `.text` 위에 겹쳐 배치하기 위함 |
| `.text: position: absolute` | wrapper 안에서 특정 위치(top/left)에 고정하기 위함. `relative` 부모 없으면 뷰포트 기준이 되어버림 |
| `z-index: 1` (box) vs `z-index: 2` (text) | box가 z-index 낮지만 box 색상이 텍스트 색상보다 불투명하므로 실제론 box가 글자를 덮음. hover 시 box가 이동하면 글자 노출 |
| `transition`을 `.box`에, `transform`을 `.wrapper:hover .box`에 | 원래 상태(`.box`)에 transition 정의 → hover/non-hover 양방향 모두 애니메이션 동작. hover에만 쓰면 mouse out 시 즉시 복귀 |
| `translateX` 사용 | `left` 속성 변경도 가능하지만 `transform`은 GPU 가속 → 더 부드러운 애니메이션 |

---

### pre1/2_sol.html — 5×5 테이블 대각선 셀 검은색

**결과 화면 (브라우저 렌더링)**
```
┌──────┬──────┬──────┬──────┬──────┐
│ 내용 │ 내용 │ 내용 │ 내용 │ 내용 │  ← 1행: 모두 흰색
├──────┼──────┼──────┼──────┼──────┤
│ 내용 │ 내용 │ 내용 │ 내용 │ 내용 │  ← 2행: 모두 흰색
├──────┼──────┼██████┼──────┼──────┤
│ 내용 │ 내용 │█흑█  │ 내용 │ 내용 │  ← 3행 3열: 검은색 ★
├──────┼──────┼──────┼──────┼──────┤
│ 내용 │ 내용 │ 내용 │ 내용 │ 내용 │  ← 4행: 모두 흰색
├──────┼──────┼──────┼──────┼██████┤
│ 내용 │ 내용 │ 내용 │ 내용 │█흑█  │  ← 5행 5열: 검은색 ★
└──────┴──────┴──────┴──────┴──────┘

테이블 전체: skyblue 배경 (padding 영역 + 셀 간격에서 노출)
각 td: white 배경 (skyblue 위를 덮음)
테두리: blue double 3px
```

**문제 조건**: 5×5 테이블, skyblue 배경, 특정 셀만 검은색 (대각선 패턴)

```css
table, td { border: double 3px blue; }
td { background-color: white; }
table {
  width: 500px; height: 500px;
  text-align: center;
  background-color: skyblue; /* td의 white가 덮으므로 테두리 간격에만 보임 */
  padding: 10px;
}

/* 대각선 셀만 검은색 */
tr:nth-child(3) td:nth-child(3) { background-color: black; }
tr:nth-child(5) td:nth-child(5) { background-color: black; }
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `table`에 `background-color: skyblue` | td에 white를 덮어쓰기 때문에 td 영역은 흰색. skyblue는 `padding` 영역 + 셀 사이 간격에만 노출 → 테두리 안쪽 여백이 skyblue로 보임 |
| `border: double 3px blue` | 문제 요구: double(이중선) 테두리 |
| `tr:nth-child(N) td:nth-child(N)` | 행 선택자와 열 선택자를 **체인**으로 연결해 특정 셀만 타겟. "3행 3열", "5행 5열"을 직접 지정 |
| 1행1열, 2행2열은 생략 | 문제가 지정한 검은 셀이 3,3과 5,5만이었으므로 (과제 요구사항에 따라 달라질 수 있음) |

---

### pre1/3_sol.html — 절대위치 + z-index + hover 회전

**결과 화면 (브라우저 렌더링)**
```
[평소 상태 - 두 큰 박스가 겹쳐 있음]

┌─────────────────────────────┐
│ div.left  (z-index:1)       │
│  ┌──────────────────────┐   │
│  │.child.one (z:1)      │   │
│  │  ┌───────────────┐   │   │
│  │  │.child.two(z:2)│   │   │
│  │  │  ┌──────────┐ │   │   │
│  │  │  │.three(z:3│ │   │   │
│  │  │  └──────────┘ │   │   │
│  │  └───────────────┘   │   │
│  └──────────────────────┘   │
│        ┌───────────────────────────────┐
│        │ div.right (z-index:2) ← 위에  │
│        │  같은 구조로 child 1~4...      │
│        └───────────────────────────────┘
└─────────────────────────────┘

[hover 시 동작]

div:hover        → z-index: 999 → 어떤 박스든 마우스 올리면 맨 위로 튀어나옴
div.child:hover  → rotate(-25deg) + transition 2s → 2초에 걸쳐 반시계 25도 회전

        ┌──────────┐          ╱──────────╲
        │child.two │  hover→  ╱  child.two╲  (25도 반시계 기울어짐)
        └──────────┘          ╲            ╱
                               ╲──────────╱
```

**문제 조건**: div.left / div.right 두 큰 박스가 겹쳐 있고, 안에 child 박스들이 계층적으로 쌓임. hover 시 최상단. child:hover 시 회전.

```css
div {
  border: solid black 1px;
  box-sizing: border-box;
  width: 500px; height: 500px;
  background-color: beige;
  position: absolute; /* 모든 div를 absolute로 → 겹침 가능 */
}
div.left  { z-index: 1; }
div.right { top: 200px; left: 300px; z-index: 2; } /* right가 left 위에 */

div.child { width: 250px; height: 250px; background-color: skyblue; }
div.one   { top: 50px;  left: 50px;  z-index: 1; }
div.two   { top: 100px; left: 100px; z-index: 2; }
div.three { top: 150px; left: 150px; z-index: 3; }
div.four  { top: 200px; left: 200px; z-index: 4; }

div:hover       { z-index: 999; } /* 어떤 div든 hover 시 최상단 */
div.child:hover { transform: rotate(-25deg); transition: transform 2s; }
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| 모든 `div`에 `position: absolute` | 서로 겹쳐 배치하려면 normal flow에서 벗어나야 함. `relative`는 자리를 차지하므로 겹침 안 됨 |
| `div.right`에 `top/left` 지정 | 두 큰 박스를 일부 겹치게 배치 → top/left로 오프셋 |
| child에 순차적 `z-index` (1,2,3,4) | 번호순으로 위에 쌓이는 시각적 계층감 표현 |
| `div:hover { z-index: 999 }` | 999는 임의의 큰 값 → 현재 정의된 모든 z-index(최대 4)보다 크면 됨. 어떤 박스든 마우스 올리면 맨 위로 |
| `transition`을 `:hover` 안에 작성 | 원래 상태에 써도 동작하지만, hover에 같이 써도 유효. 다만 mouse out 시에는 즉시 복귀 (애니메이션 없음). 원래 상태에 쓰면 양방향 애니메이션 |
| `rotate(-25deg)` | 음수 → 반시계방향 25도. 시각적으로 "기울어짐" 표현 |

---

### mid2.html vs 1_sol.html — 중첩 리스트 (id 방식 vs 태그 방식)

**두 파일의 결과 화면은 동일**
```
■ 서울시
  A. 노원구
     • 상계동  ← 빨간색 (뒤에서 5번째=홀수)
     • 중계동
     • 하계동  ← 빨간색 (뒤에서 3번째=홀수)
     • 공릉동
     • 월계동  ← 빨간색 (뒤에서 1번째=홀수)
■ 서울시
  A. 강남구
     • 논현동  ← 빨간색
     • 압구정동
     • 삼성동  ← 빨간색
     • 대치동
     • 역삼동  ← 빨간색
```

**mid2.html (id 방식)**:
```css
#a1 { list-style-type: square; }
#a2 { list-style-type: upper-alpha; }
#a3 :nth-last-of-type(2n+1) { color: red; }
```
- HTML에 id를 직접 붙여서 각 리스트를 개별 타겟
- body가 미리 작성된 경우 id가 없으므로 사용 불가

**1_sol.html (태그 후손 선택자 방식)**:
```css
ul { list-style-type: square; }
ol { list-style-type: upper-alpha; }
ol ul { list-style-type: disc; }
ol ul li:nth-last-of-type(2n+1) { color: red; }
```
- body 수정 금지 조건 → id 추가 불가 → **태그/후손 선택자만** 사용
- `ol ul`로 계층 구조를 선택자에 반영

> **시험에서는 body 수정 금지 → 반드시 태그/후손 선택자 방식 사용**

---

### mid4.html vs 2_sol.html — 테이블 zebra stripe 선택자 차이

| | mid4.html | 2_sol.html |
|--|-----------|-----------|
| zebra 선택자 | `tbody > tr:nth-of-type(2n+1)` | `tbody tr:nth-child(odd)` |
| 날짜 열 흰색 | `tbody > tr > td:first-child` | `tbody tr td:first-child` |
| 차이 | `nth-of-type`: 같은 태그 유형 중 홀수 | `nth-child(odd)`: 부모 기준 홀수 자식 |

두 방식 모두 동작하지만 `nth-child(odd)`가 더 간결하고 일반적.

---

### mid5.html vs 3_sol.html — hover 슬라이드 구조 비교

**결과 화면 (mid5.html 기준, image.png 참고)**
```
[평소]                              [hover 시]

┌──────────────┐                   글자보임!  ┌──────────────┐
│  (red box)   │  어떤 게 좋을까요?  →→→→→→→  │  (red box)   │
└──────────────┘                             └──────────────┘

┌──────────────┐
│  (red box)   │  어떤 게 좋을까요?
└──────────────┘

┌──────────────┐
│  (red box)   │  어떤 게 좋을까요?
└──────────────┘

※ 실제 스크린샷(image.png): hover 시 빨간 박스가 오른쪽으로 이동하고
  텍스트 "루비짱~~"이 왼쪽에 노출되는 모습
```

| | mid5.html | 3_sol.html |
|--|-----------|-----------|
| wrapper 클래스명 | `.box-wrapper` | `.wrapper` |
| box z-index | 2 (텍스트보다 위) | 1 (텍스트보다 아래) |
| text z-index | 1 | 2 |
| transition | `.box`에 작성 | `.box`에 작성 |
| 이동 거리 | `translateX(250px)` | `translateX(250px)` |

두 방식 모두 **wrapper: relative → box/text: absolute** 패턴 동일. z-index 값의 절대값보다 **상대적 순서**만 중요.

---

## 2024 과제 솔루션 해설

### 2024/0.html — 시간표 (Timetable)

rowspan/colspan으로 시간 슬롯과 긴 수업을 병합하는 패턴.

```html
<style>
  table { width: 900px; border-collapse: collapse; }
  table th { background-color: gainsboro; }
  table tr td { border: 1px solid gainsboro; }
</style>

<table>
  <tr>
    <th>Time</th><th>Monday</th>...<th>Friday</th>
  </tr>
  <tr>
    <td>8:00 - 9:00</td>
    <td rowspan="2">Calculus (Dr. Lee)</td>   <!-- 2행 점유 -->
    <td>Literature (Prof. Kim)</td>
    <td colspan="2">Chemistry Lab (Ms. Park)</td>  <!-- 2열 점유 -->
    <td>History (Mr. Choi)</td>
  </tr>
  <tr>
    <td>9:00 - 10:00</td>
    <!-- rowspan 때문에 Monday 셀 없음 -->
    <td></td>
    ...
  </tr>
</table>
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `rowspan="2"` | 같은 수업이 2시간 연속 → 셀 수직 병합 |
| `colspan="2"` | 실험 수업이 2개 열(요일) 동시 사용 → 셀 수평 병합 |
| `border-collapse: collapse` | 기본값은 `separate` → 셀 경계선이 2겹으로 보임. `collapse`로 1겹으로 합침 |
| rowspan 사용 후 다음 행 셀 수 감소 | rowspan된 셀은 다음 행에서 해당 열 자리를 차지하므로 `<td>` 1개 적게 써야 함 |

```
[시각화]
        Mon       Tue       Wed(+Thu)    Fri
8:00  Calculus  Liter.   Chemistry    History
      ─────────
9:00  (병합됨)   (빈칸)    Stats       (빈칸)
```

---

### 2024/1.html — 골포스트 + 공 hover 애니메이션

```html
<style>
  /* 골대: 3면 테두리만 그리기 */
  .goalpost {
    height: 180px;
    width: 320px;
    border-top-style: solid;
    border-top-width: 10px;
    border-left-style: solid;
    border-right-style: solid;
  }

  /* 공: 원형 + 고정 위치 */
  img {
    position: fixed;
    top: 300px; left: 150px;
    z-index: 10;
    border-radius: 100%;     /* 원형으로 만들기 */
    border: 5px solid black;
    transition: 2s;          /* hover 애니메이션 지속 2초 */
  }

  /* hover 시: 공이 위로 날아가며 2바퀴 회전 */
  div img:hover {
    transform: translateX(-100px) translateY(-250px) rotate(2turn);
  }

  /* 패널티 서클 */
  div.penlaty {
    border-radius: 100%;
    border: 5px dashed red;
  }
</style>
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `border-top/left/right-style` 개별 지정 | 아래쪽(bottom) 테두리는 없어야 골대 모양 → 개별 속성으로 3면만 적용 |
| `border-radius: 100%` | 50% 이상이면 타원/원형. 정사각형 요소에 적용 시 완전한 원 |
| `rotate(2turn)` | `turn` 단위 = 1바퀴. `2turn` = 360°×2 = 720° 회전. `deg`로는 `720deg` |
| `transition: 2s` | 원본 요소에 작성해야 hover 해제 시에도 역방향 애니메이션 적용됨 |
| `position: fixed` | 스크롤과 무관하게 화면 고정 위치에 공 배치 |
| `translateX(-100px) translateY(-250px)` | 왼쪽 위로 이동. 음수값 = 왼쪽/위쪽 방향 |

**transform 단위 비교**

| 표현 | 의미 |
|------|------|
| `rotate(90deg)` | 90도 회전 |
| `rotate(0.25turn)` | 1/4 바퀴 = 90도 |
| `rotate(1turn)` | 360도 (한 바퀴) |
| `rotate(2turn)` | 720도 (두 바퀴) |

**개별 border 속성**

```css
/* 전체 한번에 */
border: 10px solid black;

/* 각 면 개별 설정 */
border-top: 10px solid;
border-bottom: none;   /* 또는 작성 안 함 */
border-left: 5px solid;
border-right: 5px solid;

/* 속성 단위로 개별 설정 */
border-top-style: solid;
border-top-width: 10px;
border-top-color: black;
```

```
[골대 모양]
──────────────────  ← border-top
│                │
│                │
│                │  ← border-left, border-right 만 있음
  (바닥 없음)       ← border-bottom 없음
```

---

### 2024/2.html — qmenu 레이아웃 (relative + z-index + target)

```html
<style>
  a {
    position: relative;
    z-index: 10;    /* 링크가 이미지 위에 위치 */
  }
  .box_img {
    position: relative;
    z-index: 2;
  }
</style>

<!-- 새 탭으로 열기 -->
<a href="https://admission.seoultech.ac.kr" target="_blank">학부</a>
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `a { position: relative; z-index: 10; }` | z-index는 position이 설정된 요소에만 적용됨. 링크 클릭 영역이 이미지에 가려지지 않도록 위에 배치 |
| `target="_blank"` | 외부 링크를 새 탭에서 열기. 기본값 `_self`는 현재 탭 |
| z-index 상대적 순서 (a:10 > .box_img:2) | 절대값보다 상대적 크기만 중요. a가 이미지보다 높아야 클릭 가능 |

**target 속성 값**

| 값 | 설명 |
|----|------|
| `_self` | 현재 탭 (기본값) |
| `_blank` | 새 탭/창 |
| `_parent` | 부모 프레임 |
| `_top` | 최상위 프레임 |

---

### pre3/pre3.html — 쇼핑 리스트 (DOM 생성 + 이벤트)

동적으로 항목 추가/삭제 + 전체 삭제 기능이 있는 쇼핑 리스트 골격.

```html
<!-- 구조 -->
<input type="text" name="item" autocomplete="off" />
<button id="add">Add item</button>
<button id="removeAll">Remove all</button>
<ul></ul>

<script>
  const list = document.querySelector("ul");
  const input = document.querySelector("input");
  const button = document.querySelector("#add");
  const button2 = document.querySelector("#removeAll");

  button.addEventListener("click", () => {
    // 글자, 버튼, list item element 생성
    // list item에 글자와 버튼 추가
    // list에 list item 추가
    listBtn.addEventListener("click", () => {
      // 해당 항목 삭제
    });
    input.focus();
  });

  button2.addEventListener("click", () => {
    // 추가된 항목들을 다 찾아서 삭제
  });
</script>
```

**구현 패턴 (미완성 부분 완성 예시)**

```js
button.addEventListener("click", () => {
  const li = document.createElement("li");
  const span = document.createElement("span");
  const listBtn = document.createElement("button");

  span.textContent = input.value;
  listBtn.textContent = "Delete";
  li.appendChild(span);
  li.appendChild(listBtn);
  list.appendChild(li);

  listBtn.addEventListener("click", () => {
    list.removeChild(li);   // 클로저: li를 캡처
  });

  input.value = "";   // 입력창 초기화
  input.focus();
});

button2.addEventListener("click", () => {
  list.innerHTML = "";  // 전체 삭제 (간단)
  // 또는: while(list.firstChild) list.removeChild(list.firstChild);
});
```

| 결정 | 이유 |
|------|------|
| `listBtn` 클로저로 `li` 캡처 | `addEventListener` 콜백 안에서 외부 `li` 변수 참조 가능 → 항목별로 독립적인 삭제 동작 |
| `list.removeChild(li)` | 해당 li만 삭제. `li.remove()`도 동일 |
| `list.innerHTML = ""` | 전체 자식 삭제. 이벤트 리스너는 남아있지만 DOM에서 제거되므로 실용적 |
| `input.focus()` | 추가 후 포커스 복귀 → UX 개선 |
