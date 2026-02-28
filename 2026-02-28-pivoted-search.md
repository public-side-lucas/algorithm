---
title: "Pivoted Search"
date: 2026-02-28
category: 탐색
difficulty: medium
---

# Pivoted Search

| 항목 | 내용 |
|------|------|
| 📅 작성일 | 2026-02-28 |
| 📁 카테고리 | 탐색 |
| 🎯 난이도 | 🟡 보통 |
| ⏱️ 시간 복잡도 | **O(n)** |
| 💾 공간 복잡도 | **O(n)** |

## 📝 개요


Given a sorted array of unique integers that has been rotated at an unknown pivot, find the index of a target value or return -1 if not found.

Example

Input:

nums = [1609466400, 1609470000, 1609473600, 1609459200, 1609462800]
target = 1609459200
Output:

3
Explanation:

We perform a binary search on the rotated array:

left=0, right=4, mid=(0+4)//2=2, nums[mid]=1609473600.
nums[left]=1609466400 <= nums[mid], so the left half [indices 0..2] is sorted. Target 1609459200 is not in [1609466400..1609473600], so search in right half: left=mid+1=3.
Now left=3, right=4, mid=(3+4)//2=3, nums[mid]=1609459200, which equals the target. Return index 3.
Input Format

The input is given in three lines.

Line 1: an integer n (0 ≤ n ≤ 100000), the number of timestamps.

Line 2: n space-separated long integers nums[i] (0 ≤ nums[i] ≤ 10^18), representing a rotated version of a strictly increasing array of unique Unix timestamps.

Line 3: a single long integer target (0 ≤ target ≤ 10^18), the timestamp to search for. The sequence in nums is guaranteed to be the result of rotating an originally strictly increasing sorted array at an unknown pivot.

Constraints

0 <= nums.length <= 100000
0 <= nums[i] <= 10^18
All elements in nums are unique
nums is obtained by taking a strictly increasing sorted array and rotating it at an unknown pivot
0 <= target <= 10^18
Output Format

Output a single integer: the 0-based index of target in nums if it exists; otherwise output -1.

Sample Input 0

0
5
Sample Output 0

-1
Sample Input 1

1
100
100
Sample Output 1

0

## 💻 알고리즘 코드

```javascript
// 백준 스타일 입력 — require("fs").readFileSync 지원
const input = require("fs").readFileSync("/dev/stdin", "utf8").trim();
const lines = input.split("\n");
const n = Number(lines[0])
const nums = lines.slice(1, n+1).map(Number)
const target = Number(lines[lines.length -1])

function searchRotatedTimestamps(nums, target) {
    // Write your code here
    // return nums.findIndex((value)=> value === target)
    
    let left = 0
    let right =nums.length -1; 
    
    while(left <= right){
        const mid = Math.ceil((right + left)/2)
        if(nums[mid] === target)return mid
        
        if(nums[left] <= nums[mid]){
            if(nums[left] <= target && target < nums[mid]){
                right = mid -1
            } else {
                left = mid +1
            }
        } else {
          if(nums[mid] < target && target <= nums[right]){
                left = mid +1
            } else {
                right = mid -1
            }
        }
    }
    
    return -1
}

console.log(nums)
console.log(target)

console.log(searchRotatedTimestamps(nums,target))
```

## 📥 입력과 출력

### 입력

```
8
7
8
1
2
3
4
5
6
3
```

### 출력

```
[7, 8, 1, 2, 3, 4, 5, 6]
3
4
```

## 📊 복잡도 분석

| 구분 | 복잡도 |
|------|--------|
| ⏱️ 시간 복잡도 | **O(n)** |
| 💾 공간 복잡도 | **O(n)** |

> 반복문 1개, 빌트인 메서드 3개 감지. 시간 복잡도 O(n)(선형 시간 — 입력에 비례), 공간 복잡도 O(n).

#### 상세 분석

- 📦 **Line 3** `input.split("\n")` — String.split()는 O(n)
- 📦 **Line 5** `lines.slice(1, n+1).map(Number)` — Array.map()는 O(n)
- 📦 **Line 5** `lines.slice(1, n+1)` — Array.slice()는 O(n) 복사
- 🔄 **Line 17** `while(left <= right){` — 반복문 중첩 깊이 1 → O(n)

## 🔍 실행 흐름 분석

총 **15개**의 실행 단계가 기록되었습니다.

| Step | Line | input | lines | n | nums | target | searchRotatedTimestamps | left | right | mid | 설명 |
|------|------|------|------|------|------|------|------|------|------|------|------|
| 1 | 2 | "8
7
8
1
2
3
4
5
6
3" | - | - | - | - | - | - | - | - | const input = "8
7
8
1
2
3
4
5
6
3" |
| 2 | 3 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | - | - | - | - | - | - | - | const lines = ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] |
| 3 | 4 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | - | - | - | - | - | - | const n = 8 |
| 4 | 5 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | - | - | - | - | - | const nums = [7, 8, 1, 2, 3, 4, 5, 6] |
| 5 | 6 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | 3 | - | - | - | - | const target = 3 |
| 6 | 10 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | 3 | [Function] | - | - | - | function searchRotatedTimestamps() declared |
| 7 | 39 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | 3 | [Function] | - | - | - | console.log(nums)() called |
| 8 | 40 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | 3 | [Function] | - | - | - | console.log(target)() called |
| 9 | 14 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | 3 | [Function] | 0 | - | - | let left = 0 |
| 10 | 15 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | 3 | [Function] | 0 | 7 | - | let right = 7 |
| 11 | 17 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | 3 | [Function] | 0 | 7 | - | while (while(left <= right){) → true |
| 12 | 18 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | 3 | [Function] | 0 | 7 | 4 | const mid = 4 |
| 13 | 19 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | 3 | [Function] | 0 | 7 | 4 | if (if(nums[mid] === target)return mid) → true |
| 14 | 19 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | 3 | [Function] | 0 | 7 | 4 | return 4 |
| 15 | 42 | "8
7
8
1
2
3
4
5
6
3" | ["8", "7", "8", "1", "2", "3", "4", "5", "6", "3"] | 8 | [7, 8, 1, 2, 3, 4, 5, 6] | 3 | [Function] | - | - | - | console.log(searchRotatedTimestamps(nums,target))() called |

## 💡 핵심 포인트

nums.findIndex((value)=> value === target) 로 하는 것과 이진탐색하는 것의 이유를 알고 사용하자

---

> 🤖 이 포스트는 **Algorithm Flow** 시각화 도구를 통해 자동으로 생성되었습니다.
> 📅 생성 일시: 2026. 2. 28. 오후 1:31:31
