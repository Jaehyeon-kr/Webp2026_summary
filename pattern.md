# 자주 나오는 패턴 모음

> Ctrl+F 로 패턴명 검색 | 등장 횟수 기준으로 내림차순 정렬

---

## 1. toggle 패턴 ★★★★★

**정의**: 버튼 클릭마다 상태를 두 가지로 번갈아 전환

### 방법 A — 스타일 값으로 판단

```js
// visibility toggle (pre4/sol5)
if (el.style.visibility === "hidden") {
  el.style.visibility = "visible";
} else {
  el.style.visibility = "hidden";
}

// float toggle (final/sol4)
if (btn.style.float === "right") {
  btn.style.float = "none";
} else {
  btn.style.float = "right";
}
```

### 방법 B — id 존재 여부로 판단

```js
// 요소 없으면 생성, 있으면 삭제 (pre4/sol7)
let notice = document.getElementById("notice");
if (!notice) {
  let obj = document.createElement("div");
  obj.id = "notice";
  // ... 속성 설정 후
  document.body.insertBefore(obj, document.querySelector("p"));
} else {
  notice.remove();
}
```

### 방법 C — 커스텀 플래그 변수로 판단

```js
// 함수 객체에 플래그 저장 (final/sol2, sol3)
if (sol2.down != true) {
  // A 상태로 변경
  sol2.down = true;
} else {
  // B 상태로 변경
  sol2.down = false;
}
```

> **핵심**: 상태를 어디에 저장하느냐의 차이. 스타일값, id존재, 커스텀 플래그 중 택1

---

## 2. DOM 생성 → 설정 → 추가 패턴 ★★★★★

```js
// createElement → 속성 설정 → appendChild / insertBefore
let el = document.createElement("div");
el.id = "notice";
el.className = "counter";
el.textContent = "0";
el.innerHTML = "<strong>내용</strong>";
el.style.border = "red double 3px";

// 마지막에 추가
document.body.appendChild(el);
// 또는 특정 위치 앞에 삽입
parent.insertBefore(el, referenceNode);
```

**등장 파일**: pre4/sol4, sol7, sol8, final/sol5, sol6, sol7, pre3

---

## 3. transition + hover transform 패턴 ★★★★★

```css
/* 반드시: transition은 원래 상태에, transform은 :hover에 */
.box {
  transition: transform 0.5s ease;   /* 평소 */
}
.box:hover {
  transform: translateX(250px);       /* 변화 */
}
```

**변형 예시**

```css
/* hover 시 회전 (pre1/3_sol.html) */
div.child:hover {
  transform: rotate(-25deg);
  transition: transform 2s;
}

/* hover 시 날아가며 2바퀴 회전 (2024/1.html) */
div img:hover {
  transform: translateX(-100px) translateY(-250px) rotate(2turn);
}

/* wrapper:hover 시 내부 박스 이동 */
.wrapper:hover .box {
  transform: translateX(250px);
}
```

> `transition`을 `:hover` 안에 써도 동작하지만, hover 해제 시 역방향 애니메이션이 없어짐 → **반드시 원래 상태에 작성**

---

## 4. position: relative + absolute 겹침 패턴 ★★★★★

```css
/* 부모는 relative, 자식은 absolute → 자식이 부모 기준으로 절대 위치 */
.wrapper {
  position: relative;
  width: 300px;
  height: 80px;
}
.box {
  position: absolute;
  top: 0; left: 0;
  z-index: 1;
}
.text {
  position: absolute;
  top: 10px; left: 10px;
  z-index: 2;
}
```

```
┌─ .wrapper (relative) ──────┐
│  ┌── .text (absolute) ──┐  │
│  └──────────────────────┘  │
│  ┌── .box  (absolute) ──┐  │
│  └──────────────────────┘  │
└────────────────────────────┘
두 요소가 같은 공간에 겹침
```

**등장 파일**: mid5.html, 3_sol.html, exam/3.html, pre1/3_sol.html, 2024/2.html

---

## 5. object {} 카운터/빈도수 패턴 ★★★★

```js
// 키=항목, 값=횟수
let counter = {};
for (let item of list) {
  if (counter[item]) {
    counter[item]++;
  } else {
    counter[item] = 1;
  }
}
// 단축형
counter[item] = (counter[item] || 0) + 1;

// 결과 출력 (for...in으로 키 순회)
for (let key in counter) {
  console.log(key + ": " + counter[key]);
}
```

**등장 파일**: pre4/sol3(단어 빈도), hw3/quest9(문자 빈도)

---

## 6. split → 처리 → 결과 누적 패턴 ★★★★

```js
// 문자열 → 배열 → 각 요소 처리
let words = text.split(" ");    // 공백 기준 분리
let result = "";

for (let i = 0; i < words.length; i++) {
  result += words[i][0].toUpperCase();  // 각 단어 첫 글자
}
```

**변형**

```js
// 구두점 제거 후 분리 (hw3/quest8, quest9)
str = str.replace(/[,.\s]/g, "");   // 쉼표·마침표·공백 제거
str.split(" ")                       // 공백 기준 분리

// 역순 누적 (pre2/quest3)
for (let ch of str) {
  result = ch + result;  // 앞에 붙임 → 역순
}
```

