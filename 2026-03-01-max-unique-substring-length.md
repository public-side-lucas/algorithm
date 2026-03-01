---
title: "Max Unique Substring Length"
date: 2026-03-01
category: 기타
difficulty: easy
---

# Max Unique Substring Length

| 항목 | 내용 |
|------|------|
| 📅 작성일 | 2026-03-01 |
| 📁 카테고리 | 기타 |
| 🎯 난이도 | 🟢 쉬움 |
| ⏱️ 시간 복잡도 | **O(n²)** |
| 💾 공간 복잡도 | **O(n)** |

## 📝 개요

Max Unique Substring Length in a Session
Given a string of lowercase letters with sessions separated by '' characters, find the maximum length of a substring with all distinct letters within any single session.

Example

Input

sessionString = abcabcbb
Output

3
Explanation

- There is only one session: "abcabcbb". 
- Scanning with a sliding window for distinct letters, the longest substrings without repeats are "abc", "bca" and so on, each of length 3. 
- Therefore, the result is 3.
Input Format

A single line containing the string sessionString.
Constraints

0 <= S.length <= 100000
For all i in [0, S.length]: S[i] is either '*' or a lowercase letter 'a' to 'z'
Each session is defined as a maximal contiguous substring of S without '*' characters
Number of sessions (segments between '*') is at most S.length + 1
Output Format

A single integer denoting the maximum length among all substrings. If sessionString is empty or contains only '*', output 0.
Sample Input 0

*
Sample Output 0

0
Sample Input 1

aa
Sample Output 1

1

## 💻 알고리즘 코드

```javascript
// 백준 스타일 입력 — require("fs").readFileSync 지원
const input = require("fs").readFileSync("/dev/stdin", "utf8").trim();
const lines = input.split("\n");



function maxDistinctSubstringLengthInSessions(s) {
    const sessions = s.split("*")
    let maxResult = 0
    
    for(let session of sessions){
        
        let left = 0;
        let result = 0
        const seen = new Map()
        
        for(let right = 0; right < session.length; right++){
            const cur = session[right]
            if(seen.has(cur)){
                left = seen.get(cur) + 1
            }
            
            seen.set(cur, right)
            result = Math.max(result, right - left + 1)
        }
        
        maxResult = Math.max(maxResult, result)
    }
      return maxResult
}

console.log(maxDistinctSubstringLengthInSessions(lines[0]))
```

## 📥 입력과 출력

### 입력

```
aa
```

### 출력

```
2
```

## 📊 복잡도 분석

| 구분 | 복잡도 |
|------|--------|
| ⏱️ 시간 복잡도 | **O(n²)** |
| 💾 공간 복잡도 | **O(n)** |

> 반복문 2개, 빌트인 메서드 2개 감지. 시간 복잡도 O(n²)(이차 시간 — 중첩 루프), 공간 복잡도 O(n).

#### 상세 분석

- 📦 **Line 3** `input.split("\n")` — String.split()는 O(n)
- 📦 **Line 8** `s.split("*")` — String.split()는 O(n)
- 🔄 **Line 11** `for(let session of sessions){` — 반복문 중첩 깊이 1 → O(n)
- 🔄 **Line 17** `for(let right = 0; right < session.length; right++…` — 반복문 중첩 깊이 2 → O(n²)

## 🔍 실행 흐름 분석

총 **26개**의 실행 단계가 기록되었습니다.

| Step | Line | input | lines | maxDistinctSubstringLengthInSessions | s | sessions | maxResult | session | left | result | seen | right | cur | 설명 |
|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|
| 1 | 2 | "aa" | - | - | - | - | - | - | - | - | - | - | - | const input = "aa" |
| 2 | 3 | "aa" | ["aa"] | - | - | - | - | - | - | - | - | - | - | const lines = ["aa"] |
| 3 | 7 | "aa" | ["aa"] | [Function] | - | - | - | - | - | - | - | - | - | function maxDistinctSubstringLengthInSessions() declared |
| 4 | 8 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | - | - | - | - | - | - | - | const sessions = ["aa"] |
| 5 | 9 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | - | - | - | - | - | - | let maxResult = 0 |
| 6 | 11 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | - | - | - | - | - | for...of iteration 1: "aa" |
| 7 | 13 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | - | - | - | - | let left = 0 |
| 8 | 14 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 0 | - | - | - | let result = 0 |
| 9 | 15 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 0 | undefined | - | - | const seen = undefined |
| 10 | 17 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 0 | undefined | 0 | - | let right = 0 |
| 11 | 17 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 0 | undefined | 0 | - | for condition → true |
| 12 | 18 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 0 | undefined | 0 | "a" | const cur = "a" |
| 13 | 19 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 0 | undefined | 0 | "a" | if (if(seen.has(cur) ){) → false |
| 14 | 23 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 0 | undefined | 0 | "a" | seen.set(cur, right)() called |
| 15 | 24 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 1 | undefined | 0 | "a" | result = 1 |
| 16 | 17 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 1 | undefined | 1 | "a" | for update: for(let right = 0; right < session.length; right++){ |
| 17 | 17 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 1 | undefined | 1 | "a" | for condition → true |
| 18 | 18 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 1 | undefined | 1 | "a" | const cur = "a" |
| 19 | 19 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 1 | undefined | 1 | "a" | if (if(seen.has(cur) ){) → false |
| 20 | 23 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 1 | undefined | 1 | "a" | seen.set(cur, right)() called |
| 21 | 24 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 2 | undefined | 1 | "a" | result = 2 |
| 22 | 17 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 2 | undefined | 2 | "a" | for update: for(let right = 0; right < session.length; right++){ |
| 23 | 17 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 0 | "aa" | 0 | 2 | undefined | 2 | "a" | for condition → false |
| 24 | 27 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 2 | "aa" | 0 | 2 | undefined | - | - | maxResult = 2 |
| 25 | 29 | "aa" | ["aa"] | [Function] | "aa" | ["aa"] | 2 | - | - | - | - | - | - | return 2 |
| 26 | 32 | "aa" | ["aa"] | [Function] | - | - | - | - | - | - | - | - | - | console.log(maxDistinctSubstringLengthInSessions(lines[0]))() called |

---

> 🤖 이 포스트는 **Algorithm Flow** 시각화 도구를 통해 자동으로 생성되었습니다.
> 📅 생성 일시: 2026. 3. 1. 오후 7:47:40
