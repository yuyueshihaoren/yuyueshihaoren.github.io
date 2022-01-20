---
layout: post
date:   2022-01-20
categories: [programming]
math: true
id: 10
comment: true
---

# 1143. Longest Common Subsequence
https://leetcode.com/problems/longest-common-subsequence/
#leetcode-medium 

Given two strings `text1` and `text2`, return _the length of their longest **common subsequence**._ If there is no **common subsequence**, return `0`.

## My analysis
This is similar to the problem of edit distance. (DPV 6.3 Edit distance)

Define $m,n$ to be the length of `text1` and `text2`, respectively.

(**1-indexed** here)
Let me define the subproblem:
$Lc(i,j)$ = max length of common subsequence of sub-string of `text1` till index $i$ and sub-string of `text2` till $j$

Find the relation:
There are 2 cases and two options in case 2:
1. $text1_i$ matches $text2_j$, get 1 point.
2. $text1_i$ does not matches $text2_j$, get 0 point.
    1. keep $text1\_i$ and compare it with $text2\_{j-1}$ .
    2. Keep $text2\_{j}$ and compare it with $text1\_{i-1}$ .

We take maximum of these cases.

The relation:
$$
Lc(i,j) = \max\{1 + Lc(i-1,j-1)\; if\; text1_i=text2_j,
Lc(i-1,j), Lc(1, j-1)\}
$$

Base case:
$Lc(0,0) = 0$, suggesting two empty strings have 0 length common subsequence.

Goal:
$Lc(m+1,n+1)$

## My solution

#pseudo-code 
```pseudo-code
procedure longestCommonSubsequence
---
Input: text1, text2 with length m,n
Output: Longest common subsequence between text1 and text2
---
// text1, text2 are 1-indexed
initialize 2-d array lc of size (m+1,n+1), filled with 0
lc(0,0) = 0

for i = 1...m:
    for j = 1...n:
        case1_score = 1 if text1(i) == text2(j) else 0
        lc(i,j) = max{
        case1_score + lc(i-1,j-1),
        lc(i-1,j),
        lc(i,j-1)
        }
```

Python code:

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m,n = len(text1), len(text2)
        
        dp = [[0 for _ in range(n+1)] for _ in range(m+1)]
        
        for i in range(1,m+1):
            for j in range(1, n+1):
                align = 0
                if text1[i-1] == text2[j-1]:
                    align = 1 + dp[i-1][j-1]
                
                dp[i][j] = max(align, dp[i-1][j], dp[i][j-1])
        
        return dp[-1][-1]
```