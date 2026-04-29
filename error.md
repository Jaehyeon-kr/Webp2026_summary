# 주의해야 할 에러 & 실수 모음

> Ctrl+F 로 에러명, 증상, 키워드 검색
> 실제 과제 파일에서 발생한 버그 + 개념적으로 자주 틀리는 패턴 정리

---

## JS 에러

---

### E1. 비교 연산자 체이닝 — 항상 true 버그 ★★★

**발생 파일**: `2024/hw3.html` quest4

```js
// ❌ 틀림: 1 <= random < 2 는 항상 true
if (1 <= random < 2) {  computer = "가위"; }
if (2 <= random < 3) {  computer = "바위"; }
```

**이유**
```
JS는 왼쪽부터 평가:
(1 <= random)  → true 또는 false (boolean)
true < 2       → 1 < 2 → true  ← 항상 true!
false < 2      → 0 < 2 → true  ← 항상 true!
```

**결과**: 어떤 random 값이 와도 항상 첫 번째 if 블록만 실행 → `computer`가 항상 "가위"

```js
// ✅ 올바름
if (random === 1)      { computer = "가위"; }
else if (random === 2) { computer = "바위"; }
else                   { computer = "보"; }

// 또는 범위 비교가 필요할 때
if (random >= 1 && random < 2) { ... }
```

---

### E2. prompt() 반환값은 항상 문자열 ★★★★

**발생 파일**: `pre4/sol1`, `2024/5.html`, `hw3.html` quest1 등

```js
// ❌ 문자열 + 문자열 = 문자열 연결
let num1 = prompt("숫자1");  // "3"
let num2 = prompt("숫자2");  // "5"
console.log(num1 + num2);   // "35"  ← 버그!

// ❌ 문자열 비교 → 사전순: "9" > "10" → true (버그!)
if (num1 > num2) { ... }
```

```js
// ✅ 올바름: 사용 전 반드시 형변환
let num1 = Number(prompt("숫자1"));   // 3
let num2 = Number(prompt("숫자2"));   // 5
console.log(num1 + num2);            // 8

// 또는 parseInt / parseFloat
let len = parseInt(prompt("길이:"));
```

**형변환 함수 비교**
| 함수 | 입력 예 | 결과 |
|------|---------|------|
| `Number("42")` | `"42"` | `42` |
| `Number("42px")` | `"42px"` | `NaN` |
| `parseInt("42px")` | `"42px"` | `42` (앞쪽 숫자만 파싱) |
| `parseFloat("3.14")` | `"3.14"` | `3.14` |
| `+"42"` | `"42"` | `42` (단항 + 연산자) |

---

### E3. var 없이 선언 → 전역 변수 오염 ★★★

**발생 파일**: `hw3.html` getDist, quest6, quest7, quest8, quest9

```js
// ❌ var/let/const 없이 사용 → 전역 변수가 됨
function getDist(p1, p2) {
  Double_dist = (p1[0]-p2[0])*(p1[0]-p2[0]) + ...;  // 전역 변수!
  dist = Math.sqrt(Double_dist);                      // 전역 변수!
  return dist;
}

function quest5() {
  str = prompt("...");  // 전역 변수! → 다른 함수에서 str 접근 가능
}
```

```js
// ✅ 올바름: 반드시 선언 키워드 사용
function getDist(p1, p2) {
  let doubleDist = ...;
  let dist = Math.sqrt(doubleDist);
  return dist;
}
```

**증상**: 함수 안에서 만든 변수가 다른 함수에서도 보임 → 예측 불가능한 동작

---

### E4. DOM 요소가 없을 때 스크립트 실행 → null 에러 ★★★★

**발생 위치**: `<head>` 안 `<script>`에서 DOM 선택 시

```js
// ❌ <head> 안 script에서 실행하면 body가 아직 없음
document.getElementById("btn").addEventListener("click", f);
// TypeError: Cannot read properties of null (reading 'addEventListener')
```

```js
// ✅ 해결 1: <script>를 </body> 바로 앞에 배치
<body>
  <button id="btn">클릭</button>
  <script>
    document.getElementById("btn").addEventListener("click", f);
  </script>
</body>

// ✅ 해결 2: window.onload 또는 DOMContentLoaded 사용
window.onload = function() {
  document.getElementById("btn").addEventListener("click", f);
};
```

