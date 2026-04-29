# JavaScript 기능 정리

> Ctrl+F 로 메서드명, 개념, 이벤트명 검색

---

## 변수 선언

```js
var x = 10;   // 함수 스코프, 재선언 가능 (구식)
let y = 20;   // 블록 스코프, 재선언 불가
const z = 30; // 블록 스코프, 재할당 불가
```

---

## Falsy 값 (조건문에서 false로 처리되는 값)

```js
false, undefined, null, NaN, 0, ""
// 나머지는 모두 truthy (빈 배열 [], 빈 객체 {} 포함)
```

---

## 객체 (Object)

### 선언 / 접근

```js
// 객체 선언 (리터럴)
let person = {
  name: "Kim",
  age: 20,
  greet: function() {       // 메서드
    return "Hello " + this.name;
  }
};

// 프로퍼티 접근
person.name           // 점 표기법
person["name"]        // 괄호 표기법 (변수로 접근 가능)
person.greet()        // 메서드 호출

// 중첩 객체
let data = { user: { name: "Kim", score: 90 } };
data.user.name        // "Kim"
data["user"]["score"] // 90

// 프로퍼티 추가/변경
person.email = "kim@test.com";
person.age = 21;
```

---

## 배열 (Array)

### 선언 / 인덱싱

```js
let arr = [10, 20, 30];
arr[0]        // 10 (0부터 시작)
arr.length    // 3
```

### 배열 메서드

| 메서드 | 파라미터 | 반환값 | 설명 |
|--------|----------|--------|------|
| `.push(val)` | 추가할 값 | 새 length | **끝에** 요소 추가 |
| `.pop()` | 없음 | 제거된 값 | **끝** 요소 제거 |
| `.unshift(val)` | 추가할 값 | 새 length | **앞에** 요소 추가 |
| `.shift()` | 없음 | 제거된 값 | **앞** 요소 제거 |
| `.concat(arr2)` | 합칠 배열 | 새 배열 | 두 배열 합치기 (원본 불변) |
| `.indexOf(val)` | 찾을 값 | 인덱스 (없으면 -1) | 값의 위치 찾기 |
| `.sort()` | 없음 (또는 비교 함수) | 정렬된 배열 | 기본: 문자열 기준 정렬 |
| `.reverse()` | 없음 | 뒤집힌 배열 | 순서 뒤집기 |
| `.slice(start, end)` | 시작 인덱스, 끝 인덱스(미포함) | 새 배열 | 일부 추출 (원본 불변) |
| `.splice(start, count, ...items)` | 시작, 개수, 추가할 값들 | 제거된 요소 배열 | 요소 제거/삽입 (원본 변경) |
| `.forEach(fn)` | 콜백 함수 | undefined | 각 요소에 함수 실행 |

```js
let arr = [3, 1, 2];
arr.push(4);         // [3, 1, 2, 4]
arr.pop();           // [3, 1, 2], 반환값: 4
arr.unshift(0);      // [0, 3, 1, 2]
arr.shift();         // [3, 1, 2], 반환값: 0
arr.concat([4,5]);   // [3, 1, 2, 4, 5] (원본 그대로)
arr.indexOf(1);      // 1
arr.sort();          // [1, 2, 3]
arr.reverse();       // [3, 2, 1]
arr.slice(0, 2);     // [3, 2] (원본 그대로)
arr.splice(1, 1);    // [3, 1], 반환값: [2]

// forEach
arr.forEach(function(el) { console.log(el); });
arr.forEach(el => console.log(el)); // 화살표 함수
```

---

## 함수 (Function)

### 함수 선언 방법 비교

```js
// 1. 함수 선언식 (호이스팅 됨 → 선언 전에 호출 가능)
function add(a, b) {
  return a + b;
}

// 2. 함수 표현식 (호이스팅 안 됨)
let add = function(a, b) {
  return a + b;
};

// 3. 화살표 함수 (this 없음, 간결)
let add = (a, b) => a + b;            // 한 줄이면 return 생략 가능
let add = (a, b) => { return a + b; }; // 중괄호 있으면 return 명시
let greet = name => "Hello " + name;   // 파라미터 1개면 괄호 생략 가능

// 4. 중첩 함수
function outer() {
  function inner(x, y) { return x + y; }
  console.log(inner(1, 2));
}
```

### 기본값 파라미터 (Default Parameter)

```js
function greet(name = "Guest") {
  return "Hello " + name;
}
greet();        // "Hello Guest"
greet("Kim");   // "Hello Kim"
```

### 콜백 함수 (Callback)

```js
// 콜백: 함수를 파라미터로 전달
function doSomething(callback) {
  callback();
}
doSomething(function() { console.log("done"); });

// setInterval에 콜백 전달
let timer = setInterval(function() {
  console.log("반복");
}, 1000); // 1초마다 실행
```

---

## 조건문

### if / else if / else

```js
if (x > 0) {
  console.log("양수");
} else if (x < 0) {
  console.log("음수");
} else {
  console.log("0");
}
```

### 삼항 연산자 (Ternary)

```js
// 조건 ? 참일 때 값 : 거짓일 때 값
let result = (x > 0) ? "양수" : "음수";
```

### switch / case

```js
switch (x) {
  case 1:
    console.log("일");
    break;           // break 없으면 다음 case로 fall-through
  case 2:
    console.log("이");
    break;
  default:
    console.log("기타");
}
```

---

## 반복문

### for

```js
for (let i = 0; i < 10; i++) {
  console.log(i); // 0, 1, ..., 9
}
```

### while

```js
let i = 0;
while (i < 10) {
  console.log(i);
  i++;
}
```

### do-while (최소 1번 실행)

```js
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 10);
```

### for...of (배열/이터러블 순회)

```js
let arr = [10, 20, 30];
for (let val of arr) {
  console.log(val); // 10, 20, 30
}

// HTMLCollection / NodeList도 순회 가능
for (let li of document.getElementsByTagName("li")) {
  li.style.color = "red";
}
```

### for...in (객체 키 순회)

```js
let freq = { apple: 3, banana: 1 };
for (let key in freq) {
  console.log(key, freq[key]); // apple 3, banana 1
}
```

### forEach (배열 메서드)

```js
[10, 20, 30].forEach(function(val) { console.log(val); });
[10, 20, 30].forEach(val => console.log(val));
```

### break / continue

