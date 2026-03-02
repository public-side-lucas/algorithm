---
title: "Next Greater Element with Position Offset"
date: 2026-03-02
category: 기타
difficulty: easy
---

# Next Greater Element with Position Offset

| 항목 | 내용 |
|------|------|
| 📅 작성일 | 2026-03-02 |
| 📁 카테고리 | 기타 |
| 🎯 난이도 | 🟢 쉬움 |
| ⏱️ 시간 복잡도 | **O(n²)** |
| 💾 공간 복잡도 | **O(n)** |

## 📝 개요

Given an integer array readings, return an array result where result[i] = [value, distance], with value being the next greater element to the right of readings[i] and distance being the index difference. If no greater element exists, return [-1, -1].

Example

Input

readings = [2, 1, 2, 4, 3]
Output

[[4, 3], [2, 1], [4, 1], [-1, -1], [-1, -1]]
Explanation

For each index i in readings:

- i=0, value=2. The next greater element to its right is 4 at index 3, so distance = 3 - 0 = 3 ⇒ [4, 3].
- i=1, value=1. The next greater element is 2 at index 2, distance = 2 - 1 = 1 ⇒ [2, 1].
- i=2, value=2. The next greater element is 4 at index 3, distance = 3 - 2 = 1 ⇒ [4, 1].
- i=3, value=4. There is no greater element to the right ⇒ [-1, -1].
- i=4, value=3. There is no greater element to the right ⇒ [-1, -1].
Input Format

The first line contains an integer n denoring length of array.
The next n line denotes the elements in array.
Example

5
2
1
2
4
3
here 5 is the length of array, followed by the individual elements.

Constraints

0 <= readings.length <= 100000
-1000000000 <= readings[i] <= 1000000000
Output Format

Return a 2D array result of length n.
Sample Input 0

1
5
Sample Output 0

-1 -1
Sample Input 1

5
2
1
2
4
3
Sample Output 1

4 3
2 1
4 1
-1 -1
-1 -1

## 💻 알고리즘 코드

```javascript
// 백준 스타일 입력 — require("fs").readFileSync 지원
const input = require("fs").readFileSync("/dev/stdin", "utf8").trim();
const [sizeStr, ...inputStr] = input.split("\n");
const size = Number(sizeStr)
const inputs = inputStr.map(Number)


function findNextGreaterElementsWithDistance(readings) {
    
    const result = []
    const stack = []
    for(let i =readings.length-1; i>= 0; i--){
        const cur = readings[i]
        while(stack[stack.length-1] != undefined && stack[stack.length-1][0] <= cur){
            stack.pop()
        }
        
        if(stack[stack.length-1] != undefined && stack[stack.length-1][0] > cur)result.push([stack[stack.length-1][0], stack[stack.length-1][1] - i])
        else result.push([-1,-1])
        
        stack.push([cur, i])
    }
    return result.reverse()
}

console.log(findNextGreaterElementsWithDistance(inputs))
```

## 📥 입력과 출력

### 입력

```
5
2
1
2
4
3
```

### 출력

```
[[4, 3], [2, 1], [4, 1], [-1, -1], [-1, -1]]
```

## 📊 복잡도 분석

| 구분 | 복잡도 |
|------|--------|
| ⏱️ 시간 복잡도 | **O(n²)** |
| 💾 공간 복잡도 | **O(n)** |

> 반복문 2개, 빌트인 메서드 3개 감지. 시간 복잡도 O(n²)(이차 시간 — 중첩 루프), 공간 복잡도 O(n).

#### 상세 분석

- 📦 **Line 3** `input.split("\n")` — String.split()는 O(n)
- 📦 **Line 5** `inputStr.map(Number)` — Array.map()는 O(n)
- 🔄 **Line 12** `for(let i =readings.length-1; i>= 0; i--){` — 반복문 중첩 깊이 1 → O(n)
- 🔄 **Line 14** `while(stack[stack.length-1] != undefined && stack[…` — 반복문 중첩 깊이 2 → O(n²)
- 📦 **Line 23** `result.reverse()` — Array.reverse()는 O(n)

## 🔍 실행 흐름 분석