**등장 파일**: hw3/quest7, quest8, pre2/quest3, quest5, pre4/sol3

---

## 7. setInterval + setTimeout 조합 패턴 ★★★★

```js
// N초 동안 반복 → 자동 정지
let timer = setInterval(() => {
  // 반복 동작
}, 100);  // 100ms 간격

setTimeout(() => {
  clearInterval(timer);
}, 3000);  // 3초 후 정지
```

**변형**

```js
// 카운트업 (final/sol5)
let timeUp = setInterval(() => {
  counterDiv.textContent = Number(counterDiv.textContent) + 1;
}, 100);
setTimeout(() => { clearInterval(timeUp); }, 3000);

// 높이 0→100% 애니메이션 (final/sol8)
let x = 0;
let overlay = setInterval(() => {
  x += 1 / 12.5;
  el.style.height = x + "%";
}, 1);
setTimeout(() => { clearInterval(overlay); }, 5000);

// 실시간 텍스트 추적 (final/sol3)
let tracking = setInterval(() => {
  mark.innerHTML = input.value;
}, 1);
```

---

## 8. while (true) + break 패턴 ★★★

```js
// 종료 조건이 입력에 따라 달라질 때
while (true) {
  let input = prompt("입력:");
  if (종료조건) {
    break;
  }
  // 처리
}

// Collatz (2024/4.html): 1이 될 때까지
while (num !== 1) {
  num = (num % 2 === 0) ? num / 2 : num * 3 + 1;
  count++;
}

// 양의 홀수만 처리 (hw3/quest6)
while (true) {
  if (number < 0) { break; }
  // 홀수면 출력, 짝수면 무시
  number = prompt("입력:");
}
```

---

## 9. Math.random() 정수 패턴 ★★★

```js
Math.floor(Math.random() * N)           // 0 ~ N-1
Math.floor(Math.random() * N) + 1       // 1 ~ N
Math.floor(Math.random() * (max-min+1)) + min  // min ~ max
```

```js
// 가위바위보 (hw3/quest4)
let random = Math.floor(Math.random() * 3) + 1;  // 1, 2, 3
if      (random === 1) computer = "가위";
else if (random === 2) computer = "바위";
else                   computer = "보";
```

**⚠️ 체이닝 비교 버그**
```js
// ❌ 항상 true: JS는 왼쪽부터 평가 → boolean < 2 → 항상 true
if (1 <= random < 2) { ... }

// ✅ 올바름
if (random >= 1 && random < 2) { ... }
```

---

## 10. rowspan / colspan 패턴 ★★★

```html
<!-- 세로 병합: rowspan → 다음 행에서 그 열 td 생략 -->
<tr>
  <td rowspan="2">병합 셀</td>
  <td>일반</td>
</tr>
<tr>
  <!-- rowspan 열 생략 -->
  <td>일반</td>
</tr>

<!-- 가로 병합: colspan → 해당 행에서 td 개수 감소 -->
<tr>
  <td colspan="2">2열 병합</td>
  <td>일반</td>
</tr>
```

**등장 파일**: pre1/1.html, mid4.html, 2_sol.html, 2024/0.html

---

## 11. nth-child / nth-of-type 선택자 패턴 ★★★

```css
/* zebra stripe (홀수 행 배경색) */
tbody > tr:nth-child(odd) { background-color: #e3efff; }
tbody > tr:nth-child(2n+1) { background-color: #e3efff; }  /* 동일 */

/* 특정 셀 색상 (대각선 등) */
tr:nth-child(3) td:nth-child(3) { background-color: black; }

/* 뒤에서 홀수 번째 li 빨간색 */
ol ul li:nth-last-of-type(2n+1) { color: red; }

/* 첫 번째 열은 제외 */
tbody > tr > td:first-child { background-color: white; }
```

**등장 파일**: pre1/2_sol.html, mid2.html, mid4.html, 1_sol.html, 2_sol.html

---

## 12. 누적 곱 / 누적 합 패턴 ★★★

```js
// 팩토리얼 (누적 곱) (2024/5.html)
let last = 1;
for (let i = 1; i <= n; i++) {
  last = last * i;     // last가 i!이 됨
  arr.push(last);
}

// 평균 (누적 합) (2024/3.html)
let sum = 0;
for (let i = 0; i < arr.length; i++) {
  sum += arr[i];
}
return sum / arr.length;

// 초→분/초 변환 (hw3/quest0)
let min = Math.floor(time / 60);
let sec = time % 60;
```

---

## 13. 중복 제거 패턴 ★★★

```js
// nested for로 dedup (hw3/quest8)
let result = [];
for (let i = 0; i < list.length; i++) {
  let found = false;
  for (let j = 0; j < result.length; j++) {
    if (list[i] === result[j]) { found = true; break; }
  }
  if (!found) result.push(list[i]);
}
result.sort();
```

```
[흐름]
list 각 요소 → result에 이미 있는지 검사
  있으면 → skip (found=true, break)
  없으면 → push
```

---

## 14. 정규식 replace 패턴 ★★★