---

### E5. innerHTML vs textContent vs value 혼동 ★★★★

```js
// ❌ 잘못된 사용
input.innerHTML = "hello";   // input 요소에는 innerHTML 사용 불가 (효과 없음)
div.value = "hello";         // div에는 value 없음 → undefined

// ✅ 올바름
input.value = "hello";       // input 요소 값 읽기/쓰기
div.innerHTML = "<b>hello</b>"; // HTML 포함 내용
div.textContent = "hello";   // 텍스트만 (XSS 안전, HTML 태그 파싱 안 됨)
```

**요소별 올바른 접근**
| 요소 | 값 읽기/쓰기 | 내용 변경 |
|------|-------------|-----------|
| `input`, `textarea` | `.value` | `.value` |
| `div`, `p`, `span` | `.textContent` / `.innerHTML` | `.innerHTML` |
| `select` | `.value` (선택된 option의 value) | - |

---

### E6. `==` vs `===` 느슨한 비교 함정 ★★★

```js
// == : 타입 변환 후 비교 (느슨한)
"1" == 1    // true  ← 문자열 "1"이 숫자 1로 변환됨
null == undefined  // true
0 == false  // true
"" == false // true

// === : 타입까지 완전히 같아야 true (엄격한)
"1" === 1   // false
null === undefined // false
```

```js
// pre4/sol3 에서 주의
if (str[i] == null) str[i] = 0;
// null과 undefined 둘 다 잡으려고 == 사용 (의도적)
// 엄격하게 하려면: str[i] === undefined || str[i] === null
```

---

### E7. position 없으면 top/left/z-index 무효 ★★★★

```css
/* ❌ static 요소에는 top/left/z-index 적용 안 됨 */
div {
  top: 100px;   /* 효과 없음 */
  left: 50px;   /* 효과 없음 */
  z-index: 10;  /* 효과 없음 */
}

/* ✅ position이 설정되어야 적용됨 */
div {
  position: relative;  /* 또는 absolute, fixed, sticky */
  top: 100px;
  left: 50px;
  z-index: 10;
}
```

**JS에서도 동일**
```js
img.style.position = "relative";  // 반드시 먼저 설정
img.style.top = "100px";          // 그 다음 top/left
```

---

### E8. transition은 원래 상태에, transform은 hover에 ★★★★★

```css
/* ❌ 틀림: transition을 hover에만 쓰면 mouse out 시 즉시 복귀 (애니메이션 없음) */
.box:hover {
  transform: translateX(250px);
  transition: transform 0.5s;  /* hover 진입할 때만 애니메이션 */
}

/* ✅ 올바름: transition은 원래 상태에 작성 */
.box {
  transition: transform 0.5s;  /* 진입·해제 양방향 애니메이션 */
}
.box:hover {
  transform: translateX(250px);
}
```

```
hover 진입: .box → .box:hover  → transition 발동 ✅
hover 해제: .box:hover → .box  → transition 발동 ✅ (원래 상태에 있으므로)
```

---

### E9. absolute 자식의 기준이 되려면 부모에 position 필요 ★★★★

```css
/* ❌ 부모가 static이면 absolute 자식은 <body> 기준으로 배치됨 */
.wrapper { /* position 없음 → static */ }
.box { position: absolute; top: 0; left: 0; }  /* body 기준! */

/* ✅ 부모에 relative 지정 → 자식이 부모 기준으로 배치 */
.wrapper { position: relative; }
.box { position: absolute; top: 0; left: 0; }  /* wrapper 기준! */
```

---

### E10. 카운터/누적 변수를 지역 변수로 선언하면 매번 초기화 ★★★

```js
// ❌ 클릭할 때마다 idx가 0으로 리셋
function sol6() {
  let idx = 0;  // 지역 변수 → 매번 초기화
  li.style.color = color[idx % 7];
  idx++;
}

// ✅ 전역 변수로 선언해야 누적됨
let idx = 0;  // 함수 밖에 선언
function sol6() {
  li.style.color = color[idx % 7];
  idx++;
}
```