```js
for (let i = 0; i < 10; i++) {
  if (i === 5) break;    // 루프 완전 종료
  if (i % 2 === 0) continue; // 현재 반복만 건너뜀
}
```

---

## DOM 요소 선택

| 메서드 | 파라미터 | 반환 | 예시 |
|--------|----------|------|------|
| `getElementById(id)` | id 문자열 | 단일 DOM 객체 | `document.getElementById("txt")` |
| `getElementsByClassName(cls)` | 클래스명 | HTMLCollection | `document.getElementsByClassName("counter")` |
| `getElementsByName(name)` | name 속성값 | NodeList | `document.getElementsByName("title")[0]` |
| `getElementsByTagName(tag)` | 태그명 | HTMLCollection | `document.getElementsByTagName("input")` |
| `querySelector(selector)` | CSS 선택자 | 단일 DOM 객체 (첫 번째) | `document.querySelector("ul li")` |
| `querySelectorAll(selector)` | CSS 선택자 | NodeList | `document.querySelectorAll("#intro li")` |
| `document.head` | - | head 객체 | - |
| `document.body` | - | body 객체 | - |

```js
let el = document.getElementById("txt");              // 단일
let lis = document.querySelectorAll("ul li");         // 여러 개 → NodeList
let inputs = document.getElementsByTagName("input");  // HTMLCollection
let obj = document.getElementsByTagName("a")[0];      // 첫 번째 a 태그
```

**HTMLCollection / NodeList**: 배열처럼 `[0]`으로 접근, `.length`로 길이, `for...of`로 순회

---

## DOM 요소 내용/속성 조작

### 내용 수정

| 속성 | 설명 | 예시 |
|------|------|------|
| `.outerHTML` | 해당 요소 자체(태그 포함) HTML | `link.outerHTML` |
| `.innerHTML` | 내부 HTML 문자열 (HTML 파싱됨) | `div.innerHTML = "<b>텍스트</b>"` |
| `.textContent` | 내부 텍스트만 (XSS 안전) | `div.textContent = "0"` |
| `.value` | input 요소의 현재 값 (읽기/쓰기) | `input.value = "hello"` |

### 속성 수정

| 속성 | 설명 |
|------|------|
| `.id` | id 속성 | `obj.id = "notice"` |
| `.className` | class 속성 | `div.className = "counter"` |
| `.src` | img/script src | `img.src = "./logo.png"` |
| `.href` | a 태그 href | `link[0].href = "http://..."` |
| `.target` | a 태그 target | `link[0].target = "_blank"` |
| `.width` / `.height` | img 크기 | `img.width` |
| `.tagName` | 태그 이름 (대문자) | `obj.tagName` → `"DIV"` |
| `.childElementCount` | 자식 요소 수 | `obj.childElementCount` |

---

## 스타일 조작

```js
// style.속성명 (카멜케이스: background-color → backgroundColor)
element.style.color = "red";
element.style.backgroundColor = "beige";
element.style.fontSize = drag.value + "px";
element.style.visibility = "hidden";     // hidden | visible
element.style.float = "right";           // none | left | right
element.style.position = "relative";
element.style.left = xAxis + "px";
element.style.top = yAxis + "px";
element.style.height = x + "%";
element.style.border = "red double 3px";
element.style.zIndex = "999";
```

---

## DOM 요소 생성 / 추가 / 삭제

| 메서드 | 파라미터 | 반환 | 설명 |
|--------|----------|------|------|
| `document.createElement(tag)` | 태그명 문자열 | 새 DOM 객체 | 요소 생성 |
| `parent.appendChild(element)` | 추가할 요소 | 추가된 요소 | 부모 마지막 자식으로 추가 |
| `parent.insertBefore(new, existing)` | 새 요소, 기준 요소 | 추가된 요소 | existing 앞에 new 삽입 |
| `parent.removeChild(child)` | 제거할 자식 요소 | 제거된 요소 | 부모에서 자식 제거 |
| `element.remove()` | 없음 | undefined | 요소 자체 삭제 |

```js
// 생성 → 속성 설정 → 추가
let div = document.createElement("div");
div.id = "notice";
div.innerHTML = "<strong>Assignment #5</strong>";
div.style.border = "red double 3px";

let body = document.getElementsByTagName("body")[0];
body.insertBefore(div, document.getElementsByTagName("p")[0]); // p 앞에 삽입
document.body.appendChild(div); // body 마지막에 추가

// 삭제
div.remove();
body.removeChild(document.getElementById("notice"));
```

---

## 이벤트

### 이벤트 등록 방법

```js
// 방법 1: HTML 속성 (비권장)
// <a onclick="addObj()">My link</a>

// 방법 2: DOM 속성으로 등록
element.onclick = myFunction;
window.onload = function() { /* 페이지 로딩 완료 후 실행 */ };

// 방법 3: addEventListener (권장)
element.addEventListener("click", myFunction);
element.addEventListener("keydown", keyProcess);

// 주의: DOM 트리가 만들어지기 전에 등록하면 에러!
// 해결 1: <script>를 </body> 직전에 위치
// 해결 2: window.onload 안에서 등록
window.onload = function() {
  document.getElementById("btn").addEventListener("click", myFunction);
};
```

### 이벤트 종류

| 이벤트 | 발생 시점 | 사용 파일 |
|--------|-----------|-----------|
| `click` | 마우스 클릭 | pre4, final |
| `dblclick` | 마우스 더블클릭 | - |
| `mouseover` | 마우스가 요소 위에 올라왔을 때 | - |
| `mouseleave` | 마우스가 요소를 벗어났을 때 | - |
| `keydown` | 키를 눌렀을 때 | pre4/sol9 |
| `keyup` | 누른 키를 놓았을 때 | 5강 예제 |
| `change` | 값이 변경되고 포커스를 잃었을 때 (radio, checkbox) | - |
| `focus` | 포커스를 획득했을 때 | - |
| `load` | 로딩이 완료되었을 때 | final |
| `submit` | 폼이 전송될 때 | - |
| `reset` | reset 버튼 클릭 시 | - |
| `resize` | 윈도우 크기 변경 시 | - |

### 이벤트 객체 (event / e / evt)

이벤트 핸들러 함수에 자동으로 전달되는 객체. 이벤트 관련 정보 포함.