```js
// 특정 문자 제거
str.replace(/'/g, "")          // 아포스트로피 제거
str.replace(/,/g, "")          // 쉼표 제거
str.replace(/\./g, "")         // 마침표 제거 (이스케이프 필요)

// 문자 클래스로 여러 개 동시 제거
str.replace(/[,.\s]/g, "")     // 쉼표·마침표·공백 제거
str.replace(/[\,\.\;\s]/g, "") // 쉼표·마침표·세미콜론·공백 제거

// g 플래그: 전체 치환 (없으면 첫 번째만)
"aabaa".replace(/a/g, "x")    // "xxbxx"
"aabaa".replace(/a/, "x")     // "xabaa"
```

**등장 파일**: hw3/quest2, quest8, quest9

---

## 15. keydown 방향키 이동 패턴 ★★

```js
// 전역 변수로 현재 위치 유지
let xAxis = 0, yAxis = 0;

function keyProcess(event) {
  switch (event.keyCode) {
    case 37: xAxis -= 1; break;  // ←
    case 38: yAxis -= 1; break;  // ↑ (위 = top 감소)
    case 39: xAxis += 1; break;  // →
    case 40: yAxis += 1; break;  // ↓
  }
  img.style.left = xAxis + "px";
  img.style.top  = yAxis + "px";
}
document.addEventListener("keydown", keyProcess);
```

```
[keyCode]
37 ←   38 ↑
39 →   40 ↓
```

**등장 파일**: pre4/sol9

---

## 16. % 모듈로 순환 패턴 ★★

```js
// 배열 인덱스를 순환시킬 때
let colors = ["red", "orange", "yellow", "green", "blue", "navy", "purple"];
let idx = 0;
// 클릭할 때마다
li.style.color = colors[idx % colors.length];
idx++;
// idx가 7이 되면 % 7 = 0으로 처음 색상으로 돌아감
```

**등장 파일**: pre4/sol6

---

## 17. 클로저로 외부 변수 캡처 패턴 ★★

```js
// 이벤트 리스너가 외부에서 생성된 요소를 참조
button.addEventListener("click", () => {
  const li = document.createElement("li");
  const deleteBtn = document.createElement("button");
  deleteBtn.textContent = "Delete";
  li.appendChild(deleteBtn);
  list.appendChild(li);

  deleteBtn.addEventListener("click", () => {
    list.removeChild(li);  // ← 클로저: 위의 li를 캡처
  });
});
// 각 버튼이 자신의 li만 삭제하는 이유: 클로저 덕분에 li 독립 보관
```

**등장 파일**: pre3/pre3.html, final/sol5, pre4/sol9

---

## 18. 문자열 역순 패턴 ★★

```js
// 방법 A: for...of + 앞에 붙이기 (pre2/quest3)
let result = "";
for (let ch of str) {
  result = ch + result;
}

// 방법 B: 인덱스 역순 (hw3/quest5, final/sol1)
let result = "";
for (let i = str.length - 1; i >= 0; i--) {
  result += str[i];
}

// 방법 C: 내장 메서드 (참고)
str.split("").reverse().join("")
```

---

## 19. border-radius 원형 패턴 ★★

```css
/* 정사각형 요소에 적용 시 완전한 원 */
.circle {
  width: 50px;
  height: 50px;
  border-radius: 100%;   /* 또는 50% */
  border: 5px solid black;
}
```

**등장 파일**: 2024/1.html (공)

---

## 20. 3면만 border (골대 패턴) ★

```css
/* 4면 중 특정 면만 테두리 */
.goalpost {
  border-top-style: solid;
  border-top-width: 10px;
  border-left-style: solid;
  border-right-style: solid;
  /* border-bottom 없음 → 아래 열린 ∩ 모양 */
}
```

```
──────────────────  border-top
│                │
│                │  border-left, border-right
  (열린 바닥)
```

---

## 패턴 빈도 요약

| 순위 | 패턴 | 등장 빈도 |
|------|------|-----------|
| 1 | toggle (스타일/id/플래그) | ★★★★★ |
| 2 | DOM 생성→설정→추가 | ★★★★★ |
| 3 | transition + hover transform | ★★★★★ |
| 4 | position relative + absolute | ★★★★★ |
| 5 | object {} 빈도수 카운터 | ★★★★ |
| 6 | split → 처리 → 누적 | ★★★★ |
| 7 | setInterval + setTimeout | ★★★★ |
| 8 | while(true) + break | ★★★ |
| 9 | Math.random() 정수 | ★★★ |
| 10 | rowspan / colspan | ★★★ |
| 11 | nth-child 선택자 | ★★★ |
| 12 | 누적 곱/합 | ★★★ |
| 13 | 중복 제거 (nested for) | ★★★ |
| 14 | 정규식 replace | ★★★ |
| 15 | keydown 방향키 이동 | ★★ |
| 16 | % 모듈로 순환 | ★★ |
| 17 | 클로저 캡처 | ★★ |
| 18 | 문자열 역순 | ★★ |
| 19 | border-radius 원형 | ★★ |
| 20 | 3면 border | ★ |
