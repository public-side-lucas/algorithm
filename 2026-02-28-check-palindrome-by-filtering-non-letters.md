---
title: "Check Palindrome by Filtering Non-Letters"
date: 2026-02-28
category: 기타
difficulty: easy
---

# Check Palindrome by Filtering Non-Letters

| 항목 | 내용 |
|------|------|
| 📅 작성일 | 2026-02-28 |
| 📁 카테고리 | 기타 |
| 🎯 난이도 | 🟢 쉬움 |
| ⏱️ 시간 복잡도 | **O(n)** |
| 💾 공간 복잡도 | **O(n)** |

## 📝 개요

Given a string containing letters, digits, and symbols, determine if it reads the same forwards and backwards when considering only alphabetic characters (case-insensitive).

## 💻 알고리즘 코드

```javascript
// 백준 스타일 입력 — require("fs").readFileSync 지원
const input = require("fs").readFileSync("/dev/stdin", "utf8").trim();
const lines = input.split("\n")[0]


function isAlphabeticPalindrome(code) {
    const letters = code.split("").filter((s)=> /[a-zA-Z]/.test(s)).map((s)=> s.toLowerCase())
    const length = letters.length
    for(let i =0; i< length /2; i++){
        if(letters[i] !== letters[length - i -1 ]) return 0
    }
    
    // Write your code here
    return 1
}

console.log(isAlphabeticPalindrome(lines))
```

## 📥 입력과 출력

### 입력

```
A1b2B!a
```

### 출력

```
1
```

## 📊 복잡도 분석

| 구분 | 복잡도 |
|------|--------|
| ⏱️ 시간 복잡도 | **O(n)** |
| 💾 공간 복잡도 | **O(n)** |

> 반복문 1개, 빌트인 메서드 4개 감지. 시간 복잡도 O(n)(선형 시간 — 입력에 비례), 공간 복잡도 O(n).

#### 상세 분석

- 📦 **Line 3** `input.split("\n")` — String.split()는 O(n)
- 📦 **Line 7** `code.split("").filter((s)=> /[a-zA-Z]/.test(s)).ma…` — Array.map()는 O(n)
- 📦 **Line 7** `code.split("").filter((s)=> /[a-zA-Z]/.test(s))` — Array.filter()는 O(n)
- 📦 **Line 7** `code.split("")` — String.split()는 O(n)
- 🔄 **Line 9** `for(let i =0; i< length /2; i++){` — 반복문 중첩 깊이 1 → O(n)

## 🔍 실행 흐름 분석

총 **15개**의 실행 단계가 기록되었습니다.

| Step | Line | input | lines | isAlphabeticPalindrome | code | letters | length | i | 설명 |
|------|------|------|------|------|------|------|------|------|------|
| 1 | 2 | "A1b2B!a" | - | - | - | - | - | - | const input = "A1b2B!a" |
| 2 | 3 | "A1b2B!a" | "A1b2B!a" | - | - | - | - | - | const lines = "A1b2B!a" |
| 3 | 6 | "A1b2B!a" | "A1b2B!a" | [Function] | - | - | - | - | function isAlphabeticPalindrome() declared |
| 4 | 7 | "A1b2B!a" | "A1b2B!a" | [Function] | "A1b2B!a" | ["a", "b", "b", "a"] | - | - | const letters = ["a", "b", "b", "a"] |
| 5 | 8 | "A1b2B!a" | "A1b2B!a" | [Function] | "A1b2B!a" | ["a", "b", "b", "a"] | 4 | - | const length = 4 |
| 6 | 9 | "A1b2B!a" | "A1b2B!a" | [Function] | "A1b2B!a" | ["a", "b", "b", "a"] | 4 | 0 | let i = 0 |
| 7 | 9 | "A1b2B!a" | "A1b2B!a" | [Function] | "A1b2B!a" | ["a", "b", "b", "a"] | 4 | 0 | for condition → true |
| 8 | 10 | "A1b2B!a" | "A1b2B!a" | [Function] | "A1b2B!a" | ["a", "b", "b", "a"] | 4 | 0 | if (if(letters[i] !== letters[length - i -1 ]) return 0) → false |
| 9 | 9 | "A1b2B!a" | "A1b2B!a" | [Function] | "A1b2B!a" | ["a", "b", "b", "a"] | 4 | 1 | for update: for(let i =0; i< length /2; i++){ |
| 10 | 9 | "A1b2B!a" | "A1b2B!a" | [Function] | "A1b2B!a" | ["a", "b", "b", "a"] | 4 | 1 | for condition → true |
| 11 | 10 | "A1b2B!a" | "A1b2B!a" | [Function] | "A1b2B!a" | ["a", "b", "b", "a"] | 4 | 1 | if (if(letters[i] !== letters[length - i -1 ]) return 0) → false |
| 12 | 9 | "A1b2B!a" | "A1b2B!a" | [Function] | "A1b2B!a" | ["a", "b", "b", "a"] | 4 | 2 | for update: for(let i =0; i< length /2; i++){ |
| 13 | 9 | "A1b2B!a" | "A1b2B!a" | [Function] | "A1b2B!a" | ["a", "b", "b", "a"] | 4 | 2 | for condition → false |
| 14 | 14 | "A1b2B!a" | "A1b2B!a" | [Function] | "A1b2B!a" | ["a", "b", "b", "a"] | 4 | - | return 1 |
| 15 | 17 | "A1b2B!a" | "A1b2B!a" | [Function] | - | - | - | - | console.log(isAlphabeticPalindrome(lines))() called |

---

> 🤖 이 포스트는 **Algorithm Flow** 시각화 도구를 통해 자동으로 생성되었습니다.
> 📅 생성 일시: 2026. 2. 28. 오전 10:55:46
