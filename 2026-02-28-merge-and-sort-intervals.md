---
title: "Merge and Sort Intervals"
date: 2026-02-28
category: 기타
difficulty: easy
---

# Merge and Sort Intervals

| 항목 | 내용 |
|------|------|
| 📅 작성일 | 2026-02-28 |
| 📁 카테고리 | 기타 |
| 🎯 난이도 | 🟢 쉬움 |
| ⏱️ 시간 복잡도 | **O(n log n)** |
| 💾 공간 복잡도 | **O(n)** |

## 📝 개요

Merge and Sort Intervals
Given an array of intervals [startTime, endTime], merge all overlapping intervals and return a sorted array of non-overlapping intervals.

Example

Input

intervals = [[1, 3], [2, 6], [8, 10], [15, 18]]
Output

[[1, 6], [8, 10], [15, 18]]
Explanation

- Step 1: Sort intervals by start time (already sorted). 
- Step 2: Initialize merged list with first interval [1,3]. 
- Step 3: Compare [2,6] with last merged [1,3]. They overlap (2 ≤ 3), so merge into [1,6]. Step 4: Compare [8,10] with last merged [1,6]. No overlap (8 > 6), append [8,10]. 
- Step 5: Compare [15,18] with last merged [8,10]. No overlap (15 > 10), append [15,18]. 

Result: [[1,6],[8,10],[15,18]].
Input Format

The first line contains an integer denoting the number of intervals.
The second line contains an integer denoting the length of individual interval array.
Each of the next N lines contains two space-separated integers startTime and endTime
Intervals may be provided in any order; duplicates and fully contained intervals are allowed.
Example

4
2
1 3
2 6
8 10
15 18
here, 4 is the number of intervals, 2 is the length of individual interval array, followed by the intervals.

Constraints

0 <= intervals.length <= 100000
intervals[i].length == 2 for all 0 <= i < intervals.length
0 <= intervals[i][0] < intervals[i][1] <= 10^9 for all 0 <= i < intervals.length
Output Format

Return a 2D array of two space-separated integers start and end, representing the merged intervals sorted by increasing start time.
Sample Input 0

0
0
Sample Input 1

1
2
5 10
Sample Output 1

5 10

## 💻 알고리즘 코드

```javascript
// 백준 스타일 입력 — require("fs").readFileSync 지원
const input = require("fs").readFileSync("/dev/stdin", "utf8").trim();
const [N,M,...inputStr] = input.split("\n");

const inputs = inputStr.map((s)=>s.split(" ").map(Number))

function mergeHighDefinitionIntervals(intervals) {
    if(intervals.length ===0)return []
    // Write your code here
    const sorted = intervals.sort((a,b)=> a[0] - b[0])
    const result = [sorted[0]]
    
    for(let i =1; i<sorted.length; i++){
        const [s,e] = result[result.length -1]
        const [ns,ne] = sorted[i]
        if(e >= ns) {
            result[result.length -1][1] = Math.max(ne,e) // 중요
        } else {
            result.push(sorted[i])
        }
    }
    return result
}

console.log(mergeHighDefinitionIntervals(inputs))
```

## 📥 입력과 출력

### 입력

```
0
0
```

### 출력

```
[]
```

## 📊 복잡도 분석

| 구분 | 복잡도 |
|------|--------|
| ⏱️ 시간 복잡도 | **O(n log n)** |
| 💾 공간 복잡도 | **O(n)** |

> 반복문 1개, 빌트인 메서드 5개 감지. 시간 복잡도 O(n log n)(선형 로그 시간 — 효율적 정렬 수준), 공간 복잡도 O(n).

#### 상세 분석

- 📦 **Line 3** `input.split("\n")` — String.split()는 O(n)
- 📦 **Line 5** `inputStr.map((s)=>s.split(" ").map(Number))` — Array.map()는 O(n)
- 📦 **Line 5** `s.split(" ").map(Number)` — Array.map()는 O(n)
- 📦 **Line 5** `s.split(" ")` — String.split()는 O(n)
- 📦 **Line 11** `intervals.sort((a,b)=> a[0] - b[0])` — Array.sort()는 평균 O(n log n)
- 🔄 **Line 14** `for(let i =1; i<sorted.length; i++){` — 반복문 중첩 깊이 1 → O(n)

## 🔍 실행 흐름 분석

총 **7개**의 실행 단계가 기록되었습니다.

| Step | Line | input | N | M | inputStr | inputs | mergeHighDefinitionIntervals | intervals | 설명 |
|------|------|------|------|------|------|------|------|------|------|
| 1 | 2 | "0
0" | - | - | - | - | - | - | const input = "0
0" |
| 2 | 3 | "0
0" | "0" | "0" | [] | - | - | - | const destructured = ["0", "0"] |
| 3 | 5 | "0
0" | "0" | "0" | [] | [] | - | - | const inputs = [] |
| 4 | 8 | "0
0" | "0" | "0" | [] | [] | [Function] | - | function mergeHighDefinitionIntervals() declared |
| 5 | 9 | "0
0" | "0" | "0" | [] | [] | [Function] | [] | if (if(intervals.length ===0)return []) → true |
| 6 | 9 | "0
0" | "0" | "0" | [] | [] | [Function] | [] | return [] |
| 7 | 26 | "0
0" | "0" | "0" | [] | [] | [Function] | - | console.log(mergeHighDefinitionIntervals(inputs))() called |

## 💡 핵심 포인트

result[result.length -1][1] = Math.max(ne,e) // 중요
더 큰값이 들어가야함!!!!

---

> 🤖 이 포스트는 **Algorithm Flow** 시각화 도구를 통해 자동으로 생성되었습니다.
> 📅 생성 일시: 2026. 2. 28. 오전 11:12:54