| 프로퍼티/메서드 | 설명 |
|----------------|------|
| `e.type` | 이벤트 종류 문자열 (`"click"`, `"load"` 등) |
| `e.target` | 이벤트를 발생시킨 DOM 객체 |
| `e.target.value` | 이벤트 발생 요소의 value (input 값 읽기) |
| `e.currentTarget` | 현재 이벤트 리스너가 붙은 DOM 객체 |
| `e.defaultPrevented` | 기본 동작이 취소되었는지 (true/false) |
| `e.preventDefault()` | 기본 동작 취소 (링크 이동, 폼 제출 등) |

**KeyboardEvent** (keydown/keyup 이벤트 객체)
| 프로퍼티 | 설명 |
|----------|------|
| `e.key` | 눌린 키의 문자열 (`"ArrowLeft"`, `"Enter"` 등) |
| `e.keyCode` | 눌린 키의 숫자 코드 (구식, 37=←, 38=↑, 39=→, 40=↓) |
| `e.ctrlKey` | Ctrl 키 눌린 상태면 true |
| `e.altKey` | Alt 키 눌린 상태면 true |

```js
// event.target 활용
let setTitle = (event) => {
  document.getElementsByClassName("header")[0].innerHTML = event.target.value;
};
document.getElementsByName("title")[0].addEventListener("keyup", setTitle);
```

### keydown 이벤트 + 방향키

```js
function keyProcess(event) {
  switch (event.keyCode) {
    case 37: xAxis -= 1; break; // ← 왼쪽
    case 38: yAxis -= 1; break; // ↑ 위
    case 39: xAxis += 1; break; // → 오른쪽
    case 40: yAxis += 1; break; // ↓ 아래
  }
  img.style.left = xAxis + "px";
  img.style.top  = yAxis + "px";
}
document.addEventListener("keydown", keyProcess);
```
- 사용 파일: [pre4.html](pre4/pre4.html) sol9

---

## 타이머

### setInterval — 반복 실행

```js
// setInterval(콜백함수, 밀리초) → 타이머 ID 반환
let timer = setInterval(() => {
  // N ms 마다 반복 실행
}, 100); // 100ms = 0.1초

// 정지: clearInterval에 타이머 ID 전달
clearInterval(timer);
```

### setTimeout — 지연 후 1회 실행

```js
// setTimeout(콜백함수, 밀리초) → N ms 후 1회만 실행
setTimeout(() => {
  clearInterval(timer); // 보통 타이머 정지에 활용
}, 3000); // 3초 후
```

### 조합 패턴 (일정 시간 후 자동 정지)

```js
// 100ms 간격 카운트업, 3초 후 정지 (final/sol5)
let timeUp = setInterval(() => {
  counterDiv.textContent = Number(counterDiv.textContent) + 1;
}, 100);
setTimeout(() => {
  clearInterval(timeUp);
}, 3000);
```

### 오버레이 높이 애니메이션 (final/sol8)

```js
// 5초 동안 height 0% → 100%로 상승 (1ms 간격, 1/12.5씩 증가)
let x = 0;
let overlay = setInterval(() => {
  x = x + 1/12.5;
  whiteOverlay.style.height = x + "%";
}, 1);
setTimeout(() => {
  clearInterval(overlay);
}, 5000);
```

---

## 문자열 메서드

| 메서드/속성 | 파라미터 | 반환값 | 설명 |
|------------|----------|--------|------|
| `.length` | 없음 | 숫자 | 문자열 길이 |
| `.toUpperCase()` | 없음 | 새 문자열 | 대문자 변환 |
| `.toLowerCase()` | 없음 | 새 문자열 | 소문자 변환 |
| `.split(sep)` | 구분자 문자열 | 배열 | 구분자로 나눠 배열 반환 |
| `.indexOf(str)` | 찾을 문자열 | 인덱스 (없으면 -1) | 위치 찾기 |
| `.slice(start, end)` | 시작, 끝(미포함) | 새 문자열 | 부분 추출 |
| `[i]` | 인덱스 | 문자 1개 | 특정 위치 문자 |

```js
// 문자열 역순 (for 루프, final/sol1)
let rev = "";
for (let i = txt.length; i > 0; i--) {
  rev += txt[i-1];
}

// 문자열 역순 (for...of, pre2/quest3)
function myReverse(str) {
  let result = "";
  for (let ch of str) {
    result = ch + result; // 앞에 추가
  }
  return result;
}

// 단어 분리
"a b c".split(" ")   // ["a", "b", "c"]
"hello".toUpperCase() // "HELLO"
"HELLO"[1]           // "E"
```

---

## 수학 / 형변환

| 메서드/연산 | 파라미터 | 반환값 | 설명 |
|------------|----------|--------|------|
| `Number(val)` | 문자열/boolean | 숫자 | 문자열 → 숫자 변환 |
| `String(val)` | 숫자/boolean | 문자열 | 숫자 → 문자열 변환 |
| `parseInt(str)` | 문자열 | 정수 | 정수로 변환 |
| `parseFloat(str)` | 문자열 | 실수 | 실수로 변환 |
| `Math.sqrt(x)` | 숫자 | 숫자 | 제곱근 |
| `Math.pow(x, n)` | 밑, 지수 | 숫자 | x의 n제곱 |
| `Math.floor(x)` | 숫자 | 정수 | 내림 |
| `Math.ceil(x)` | 숫자 | 정수 | 올림 |
| `Math.round(x)` | 숫자 | 정수 | 반올림 |
| `Math.abs(x)` | 숫자 | 숫자 | 절댓값 |
| `Math.random()` | 없음 | 0~1 사이 실수 | 난수 |
| `% (모듈로)` | - | 나머지 | 나머지 연산 (순환에 사용) |

```js
// 두 점 사이 거리 (pre2/quest1)
function getDist(x1, y1, x2, y2) {
  return Math.sqrt(Math.pow(x1-x2, 2) + Math.pow(y1-y2, 2));
}

Number("42")    // 42
Number("42px")  // NaN
String(42)      // "42"
```

---

## 입출력

| 메서드 | 파라미터 | 반환값 | 설명 |
|--------|----------|--------|------|
| `prompt("메시지")` | 메시지 문자열 | 입력 문자열 (취소 시 null) | 사용자 입력 다이얼로그 |
| `alert("메시지")` | 메시지 문자열 | undefined | 알림 다이얼로그 |
| `confirm("메시지")` | 메시지 문자열 | true/false | 확인/취소 다이얼로그 |
| `console.log(값)` | 출력할 값 | undefined | 콘솔 출력 (디버깅) |