총 **52개**의 실행 단계가 기록되었습니다.

| Step | Line | input | sizeStr | inputStr | size | inputs | findNextGreaterElementsWithDistance | readings | result | stack | i | cur | 설명 |
|------|------|------|------|------|------|------|------|------|------|------|------|------|------|
| 1 | 2 | "5
2
1
2
4
3" | - | - | - | - | - | - | - | - | - | - | const input = "5
2
1
2
4
3" |
| 2 | 3 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | - | - | - | - | - | - | - | - | const destructured = ["5", "2", "1", "2", "4", "3"] |
| 3 | 4 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | - | - | - | - | - | - | - | const size = 5 |
| 4 | 5 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | - | - | - | - | - | - | const inputs = [2, 1, 2, 4, 3] |
| 5 | 8 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | - | - | - | - | - | function findNextGreaterElementsWithDistance() declared |
| 6 | 10 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [] | - | - | - | const result = [] |
| 7 | 11 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [] | [] | - | - | const stack = [] |
| 8 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [] | [] | 4 | - | let i = 4 |
| 9 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [] | [] | 4 | - | for condition → true |
| 10 | 13 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [] | [] | 4 | 3 | const cur = 3 |
| 11 | 14 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [] | [] | 4 | 3 | while (while(stack[stack.length-1] != undefined && stack[stack.length-1][0] <= cur){) → false |
| 12 | 18 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [] | [] | 4 | 3 | if (if(stack[stack.length-1] != undefined && stack[stack.length-1][0] > cur)result.push([stack[stack.length-1][0], stack[stack.length-1][1] - i])) → false |
| 13 | 19 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1]] | [] | 4 | 3 | else result.push([-1,-1])() called → 1 |
| 14 | 21 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1]] | [[3, 4]] | 4 | 3 | stack.push([cur, i])() called → 1 |
| 15 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1]] | [[3, 4]] | 3 | 3 | for update: for(let i =readings.length-1; i>= 0; i--){ |
| 16 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1]] | [[3, 4]] | 3 | 3 | for condition → true |
| 17 | 13 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1]] | [[3, 4]] | 3 | 4 | const cur = 4 |
| 18 | 14 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1]] | [[3, 4]] | 3 | 4 | while (while(stack[stack.length-1] != undefined && stack[stack.length-1][0] <= cur){) → true |
| 19 | 15 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1]] | [] | 3 | 4 | stack.pop()() called → [3, 4] |
| 20 | 14 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1]] | [] | 3 | 4 | while (while(stack[stack.length-1] != undefined && stack[stack.length-1][0] <= cur){) → false |
| 21 | 18 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1]] | [] | 3 | 4 | if (if(stack[stack.length-1] != undefined && stack[stack.length-1][0] > cur)result.push([stack[stack.length-1][0], stack[stack.length-1][1] - i])) → false |
| 22 | 19 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1]] | [] | 3 | 4 | else result.push([-1,-1])() called → 2 |
| 23 | 21 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1]] | [[4, 3]] | 3 | 4 | stack.push([cur, i])() called → 1 |
| 24 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1]] | [[4, 3]] | 2 | 4 | for update: for(let i =readings.length-1; i>= 0; i--){ |
| 25 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1]] | [[4, 3]] | 2 | 4 | for condition → true |
| 26 | 13 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1]] | [[4, 3]] | 2 | 2 | const cur = 2 |
| 27 | 14 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1]] | [[4, 3]] | 2 | 2 | while (while(stack[stack.length-1] != undefined && stack[stack.length-1][0] <= cur){) → false |
| 28 | 18 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1]] | [[4, 3]] | 2 | 2 | if (if(stack[stack.length-1] != undefined && stack[stack.length-1][0] > cur)result.push([stack[stack.length-1][0], stack[stack.length-1][1] - i])) → true |
| 29 | 18 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1]] | [[4, 3]] | 2 | 2 | if(stack[stack.length-1] != undefined && stack[stack.length-1][0] > cur)result.push([stack[stack.length-1][0], stack[stack.length-1][1] - i])() called → 3 |
| 30 | 21 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1]] | [[4, 3], [2, 2]] | 2 | 2 | stack.push([cur, i])() called → 2 |
| 31 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1]] | [[4, 3], [2, 2]] | 1 | 2 | for update: for(let i =readings.length-1; i>= 0; i--){ |
| 32 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1]] | [[4, 3], [2, 2]] | 1 | 2 | for condition → true |
| 33 | 13 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1]] | [[4, 3], [2, 2]] | 1 | 1 | const cur = 1 |
| 34 | 14 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1]] | [[4, 3], [2, 2]] | 1 | 1 | while (while(stack[stack.length-1] != undefined && stack[stack.length-1][0] <= cur){) → false |
| 35 | 18 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1]] | [[4, 3], [2, 2]] | 1 | 1 | if (if(stack[stack.length-1] != undefined && stack[stack.length-1][0] > cur)result.push([stack[stack.length-1][0], stack[stack.length-1][1] - i])) → true |
| 36 | 18 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1]] | [[4, 3], [2, 2]] | 1 | 1 | if(stack[stack.length-1] != undefined && stack[stack.length-1][0] > cur)result.push([stack[stack.length-1][0], stack[stack.length-1][1] - i])() called → 4 |
| 37 | 21 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1]] | [[4, 3], [2, 2], [1, 1]] | 1 | 1 | stack.push([cur, i])() called → 3 |
| 38 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1]] | [[4, 3], [2, 2], [1, 1]] | 0 | 1 | for update: for(let i =readings.length-1; i>= 0; i--){ |
| 39 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1]] | [[4, 3], [2, 2], [1, 1]] | 0 | 1 | for condition → true |
| 40 | 13 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1]] | [[4, 3], [2, 2], [1, 1]] | 0 | 2 | const cur = 2 |
| 41 | 14 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1]] | [[4, 3], [2, 2], [1, 1]] | 0 | 2 | while (while(stack[stack.length-1] != undefined && stack[stack.length-1][0] <= cur){) → true |
| 42 | 15 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1]] | [[4, 3], [2, 2]] | 0 | 2 | stack.pop()() called → [1, 1] |
| 43 | 14 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1]] | [[4, 3], [2, 2]] | 0 | 2 | while (while(stack[stack.length-1] != undefined && stack[stack.length-1][0] <= cur){) → true |
| 44 | 15 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1]] | [[4, 3]] | 0 | 2 | stack.pop()() called → [2, 2] |
| 45 | 14 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1]] | [[4, 3]] | 0 | 2 | while (while(stack[stack.length-1] != undefined && stack[stack.length-1][0] <= cur){) → false |
| 46 | 18 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1]] | [[4, 3]] | 0 | 2 | if (if(stack[stack.length-1] != undefined && stack[stack.length-1][0] > cur)result.push([stack[stack.length-1][0], stack[stack.length-1][1] - i])) → true |
| 47 | 18 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1], [4, 3]] | [[4, 3]] | 0 | 2 | if(stack[stack.length-1] != undefined && stack[stack.length-1][0] > cur)result.push([stack[stack.length-1][0], stack[stack.length-1][1] - i])() called → 5 |
| 48 | 21 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1], [4, 3]] | [[4, 3], [2, 0]] | 0 | 2 | stack.push([cur, i])() called → 2 |
| 49 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1], [4, 3]] | [[4, 3], [2, 0]] | -1 | 2 | for update: for(let i =readings.length-1; i>= 0; i--){ |
| 50 | 12 | "5
2
1
2
4
3" | "5" | ["2", "1", "2", "4", "3"] | 5 | [2, 1, 2, 4, 3] | [Function] | [2, 1, 2, 4, 3] | [[-1, -1], [-1, -1], [4, 1], [2, 1], [4, 3]] | [[4, 3], [2, 0]] | -1 | 2 | for condition → false |

> 📋 총 52개의 스텝 중 처음 50개만 표시됩니다.

## 💡 핵심 포인트

스택으로 접근

---

> 🤖 이 포스트는 **Algorithm Flow** 시각화 도구를 통해 자동으로 생성되었습니다.
> 📅 생성 일시: 2026. 3. 2. 오후 8:56:20
