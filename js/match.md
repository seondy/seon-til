# match

## match 함수  
String.prototype.match 동작
- 문자열을 정규식과 대조함
  - 매칭 O: 배열 반환. (전체 매칭 문자열, 각 캡처 그룹의 값)
  - 매칭 X: null값 반환.

---

## 정규식 `^\/([a-z]{2})(\/.*)$`
- ^ : 문자열 시작.
- \/ : 슬래시(/) 한 개.
- ([a-z]{2}) : 소문자 알파벳 두 글자(캡처 그룹 1)
- (\/.*) : 슬래시(/) 한 개 + 그 뒤의 모든 문자(캡처 그룹 2)
- $ : 문자열 끝.

---

## 사용 예시
```js
const regex = /^\/([a-z]{2})(\/.*)$/;

const str1 = "/ko/about";
const str2 = "/en";
const str3 = "/abc/test";

console.log(str1.match(regex));
console.log(str2.match(regex));
console.log(str3.match(regex));
```

```js
console.log(str1.match(regex)); // /ko/about

[
  "/ko/about", // 전체 매칭
  "ko",        // 캡처 그룹 1
  "/about"     // 캡처 그룹 2
]
```

```js
console.log(str2.match(regex)); // /en

null
// 매칭 실패로 null 반환
```

```js
console.log(str3.match(regex)); // /abc/test

null
// 매칭 실패로 null 반환
// 정규식 캡처 그룹 1에 맞지 않음
```

### 참고
- [mdn String.prototype.match()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/match)
---
`2026-03-17`