**같은 원리가 적용되는 곳**
- `pre4/sol6`: `buttonColor` (색상 순환 인덱스)
- `pre4/sol9`: `xAxis`, `yAxis` (이미지 이동 좌표)
- `final/sol5`: 타이머 ID 변수

---

### E11. 문자열 누적: `str += ch` vs `str = ch + str` 방향 주의 ★★★

```js
let str = "";
for (let ch of "abc") {
  str += ch;        // "a" → "ab" → "abc"  (정방향)
  // str = ch + str // "a" → "ba" → "cba"  (역순)
}
```

```
str += ch       → 뒤에 붙임 → 정방향
str = ch + str  → 앞에 붙임 → 역순
```

**발생 파일**: `pre2/quest3`, `final/sol1` 역순 구현 시

---

### E12. Number() 변환 없이 textContent로 숫자 연산 ★★★

```js
// ❌ textContent는 문자열 → + 연산이 문자열 연결이 됨
counterDiv.textContent = counterDiv.textContent + 1;
// "0" + 1 → "01"  (원하는 결과: 1)

// ✅ Number()로 변환 후 연산
counterDiv.textContent = Number(counterDiv.textContent) + 1;
// 0 + 1 → 1
```

**발생 파일**: `final/sol5` (카운터 증가)

---

### E13. 정규식 마침표 `.` 이스케이프 필요 ★★

```js
// ❌ /./g → 모든 문자(.)와 매칭 (정규식에서 .은 임의의 한 문자)
str.replace(/./g, "")   // 모든 문자 제거 → 빈 문자열

// ✅ \.로 이스케이프 → 마침표 리터럴만 매칭
str.replace(/\./g, "")  // 마침표만 제거
```

**특수문자 이스케이프가 필요한 정규식 문자**
```
.  ^  $  *  +  ?  {  }  [  ]  \  |  (  )
→ 리터럴로 쓰려면 앞에 \ 붙이기
```

---

### E14. rowspan 사용 후 다음 행 `<td>` 개수 ★★★

```html
<!-- ❌ rowspan=2 사용 후 다음 행에 td를 그대로 쓰면 열이 밀림 -->
<tr>
  <td rowspan="2">날짜</td>
  <td>내용1</td>
  <td>내용2</td>   <!-- 3개 td → 총 4열 -->
</tr>
<tr>
  <td>내용3</td>   <!-- rowspan 때문에 여기에는 2개만 써야 함 -->
  <td>내용4</td>   <!-- 이렇게 하면 5열이 돼버림 -->
  <td>내용5</td>   <!-- ❌ 열 초과 → 레이아웃 깨짐 -->
</tr>

<!-- ✅ rowspan된 열 수만큼 다음 행 td 생략 -->
<tr>
  <td rowspan="2">날짜</td>  <!-- 1열 차지 → 다음 행에서 생략 -->
  <td>내용1</td>
  <td>내용2</td>
</tr>
<tr>
  <!-- 날짜 td 없음: rowspan이 이미 이 자리를 차지 중 -->
  <td>내용3</td>
  <td>내용4</td>
</tr>
```

---

### E15. for...in vs for...of 혼동 ★★★

```js
let arr = [10, 20, 30];
let obj = { a: 1, b: 2 };

// for...of: 배열/이터러블의 값
for (let val of arr) { console.log(val); }  // 10, 20, 30 ✅

// for...in: 객체의 키 (인덱스/프로퍼티명)
for (let key in obj) { console.log(key); }  // "a", "b" ✅

// ❌ 배열에 for...in 쓰면 인덱스(문자열) 순회
for (let i in arr) { console.log(i); }  // "0", "1", "2" → 값이 아닌 인덱스!

// ❌ 객체에 for...of 쓰면 TypeError
for (let val of obj) { }  // TypeError: obj is not iterable
```

---

### E16. `img.width` / `img.height` → DOM 추가 전에는 0 ★★

```js
// ❌ DOM에 추가하기 전 또는 이미지 로딩 전에는 0 반환
let img = document.createElement("img");
img.src = "photo.png";
console.log(img.width);   // 0 (로딩 전)

// ✅ DOM에 추가 후 onload에서 읽기
document.body.appendChild(img);
img.onload = function() {
  console.log(img.naturalWidth);   // 원본 픽셀 크기
  console.log(img.width);          // 렌더링 크기
};
```