---

## 조건 / 토글 패턴

```js
// 상태 토글 (flag 패턴, final/sol2)
if (sol2.down != true) {
  btts.remove();
  document.body.appendChild(btts2);
  sol2.down = true;
} else {
  btts.remove();
  document.body.insertBefore(btts2, label);
  sol2.down = false;
}

// 스타일 값으로 토글 (pre4/sol5)
if (el.style.visibility == "hidden") {
  el.style.visibility = "visible";
} else {
  el.style.visibility = "hidden";
}

// 요소 존재 여부로 토글 (pre4/sol7)
let notice = document.getElementById("notice");
if (!notice) {
  // 없으면 생성
} else {
  // 있으면 삭제
  notice.remove();
}
```

---

## 실시간 추적 패턴 (final/sol3)

```js
// setInterval로 input 값을 실시간 mark에 반영
let tracking;
if (sol3.now != true) {
  tracking = setInterval(() => {
    mark.innerHTML = txt.value;
  }, 1); // 1ms 간격
  sol3.now = true;
} else {
  clearInterval(tracking);
  sol3.now = false;
}
```

---

## 전체 패턴 예시 모음

### 카운터 생성 + 자동 정지 (final/sol5)
```js
const counterDiv = document.createElement("div");
counterDiv.textContent = "0";
counterDiv.className = "counter";
document.getElementById("list").appendChild(counterDiv);

let timeUp = setInterval(() => {
  counterDiv.textContent = Number(counterDiv.textContent) + 1;
}, 100);
setTimeout(() => { clearInterval(timeUp); }, 3000);
```

### range 슬라이더로 폰트 크기 조절 (final/sol6)
```js
const controller = document.createElement("div");
controller.innerHTML = '<label>폰트 크기: <input type="range" id="fontSizeSlider"></label>';
document.body.appendChild(controller);

let drag = document.getElementById("fontSizeSlider");
drag.min = "10"; drag.max = "50"; drag.value = "16";

setInterval(() => {
  document.getElementById("txt").style.fontSize = drag.value + "px";
}, 1);
```

### div 생성/삭제 토글 (pre4/sol7)
```js
function sol7() {
  let notice = document.getElementById("notice");
  if (!notice) {
    let obj = document.createElement("div");
    obj.id = "notice";
    obj.style.border = "red double 3px";
    obj.innerHTML = "<strong>Assignment #5</strong>";
    let body = document.getElementsByTagName("body")[0];
    body.insertBefore(obj, document.getElementsByTagName("p")[0]);
  } else {
    document.getElementsByTagName("body")[0].removeChild(notice);
  }
}
```

### 단어 빈도 계산 (pre4/sol3)
```js
let lst = text.split(" ");
let freq = {};
for (let word of lst) {
  if (freq[word] == null) freq[word] = 0;
  freq[word] += 1;
}
// 1번만 등장한 단어만 출력
for (let k in freq) {
  if (freq[k] == 1) answer += k + " ";
}
```

### 색상 순환 (pre4/sol6)
```js
var color = ["red","orange","yellow","green","blue","navy","purple"];
var idx = 0;
function sol6() {
  for (let li of document.getElementsByTagName("li")) {
    li.style.color = color[idx % 7];
  }
  idx++;
}
```

---

## 솔루션 해법 해설

> 각 과제 솔루션이 **왜 그렇게 짜여졌는지** 의도와 핵심 기법 설명

---

### pre1 — HTML/CSS 과제 (JS 없음)

pre1은 JS 없이 HTML 구조와 CSS만 사용하는 과제. 솔루션 해설은 [html.md](html.md) 참고.

| 파일 | 내용 | 상태 |
|------|------|------|
| pre1/1.html | 테이블 구조 (colspan/rowspan + 인라인 스타일만 허용) | 원본이 정답 |
| pre1/2.html | 5×5 테이블 CSS (대각선 셀 검은색) | → 2_sol.html |
| pre1/3.html | 절대위치 + z-index + hover 회전 | → 3_sol.html |

---

### pre2 — JS 함수 기초

**화면 구조**: `<body>`에 내용 없음. 모든 동작이 `prompt` → `console.log`로만 출력.

---

#### pre2/quest1 — 두 점 사이 거리

```js
function quest1() {
  var a1 = prompt("첫 번째 점의 x좌표");
  var b1 = prompt("첫 번째 점의 y좌표");
  var a2 = prompt("두 번째 점의 x좌표");
  var b2 = prompt("두 번째 점의 y좌표");

  function getDist(x1, y1, x2, y2) {
    return Math.sqrt(Math.pow(x1-x2, 2) + Math.pow(y1-y2, 2));
  }
  console.log(getDist(a1, b1, a2, b2));
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `getDist`를 내부 함수로 정의 | quest1 안에서만 쓰이는 함수 → 스코프 제한. 전역 오염 방지 |
| `Math.sqrt(Math.pow(...) + Math.pow(...))` | 거리 공식: `√((x1-x2)² + (y1-y2)²)` |
| `prompt` 결과를 Number 변환 안 함 | `Math.pow`에 문자열 넣으면 JS가 자동 형변환 → 동작은 하지만, 엄밀히는 `Number(a1)` 해줘야 정확 |

```
[실행 흐름]
prompt → prompt → prompt → prompt
           ↓
     getDist(a1,b1,a2,b2) 호출
           ↓
     console.log 결과 출력
