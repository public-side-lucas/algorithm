---
title: "Find Peak Element in Bitonic Array"
date: 2026-02-28
category: 탐색
difficulty: easy
---

# Find Peak Element in Bitonic Array

| 항목 | 내용 |
|------|------|
| 📅 작성일 | 2026-02-28 |
| 📁 카테고리 | 탐색 |
| 🎯 난이도 | 🟢 쉬움 |
| ⏱️ 시간 복잡도 | **O(n)** |
| 💾 공간 복잡도 | **O(n)** |

## 📝 개요

Given a bitonic array (strictly increasing then strictly decreasing), find the index of the maximum element in O(log n) time.

Example

Input:

counts = [1, 3, 5, 4, 2]
Output:

2
Explanation:

We perform a binary search on counts:

low = 0, high = 4. mid = (0 + 4) // 2 = 2. counts[2] = 5, counts[3] = 4. Since 5 > 4, we are on the descending side, so we move high = mid = 2.
low = 0, high = 2. mid = (0 + 2) // 2 = 1. counts[1] = 3, counts[2] = 5. Since 3 < 5, we are on the ascending side, so we move low = mid + 1 = 2.
Now low = 2, high = 2, loop ends and we return 2, which is the index of the maximum element (5).
Input Format

The input consists of two lines:

A single integer n (3 ≤ n ≤ 100000), the length of the array counts.
n space-separated integers counts[0] through counts[n-1], each 0 ≤ counts[i] ≤ 1,000,000, all distinct and forming a strictly increasing sequence up to a single peak, then strictly decreasing.
Constraints

1 <= counts.length <= 100000
0 <= counts[i] <= 1000000 for all 0 <= i < counts.length
All counts[i] are distinct
There exists an index p (0 < p < counts.length - 1) such that:
for all 1 <= i <= p: counts[i] > counts[i - 1]
for all p + 1 <= i < counts.length: counts[i] < counts[i - 1]
Output Format

Output a single integer: the 0-based index of the maximum element in the provided bitonic array.

Sample Input 0

3
1
3
2
Sample Output 0

1
Sample Input 1

5
1
2
3
2
1
Sample Output 1

2

## 💻 알고리즘 코드

```javascript
// 백준 스타일 입력 — require("fs").readFileSync 지원
const input = require("fs").readFileSync("/dev/stdin", "utf8").trim();
const [sizeStr, ...inputStr ] = input.split("\n");
const size = Number(sizeStr)
const counts = inputStr.map(Number)


/*
 * Complete the 'findPeakIndex' function below.
 *
 * The function is expected to return an INTEGER.
 * The function accepts INTEGER_ARRAY counts as parameter.
 */

function findPeakIndex(counts) {
    // Write your code here
    let left = 0
    let right = counts.length-1
    let mid = 0
    
    while(left<right){
        mid = Math.ceil((left+right)/2)
        
        if( counts[mid] > counts[mid-1]){
            left = mid  
        } else {
            right = mid - 1
        } 
    }
    
    return left
}

console.log(findPeakIndex(counts))
```

## 📥 입력과 출력

### 입력

```
5
1
2
3
2
1
```

### 출력

```
2
```

## 📊 복잡도 분석

| 구분 | 복잡도 |
|------|--------|
| ⏱️ 시간 복잡도 | **O(n)** |
| 💾 공간 복잡도 | **O(n)** |

> 반복문 1개, 빌트인 메서드 2개 감지. 시간 복잡도 O(n)(선형 시간 — 입력에 비례), 공간 복잡도 O(n).

#### 상세 분석

- 📦 **Line 3** `input.split("\n")` — String.split()는 O(n)
- 📦 **Line 5** `inputStr.map(Number)` — Array.map()는 O(n)
- 🔄 **Line 21** `while(left<right){` — 반복문 중첩 깊이 1 → O(n)

## 🔍 실행 흐름 분석

총 **19개**의 실행 단계가 기록되었습니다.

| Step | Line | input | sizeStr | inputStr | size | counts | findPeakIndex | left | right | mid | 설명 |
|------|------|------|------|------|------|------|------|------|------|------|------|
| 1 | 2 | "5
1
2
3
2
1" | - | - | - | - | - | - | - | - | const input = "5
1
2
3
2
1" |
| 2 | 3 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | - | - | - | - | - | - | const destructured = ["5", "1", "2", "3", "2", "1"] |
| 3 | 4 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | - | - | - | - | - | const size = 5 |
| 4 | 5 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | - | - | - | - | const counts = [1, 2, 3, 2, 1] |
| 5 | 15 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | - | - | - | function findPeakIndex() declared |
| 6 | 17 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 0 | - | - | let left = 0 |
| 7 | 18 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 0 | 4 | - | let right = 4 |
| 8 | 19 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 0 | 4 | 0 | let mid = 0 |
| 9 | 21 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 0 | 4 | 0 | while (while(left<right){) → true |
| 10 | 22 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 0 | 4 | 2 | mid = 2 |
| 11 | 24 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 0 | 4 | 2 | if (if( counts[mid] > counts[mid-1]){) → true |
| 12 | 25 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 2 | 4 | 2 | left = 2 |
| 13 | 21 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 2 | 4 | 2 | while (while(left<right){) → true |
| 14 | 22 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 2 | 4 | 3 | mid = 3 |
| 15 | 24 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 2 | 4 | 3 | if (if( counts[mid] > counts[mid-1]){) → false |
| 16 | 27 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 2 | 2 | 3 | right = 2 |
| 17 | 21 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 2 | 2 | 3 | while (while(left<right){) → false |
| 18 | 31 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | 2 | 2 | 3 | return 2 |
| 19 | 34 | "5
1
2
3
2
1" | "5" | ["1", "2", "3", "2", "1"] | 5 | [1, 2, 3, 2, 1] | [Function] | - | - | - | console.log(findPeakIndex(counts))() called |

## 💡 핵심 포인트

이진 탐색 Peak Finding 핵심 정리
1. ceil vs floor 선택 규칙
이게 가장 많이 헷갈렸던 부분이야. 규칙은 하나:

mid가 대입되는 쪽의 반대로 밀어라

right = mid 있으면left = mid 있으면floor 사용ceil 사용
섞으면 무한루프 발생.
2. 비교 대상과 대입 패턴은 세트
세트비교대입mid 계산Amid+1과 비교left = mid+1, right = midfloorBmid-1과 비교left = mid, right = mid-1ceil
A세트 비교에 B세트 대입을 섞으면 답을 건너뛰거나 무한루프가 발생해.
3. mid가 답 후보인지 판단
right = mid - 1은 mid를 완전히 버리는 거야. mid가 답일 수 있는 상황에서 이렇게 하면 답을 놓쳐. peak 문제에서 counts[mid] >= counts[mid+1]이면 mid 자체가 peak 후보니까 right = mid로 살려둬야 했어.
4. 경계 체크
counts[mid+1]이나 counts[mid-1] 접근 시 배열 범위를 벗어날 수 있어. while(left < right) 조건이 이걸 보호해주는지 항상 확인해야 해.

이진 탐색 문제 만나면 코드 짜기 전에 항상 이 순서로 정리해봐:

어떤 조건에서 어느 쪽을 버릴지 결정
mid가 답 후보인지 확인 → mid vs mid ± 1 대입 결정
그에 맞는 floor/ceil 선택

---

> 🤖 이 포스트는 **Algorithm Flow** 시각화 도구를 통해 자동으로 생성되었습니다.
> 📅 생성 일시: 2026. 2. 28. 오후 1:59:21