---

### E17. `style.float` 속성명 ★

```js
// ❌ float는 JS 예약어 → .float 불가
element.style.float = "right";    // 일부 브라우저에서 동작 안 함

// ✅ cssFloat 또는 style["float"] 사용
element.style.cssFloat = "right";
element.style["float"] = "right";
```

---

## CSS 에러

---

### C1. `nth-child` vs `nth-of-type` 선택 실수 ★★★

```css
/* 상황: tbody 안 tr에 zebra stripe 적용 */

/* nth-child: 부모의 모든 자식 중 n번째 */
tbody tr:nth-child(odd) { ... }

/* nth-of-type: 같은 타입(tr) 중 n번째 */
tbody tr:nth-of-type(odd) { ... }

/* 두 방식 모두 동작하지만, thead가 있으면 차이 발생 가능 */
/* thead > tr이 첫 번째 자식이면 nth-child(1)에 포함될 수 있음 */
/* 안전한 방법: tbody > tr:nth-child(odd) (tbody로 범위 한정) */
```

---

### C2. `nth-child(odd)` vs `nth-last-of-type(2n+1)` 혼동 ★★★

```css
/* nth-child(odd): 앞에서 1, 3, 5번째 */
li:nth-child(odd) { color: red; }
/* 5개 항목: 1,3,5번째 → 빨간색 */

/* nth-last-of-type(2n+1): 뒤에서 1, 3, 5번째 */
li:nth-last-of-type(2n+1) { color: red; }
/* 5개 항목: 5,3,1번째(뒤에서) → 빨간색 */
```

```
항목: [A] [B] [C] [D] [E]
       1   2   3   4   5  ← nth-child(odd): A,C,E 빨간색
       5   4   3   2   1  ← nth-last-of-type(2n+1): A,C,E 빨간색 (5항목이면 동일)

항목: [A] [B] [C] [D]
       1   2   3   4   ← nth-child(odd): A,C 빨간색
       4   3   2   1   ← nth-last-of-type(2n+1): B,D 빨간색 (4항목이면 다름!)
```

**판단 기준**: 문제가 "앞에서 홀수번째"면 `nth-child(odd)`, "뒤에서 홀수번째"면 `nth-last-of-type(2n+1)`

---

### C3. border-collapse 없으면 테두리 2겹 ★★

```css
/* ❌ 기본값 separate: 셀 사이 테두리가 2겹으로 보임 */
table { border: 1px solid black; }
td    { border: 1px solid black; }
/* → 셀 사이에 2px처럼 보임 */

/* ✅ collapse: 테두리 합치기 */
table {
  border-collapse: collapse;
  border: 1px solid black;
}
td { border: 1px solid black; }
```

---

### C4. `visibility: hidden` vs `display: none` ★★★

```css
visibility: hidden;  /* 숨김 + 공간 유지 → 레이아웃 안 깨짐 */
display: none;       /* 숨김 + 공간도 사라짐 → 레이아웃 재배치 발생 */
```

```
visibility: hidden    display: none
[  ]  [  ]  [  ]      [A]  [C]  ← B 자리가 사라짐
 A    B(숨)  C          레이아웃 변경!
```

**토글 시**: `visibility`는 공간 유지 → 레이아웃 변화 없이 숨김/표시 가능

---

### C5. inline 요소에 width/height 적용 안 됨 ★★

```css
/* ❌ span, a, img(inline)에는 width/height/margin 상하 무효 */
span {
  width: 200px;  /* 효과 없음 */
  height: 50px;  /* 효과 없음 */
}

/* ✅ display 변경 후 적용 */
span {
  display: block;        /* 또는 */
  display: inline-block; /* 크기 설정 가능 + 인라인 흐름 유지 */
  width: 200px;
  height: 50px;
}
```

---

### C6. 후손 선택자 vs 자식 선택자 혼동 ★★

```css
/* 후손 선택자 (공백): 직접/간접 모든 하위 */
ol ul li { color: red; }  /* ol 아래 ul 아래 li (몇 단계든 OK) */

/* 자식 선택자 (>): 직접 자식만 */
tbody > tr { ... }   /* tbody의 직접 자식 tr만 */
tr > td:first-child { ... }  /* tr의 직접 첫 번째 td만 */
```