```

---

#### pre2/quest2 — 문자열 대문자 변환

```js
function quest2(str) {
  console.log(str.toUpperCase());
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| 파라미터로 `str` 받음 | 다른 quest들은 prompt로 입력받지만, quest2는 외부에서 문자열 전달 방식 |
| `.toUpperCase()` | 문자열 메서드 → 원본 불변, 새 대문자 문자열 반환 |

---

#### pre2/quest3 — 문자열 역순

```js
function quest3() {
  let temp = prompt("문자열을 입력하세요.");

  function myReverse(temp) {
    let str = "";
    for (let i of temp) {
      str = i + str;  // 현재 문자를 str 앞에 붙임
    }
    return str;
  }
  console.log(myReverse(temp));
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `str = i + str` (앞에 추가) | 뒤에서 앞으로 뒤집는 핵심 트릭. `str += i`면 그냥 정방향 |
| `for...of` 사용 | 문자열은 이터러블 → `for...of`로 문자 하나씩 순회 가능 |

```
[동작 예시] "abc" 역순
i='a': str = 'a' + '' = 'a'
i='b': str = 'b' + 'a' = 'ba'
i='c': str = 'c' + 'ba' = 'cba'  ← 완성
```

---

#### pre2/quest4 — 숫자 각 자리 합계

```js
function quest4() {
  let temp = prompt("숫자를 입력하세요.").split("");

  function myReverse(temp) {  // 이름이 myReverse지만 실제로는 각 자리 합계
    let sum = 0;
    temp.forEach(element => {
      sum += Number(element);
    });
    return sum;
  }
  console.log(myReverse(temp));
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `.split("")` | 빈 문자열로 split → 각 문자(숫자 자리)를 배열 요소로 분리. `"123".split("") → ["1","2","3"]` |
| `Number(element)` | split 결과는 문자열 → 숫자로 변환 후 합산. 안 하면 `"1"+"2"+"3" = "123"` (문자열 연결) |
| `forEach` 사용 | 배열의 각 요소에 같은 연산 적용 → forEach가 for보다 간결 |

```
[동작 예시] "123" 입력
split("") → ["1", "2", "3"]
forEach: sum = 0+1+2+3 = 6
```

---

#### pre2/quest5 — 각 단어 첫 글자 대문자

```js
function quest5() {
  let temp = prompt("문자열을 입력하세요.").split(" ");

  function myReverse(temp) {
    let sum = "";
    temp.forEach(element => {
      sum += element[0].toUpperCase();
    });
    return sum;
  }
  console.log(myReverse(temp));
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `.split(" ")` | 공백으로 split → 단어 배열. `"hello world".split(" ") → ["hello","world"]` |
| `element[0]` | 배열 인덱스로 문자열 첫 글자 접근. `"hello"[0] → "h"` |
| `.toUpperCase()` | 첫 글자만 대문자로 변환 |
| `sum +=` (누적) | 각 단어 첫 글자들을 이어붙여 결과 문자열 생성 |

```
[동작 예시] "hello world foo" 입력
split(" ") → ["hello", "world", "foo"]
forEach: sum = "H" + "W" + "F" = "HWF"
```

---

### pre4 — JS DOM 조작 (9문제)

**화면 구조**
```
[Number 1: ____]  ← id="num1"
[Number 2: ____]  ← id="num2"
[Text:     ____]  ← id="txt"

• #1  • #2  • #3  • #4  • #5
• #6  • #7  • #8  • #9
            ← 각 li 클릭 시 해당 sol() 호출

[answer div]  ← 결과 출력 영역, id="answer"
```

---

#### pre4/sol1 — 두 수 덧셈

```js
function sol1() {
  let num1 = document.getElementById("num1").value;
  let num2 = document.getElementById("num2").value;
  var sum = Number(num1) + Number(num2);
  document.getElementById("txt").value = sum;
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `Number(num1)` | `.value`는 항상 **문자열** 반환. 변환 안 하면 `"3"+"5" = "35"` (문자열 연결) |
| 결과를 `txt.value`에 저장 | input 요소의 값은 `.value`로 읽고 씀 (`.innerHTML` 아님) |

---

#### pre4/sol2 — 두 수 비교

```js
function sol2() {
  let num1 = Number(document.getElementById("num1").value);
  let num2 = Number(document.getElementById("num2").value);
  let winner = (num1 > num2) ? num1 : num2;
  document.getElementById("txt").value = winner;
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `.value` 읽을 때 바로 `Number()` 변환 | sol1은 더할 때 변환, sol2는 비교 전에 변환. 비교 연산(`>`)도 문자열이면 사전순 비교로 틀림 (`"9" > "10"` → true) |

---

#### pre4/sol3 — 중복 없는 단어 추출

```js
function sol3() {
  let lst = document.getElementById("txt").value.split(" ");
  let str = {};  // 빈 객체를 빈도수 저장용으로 사용

  for (let i of lst) {
    if (str[i] == null) str[i] = 0;
    str[i] += 1;
  }

  let answer = "";
  for (let i in str) {
    if (str[i] == 1) answer += String(i) + " ";
  }
  document.getElementById("answer").innerHTML = answer;
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| 객체 `{}`를 빈도수 맵으로 사용 | JS에 Map 있지만, 객체도 `obj[key]`로 딕셔너리처럼 사용 가능. 가장 간단한 방법 |
| `str[i] == null` 체크 | 처음 등장하는 단어는 객체에 key가 없어 `undefined` → null과 `==` 비교 시 true (느슨한 비교) |
| `for...of`로 배열 순회 후 `for...in`으로 객체 순회 | 배열 → `for...of` (값), 객체 키 → `for...in` (키) |

```
[동작 예시] "a b a c" 입력
split → ["a","b","a","c"]
빈도: { a:2, b:1, c:1 }
for...in: b==1 → answer="b ", c==1 → answer="b c "
```

---

#### pre4/sol4 — 텍스트 N번 반복 출력

```js
function sol4() {
  let count = Number(document.getElementById("num1").value);
  let text = document.getElementById("txt").value;

  let p = document.createElement("p");
  for (let i = 0; i < count; i++) {
    p.innerHTML += text + "<br>";
  }
  document.getElementById("answer").appendChild(p);
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `p` 하나 만들어서 루프 안에서 `innerHTML +=` | `p`를 루프마다 새로 만들면 answer에 N개의 p가 추가됨. 하나의 p에 누적하면 깔끔 |
| `innerHTML += text + "<br>"` | `<br>`로 줄바꿈. `textContent` 쓰면 HTML 파싱 안 되므로 innerHTML 사용 |
| `appendChild`를 루프 **밖**에서 | 루프 안에서 매번 appendChild하면 DOM 조작이 N번 → 성능 낭비. 완성 후 한 번만 추가 |

```
[동작 예시] num1=3, txt="hello"
p.innerHTML = "hello<br>hello<br>hello<br>"
→ answer에 p 추가
```

---

#### pre4/sol5 — input visibility 토글

```js
function sol5() {
  let inputs = document.getElementsByTagName("input");
  for (let i of inputs) {
    if (i.style.visibility == "hidden") {
      i.style.visibility = "visible";
    } else {
      i.style.visibility = "hidden";
    }
  }
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `getElementsByTagName("input")` | 페이지 내 모든 input 선택. 버튼(li)은 input이 아니므로 영향 없음 |
| `visibility: hidden` vs `display: none` | `hidden`은 **공간 유지**하면서 숨김 → 레이아웃 흔들림 없이 토글 가능. `none`은 공간도 사라짐 |
| 현재 값을 읽어서 반대로 설정 | flag 변수 없이 현재 상태로 판단 → 코드 간결 |

---

#### pre4/sol6 — li 색상 무지개 순환

```js
var buttonColor = 0;
var color = ["red","orange","yellow","green","blue","navy","purple"];

function sol6() {
  for (let li of document.getElementsByTagName("li")) {
    li.style.color = color[buttonColor % 7];
  }
  buttonColor++;
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `buttonColor`를 전역 변수로 선언 | 클릭할 때마다 누적되어야 하므로 함수 밖에 선언. 지역 변수면 매번 0으로 리셋 |
| `% 7` (모듈로 연산) | 0~6 → 7가지 색상 순환. 7 이상이면 다시 0부터. 배열 길이에 맞춰 순환 |
| 모든 `li`에 **같은 색** 적용 | 버튼 클릭 1회 → 전체 리스트가 같은 색으로 바뀜. 클릭할 때마다 다음 색으로 |

```
[클릭 횟수별 색상]
1번째 클릭: 0%7=0 → red
2번째 클릭: 1%7=1 → orange
...
8번째 클릭: 7%7=0 → red (순환)
```

---

#### pre4/sol7 — 공지사항 div 토글

```js
function sol7() {
  let notice = document.getElementById("notice");
  if (!notice) {
    let obj = document.createElement("div");
    obj.id = "notice";
    obj.style.border = "red double 3px";
    obj.style.fontSize = "2em";
    obj.style.height = "100px";
    obj.style.width = "520px";
    obj.style.backgroundColor = "beige";
    obj.innerHTML = "<strong>Assignment #5</strong>";

    let body = document.getElementsByTagName("body")[0];
    body.insertBefore(obj, document.getElementsByTagName("p")[0]);
  } else {
    document.getElementsByTagName("body")[0].removeChild(notice);
  }
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `getElementById("notice")`로 존재 여부 판단 | 없으면 `null` 반환 → `!notice`가 true. id를 상태 플래그로 활용 |
| `insertBefore(obj, p[0])` | 첫 번째 `<p>` 앞에 삽입 → 화면 상단에 공지사항 표시 |
| `removeChild(notice)` | `notice.remove()`도 동일하게 동작. 부모에서 자식 제거 |
| 스타일을 JS로 직접 지정 | 외부 CSS 없이도 동작하도록 인라인 스타일로 설정 |

```
[토글 동작]
1번째 클릭: notice=null → 생성 + 삽입
2번째 클릭: notice=div요소 → 삭제
3번째 클릭: notice=null → 다시 생성 ...
```

---

#### pre4/sol8 — 이미지 생성 + 크기 읽기

```js
function sol8() {
  let img = document.createElement("img");
  img.src = "./logo (1).png";

  // 주의: DOM에 추가하기 전에는 width/height가 0
  let num1 = document.getElementById("num1");
  let num2 = document.getElementById("num2");
  num1.value = img.width;   // 로딩 전이면 0
  num2.value = img.height;  // 로딩 전이면 0
}
```

**핵심 선택 이유 + 주의사항**

| 결정 | 이유 |
|------|------|
| `createElement("img")` + `.src` 설정 | img 요소 생성 후 src 지정 → 이미지 로딩 시작 |
| `img.width` / `img.height` | DOM 객체의 렌더링 크기. **DOM에 추가되고 이미지 로딩 완료 전에는 0 반환** |
| 실제 크기 읽으려면 `onload` 이벤트 필요 | `img.onload = function() { console.log(img.naturalWidth); }` |

```
[주의] img를 DOM에 appendChild하지 않으면 브라우저가 렌더링 안 함
→ width/height = 0
정확한 크기: img.naturalWidth / img.naturalHeight (원본 픽셀 크기)
```

---

#### pre4/sol9 — 방향키로 이미지 이동

```js
var xAxis = 0;
var yAxis = 0;

function sol9() {
  let img = document.createElement("img");
  img.src = "logo (1).png";
  img.style.position = "relative";

  function keyProcess(event) {
    switch (event.keyCode) {
      case 37: xAxis -= 1; break;  // ←
      case 38: yAxis -= 1; break;  // ↑
      case 39: xAxis += 1; break;  // →
      case 40: yAxis += 1; break;  // ↓
    }
    img.style.left = xAxis + "px";
    img.style.top  = yAxis + "px";
  }

  document.getElementById("answer").appendChild(img);
  document.addEventListener("keydown", keyProcess);
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `xAxis`, `yAxis`를 전역 변수로 선언 | 이벤트가 발생할 때마다 누적된 위치값 유지. 지역 변수면 키 누를 때마다 0으로 리셋 |
| `img.style.position = "relative"` | `top`/`left`는 `position`이 static이 아닐 때만 적용됨 |
| `switch` + `event.keyCode` | 방향키 4개를 분기. keyCode 37~40 = ←↑→↓ |
| `keyProcess`를 sol9 내부 함수로 정의 | img 변수를 클로저로 캡처. 함수 밖에 정의하면 img에 접근 불가 |
| `document.addEventListener` | 특정 요소가 아닌 문서 전체에서 키 입력 감지 |

```
[keyCode 방향키]
37 ←  38 ↑
39 →  40 ↓

[이동 방향]
↑ yAxis 감소 (top 감소 → 위로)
↓ yAxis 증가 (top 증가 → 아래로)
← xAxis 감소 (left 감소 → 왼쪽으로)
→ xAxis 증가 (left 증가 → 오른쪽으로)
```

---

## 2024 과제 솔루션 해설

### 2024/3.html — calculateAverage (3가지 방식)

같은 평균 계산을 `for`, `for...of`, `forEach` 3가지로 구현하는 예제.

```js
// ① for 루프 — 인덱스로 접근
function calculateAverage(scores) {
  let sum = 0;
  for (i = 0; i < scores.length; i++) {
    sum = sum + scores[i];
  }
  return sum / scores.length;
}

// ② for...of — 요소값 직접 순회
function calculateAverage2(scores) {
  let sum = 0;
  for (ch of scores) {
    sum = sum + ch;
  }
  return sum / scores.length;
}

// ③ forEach — 콜백 함수로 순회 (화살표 함수)
function calculateAverage3(scores) {
  let sum = 0;
  scores.forEach(element => {
    sum = sum + element;
  });
  return sum / scores.length;
}
```

**비교표**

| 방식 | 인덱스 접근 | 요소 접근 | 외부 변수 수정 | break 가능 |
|------|-------------|-----------|----------------|------------|
| `for` | ✅ i로 직접 | `arr[i]` | ✅ | ✅ |
| `for...of` | ❌ | 변수에 직접 | ✅ | ✅ |
| `forEach` | ❌ (콜백 인자로는 가능) | 콜백 인자 | ✅ (외부 변수) | ❌ |

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `forEach`에서 `sum`을 외부에 선언 | `forEach` 콜백 안은 별도 스코프 → 결과를 바깥으로 꺼내려면 외부 변수에 누적해야 함 |
| `return sum / scores.length`는 루프 밖에 | 루프 완료 후 전체 합계를 길이로 나눠야 하므로 |

---

### 2024/4.html — 콜라츠 추측 (Collatz Conjecture)

숫자에 짝수이면 2로 나누고, 홀수이면 3×n+1 을 반복해 1이 될 때까지의 횟수를 센다.

```js
function collatzStep() {
  let num, count;
  num = prompt("2~100 사이의 숫자를 입력하세요");
  count = 0;
  while (num !== 1) {
    if (num % 2 == 0) {
      num = num / 2;
    } else {
      num = num * 3 + 1;
    }
    count = count + 1;
  }
  console.log("총 " + count + " 회의 작업이 요구됨.");
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `while (num !== 1)` | 종료 조건이 "1이 될 때까지" → 몇 번 반복할지 모르므로 `for`보다 `while` 적합 |
| `count`를 루프 밖에서 초기화 | 함수 호출마다 0에서 시작해야 함 |
| `num % 2 == 0`으로 짝홀 판단 | 나머지가 0이면 짝수, 1이면 홀수 |

```
[실행 예: num=6]
6 → 3 → 10 → 5 → 16 → 8 → 4 → 2 → 1  (8회)
```

---

### 2024/5.html — 팩토리얼 누적합 (facSum)

1! + 2! + 3! + ... + n! 계산 + 각 팩토리얼 값을 배열로 출력.

```js
function facSum() {
  let len, paclist, last, sum;
  len = prompt("리스트의 길이를 입력하세요:");
  paclist = [];
  last = 1;
  sum = 0;
  for (i = 1; i < (parseInt(len) + 1); i++) {
    last = last * i;       // 이전 팩토리얼 × i = i!
    paclist.push(last);    // 배열에 추가
  }
  for (i = 0; i < paclist.length; i++) {
    sum = sum + paclist[i];
  }
  console.log("List", paclist);
  console.log("합계: ", sum);
}
```

**핵심 선택 이유**

| 결정 | 이유 |
|------|------|
| `last = last * i` 패턴 | 매번 0부터 곱하지 않고, 이전 결과에 i만 곱하면 i! 계산 (누적 곱) |
| `paclist.push(last)` | 배열 끝에 요소 추가. `arr[i] = val`도 가능하지만 push가 더 간결 |
| `parseInt(len)` | `prompt()`는 항상 문자열 반환 → 정수로 변환 필요 |
| 루프를 2개로 분리 | 팩토리얼 목록 생성 후 합계 계산. 하나로 합칠 수도 있음 |

```
[len=4 기준]
i=1: last=1   → [1]
i=2: last=2   → [1, 2]
i=3: last=6   → [1, 2, 6]
i=4: last=24  → [1, 2, 6, 24]
합계: 33
```

---

### 2024/hw3.html — quest0~9

#### quest0 — 초 → 분/초 변환

```js
function quest0() {
  var time = prompt("초 단위 시간을 입력하세요");
  var min = time / 60;
  var sec = time % 60;
  console.log(Math.floor(min) + " 분 " + sec + " 초입니다.");
}
```

| 결정 | 이유 |
|------|------|
| `Math.floor(min)` | 나눗셈 결과는 소수 → 버림하여 정수 분 획득 |
| `time % 60` | 나머지 = 초 단위 잔여분 |

---

#### quest1 + getDist — 두 점 거리 계산

```js
function quest1() {
  var x1 = prompt("첫 번째 점의 x좌표");
  var y1 = prompt("첫 번째 점의 y좌표");
  var x2 = prompt("두 번째 점의 x좌표");
  var y2 = prompt("두 번째 점의 y좌표");
  var p1 = [x1, y1];
  var p2 = [x2, y2];
  let distance = getDist(p1, p2);
  console.log(distance);
}

function getDist(p1, p2) {
  Double_dist = (p1[0] - p2[0]) * (p1[0] - p2[0]) + (p1[1] - p2[1]) * (p1[1] - p2[1]);
  dist = Math.sqrt(Double_dist);
  return dist;
}
```

| 결정 | 이유 |
|------|------|
| 좌표를 배열 `[x, y]`로 전달 | 2개 값을 묶어 함수 인자 1개로 전달 |
| `p1[0] - p2[0]` | 배열 인덱스로 x좌표 접근 |
| `Math.sqrt(...)` | 유클리드 거리 = √((x1-x2)² + (y1-y2)²) |

---

#### quest2 — 대문자 변환 + 특수문자 제거

```js
function quest2(str) {
  let upperStr = str.toUpperCase().replace(/'/g, "");
  return upperStr;
}
```

| 결정 | 이유 |
|------|------|
| `.toUpperCase()` | 문자열 전체를 대문자로 변환 |
| `.replace(/'/g, "")` | 정규식으로 아포스트로피(') 전부 제거. `g` 플래그 = 전역 치환 |

**정규식 replace 패턴**
```js
str.replace(/패턴/g, "교체값")
// g 없으면 첫 번째 매치만 교체
// g 있으면 전부 교체

str.replace(/[,.\s]/g, "")   // 쉼표, 마침표, 공백 제거
str.replace(/[\,\.]/g, "")   // 쉼표, 마침표 제거
str.replace(/'/g, "")        // 아포스트로피 제거
```

---

#### quest3 + operate — 사칙연산 계산기 (switch)

```js
function operate(num1, oper, num2) {
  var result;
  switch (oper) {
    case "+": result = num1 + num2; break;
    case "-": result = num1 - num2; break;
    case "/": result = Math.floor(num1 / num2); break;  // 정수 나눗셈
    case "*": result = num1 * num2; break;
    case "%": result = num1 % num2; break;
  }
  return result;
}
```

| 결정 | 이유 |
|------|------|
| `switch(oper)` | 문자열 연산자로 분기. if/else보다 각 케이스가 명확 |
| `Math.floor(num1 / num2)` | `/`는 정수 나눗셈 요구 → 소수점 버림 |
| `Number(prompt(...))` | prompt 결과는 string → 숫자 연산 전 변환 필수 |

---

#### quest4 — 가위바위보 (Math.random + 버그 주의)

```js
function quest4() {
  var human = prompt("가위 바위 보!");
  var random = Math.floor(Math.random() * 3) + 1;  // 1, 2, 3 중 하나
  // ⚠️ 버그: if (1 <= random < 2) 는 항상 true
  // 올바른 방법: if (random === 1)
  if (random === 1)      computer = "가위";
  else if (random === 2) computer = "바위";
  else                   computer = "보";
}
```

**Math.random() 패턴**
```js
Math.floor(Math.random() * N)         // 0 ~ N-1 정수
Math.floor(Math.random() * N) + 1     // 1 ~ N 정수
Math.floor(Math.random() * (max - min + 1)) + min  // min ~ max 정수
```

**⚠️ JS 비교 연산자 체이닝 버그**
```js
// ❌ 틀림: 1 <= random < 2 는 항상 true
//   → (1 <= random)이 true/false(boolean)로 평가
//   → boolean < 2 → 1 < 2 또는 0 < 2 → 항상 true
if (1 <= random < 2) { ... }

// ✅ 올바름
if (random >= 1 && random < 2) { ... }
if (random === 1) { ... }
```

---

#### quest5 + myReverse — 문자열 역순

```js
function myReverse(str) {
  var strlength = str.length;
  var reversestr = "";
  for (i = 1; i < strlength + 1; i++) {
    reversestr = reversestr + str[strlength - i];
  }
  return reversestr;
}
```

| 결정 | 이유 |
|------|------|
| `str[strlength - i]` | i=1일 때 마지막 문자, i=2일 때 끝에서 두 번째... |
| 빈 문자열에 누적 | `reversestr += str[...]` 패턴으로 역순 문자열 구성 |

```
str = "abc", length=3
i=1: str[2]="c" → reversestr="c"
i=2: str[1]="b" → reversestr="cb"
i=3: str[0]="a" → reversestr="cba"
```

---

#### quest6 — 양의 홀수만 출력 (while + 조건 분기)

```js
function quest6() {
  var number = prompt("숫자를 입력하세요:");
  while (true) {
    if (number > 0 && number % 2 == 1) {
      console.log(number + "를 입력하셨네요.");
    } else if (number < 0) {
      console.log("끝!");
      break;
    }
    number = prompt("숫자를 입력하세요:");
  }
}
```

| 결정 | 이유 |
|------|------|
| `while (true)` + `break` | 종료 조건이 입력값에 따라 다름 → 무한 루프로 반복 후 조건 만족 시 탈출 |
| 음수 입력 시 `break` | 특정 입력값을 종료 신호로 사용하는 패턴 |

---

#### quest7 — 단어 첫 글자 대문자 (initials)

```js
function quest7() {
  var text = prompt("문자열을 입력해주세요.");
  var strsplit = text.split(" ");
  var strupper = "";
  for (i = 0; i < strsplit.length; i++) {
    strupper = strupper + strsplit[i][0].toUpperCase();
  }
  console.log(strupper);
}
```

| 결정 | 이유 |
|------|------|
| `text.split(" ")` | 공백으로 분리 → 단어 배열 생성 |
| `strsplit[i][0]` | i번째 단어의 0번째 문자 = 첫 글자 |
| `.toUpperCase()` | 첫 글자만 대문자로 변환 |

```
"my name is" → ["my","name","is"] → "M"+"N"+"I" → "MNI"
```

---

#### quest8 — 중복 없는 단어 정렬 출력 (nested for dedup)

```js
function quest8(str) {
  str = str.replace(/\,/g, "").replace(/\./g, "");
  var strlist = str.split(" ");
  var array = [];
  for (i = 0; i < strlist.length; i++) {
    var found = false;
    for (var j = 0; j < array.length; j++) {
      if (strlist[i] === array[j]) {
        found = true;
        break;
      }
    }
    if (!found) {
      array.push(strlist[i]);
    }
  }
  array.sort();
  for (i = 0; i < array.length; i++) {
    console.log(array[i]);
  }
}
```

**중복 제거 패턴 (nested for)**
```
단어마다: 결과 배열에 이미 있는지 검사
  - 있으면: found=true, break
  - 없으면: push
→ 결과 배열에는 중복 없음
```

| 결정 | 이유 |
|------|------|
| `found` 플래그 | 내부 루프 탈출 후 "발견됐는지" 외부에서 판단하기 위한 불리언 |
| `break` (내부 루프) | 이미 찾았으면 더 비교할 필요 없음 → 성능 최적화 |
| `array.sort()` | 알파벳순 정렬 (기본: 문자열 오름차순) |

---

#### quest9 — 문자 빈도수 계산 (object frequency map)

```js
function quest9(str) {
  var alphabet = {};
  var cleanStr = str.replace(/[\,\.\;\s]/g, "");  // 구두점·공백 제거
  for (var i = 0; i < cleanStr.length; i++) {
    var char = cleanStr[i];
    if (alphabet[char]) {
      alphabet[char]++;
    } else {
      alphabet[char] = 1;
    }
  }
  for (var key in alphabet) {
    console.log(key + ": " + alphabet[key]);
  }
}
```

**object를 카운터로 쓰는 패턴**
```js
var counter = {};
// 처음 등장: 초기화
// 이미 있으면: +1
if (counter[item]) {
  counter[item]++;
} else {
  counter[item] = 1;
}
// 또는 단축형:
counter[item] = (counter[item] || 0) + 1;
```

| 결정 | 이유 |
|------|------|
| 빈 객체 `{}`를 카운터로 사용 | 키=문자, 값=횟수로 자연스럽게 매핑 |
| `alphabet[char]` truthy 체크 | 값이 없으면 `undefined` (falsy) → 최초 등장 판별 |
| `for...in` | 객체의 모든 키를 순회 |
| 정규식 `[\,\.\;\s]` | 문자 클래스 `[]`로 여러 문자 한 번에 매칭 |