**시험에서 zebra stripe 자주 실수**
```css
/* ❌ 너무 범위 좁힘 */
tbody > tr:nth-child(odd) > td { background: #e3efff; }

/* ✅ tr에 배경 적용 (td가 투명하면 tr 배경 보임) */
tbody tr:nth-child(odd) { background-color: #e3efff; }
```

---

## HTML 에러

---

### H1. label의 for 속성 ≠ input의 name → id로 연결 ★★

```html
<!-- ❌ for와 name을 일치시키면 연결 안 됨 -->
<label for="stuName">성명</label>
<input type="text" name="stuName">   <!-- id가 없음 → label 클릭해도 포커스 안 감 -->

<!-- ✅ for와 id를 일치시켜야 연결됨 -->
<label for="sName">성명</label>
<input type="text" name="stuName" id="sName">
```

---

### H2. radio/checkbox → 같은 name으로 묶어야 그룹 동작 ★★

```html
<!-- ❌ name이 다르면 radio가 독립적으로 동작 → 여러 개 동시 선택 가능 -->
<input type="radio" name="lang1" value="C"> C
<input type="radio" name="lang2" value="Java"> Java

<!-- ✅ 같은 name으로 묶어야 하나만 선택 가능 -->
<input type="radio" name="stuLang" value="C"> C
<input type="radio" name="stuLang" value="Java"> Java
```

---

### H3. target="_blank" 없으면 현재 탭에서 열림 ★★

```html
<!-- 현재 탭에서 열림 (기본값 _self) -->
<a href="https://example.com">링크</a>

<!-- 새 탭에서 열림 -->
<a href="https://example.com" target="_blank">링크</a>

<!-- iframe 안에서 열림 -->
<a href="page.html" target="myFrame">링크</a>
<iframe name="myFrame"></iframe>
```

---

## 에러 요약 테이블

| 코드 | 에러 | 빈도 |
|------|------|------|
| E1 | `1 <= x < 2` 체이닝 비교 → 항상 true | ★★★ |
| E2 | `prompt()` 반환 = 문자열 → 형변환 필수 | ★★★★ |
| E3 | `var` 없이 선언 → 전역 변수 오염 | ★★★ |
| E4 | `<head>`에서 DOM 접근 → null 에러 | ★★★★ |
| E5 | `innerHTML` / `textContent` / `value` 혼동 | ★★★★ |
| E6 | `==` 느슨한 비교 함정 | ★★★ |
| E7 | `position` 없으면 `top`/`left`/`z-index` 무효 | ★★★★ |
| E8 | `transition`을 `:hover`에만 쓰면 역방향 없음 | ★★★★★ |
| E9 | `absolute` 자식 기준은 부모의 `position` | ★★★★ |
| E10 | 누적 변수를 지역 변수로 → 매번 초기화 | ★★★ |
| E11 | `str += ch` vs `str = ch + str` 방향 | ★★★ |
| E12 | `textContent` 숫자 연산 시 `Number()` 필요 | ★★★ |
| E13 | 정규식 `.` 이스케이프 미처리 | ★★ |
| E14 | `rowspan` 후 다음 행 `<td>` 개수 초과 | ★★★ |
| E15 | `for...in` vs `for...of` 혼동 | ★★★ |
| E16 | `img.width` 로딩 전 = 0 | ★★ |
| E17 | `style.float` 예약어 충돌 | ★ |
| C1 | `nth-child` vs `nth-of-type` 선택 실수 | ★★★ |
| C2 | `nth-child(odd)` vs `nth-last-of-type(2n+1)` 혼동 | ★★★ |
| C3 | `border-collapse` 없으면 테두리 2겹 | ★★ |
| C4 | `visibility:hidden` vs `display:none` 혼동 | ★★★ |
| C5 | inline 요소에 width/height 무효 | ★★ |
| C6 | 후손 선택자 vs 자식(`>`) 선택자 혼동 | ★★ |
| H1 | `label for` = `input id` (name 아님) | ★★ |
| H2 | radio 그룹 = 같은 `name` | ★★ |
| H3 | 새 탭 열기 = `target="_blank"` | ★★ |
