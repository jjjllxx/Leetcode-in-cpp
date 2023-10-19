# Intervaal Dynamic Programming
## Difference
1. Linear DP: Transfer from prefix/suffix.
2. Interval DP: Transfer from small interval to large interval.

## Choose or Not Choose
Reduce the size of the problem from both sides inward.  
Example: [516. Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/description/)
Method 1: Calculate the LCS between string and reversed string.  
Method 2: Consider from two sides inward.
``` cpp
dfs(i, j) = dfs(i + 1, j - 1);                  // s[i] == s[j]
dfs(i, j) = max(dfs(i + 1, j), dfs(i, j - 1));  // s[i] != s[j]
```
Base Case:
``` cpp
dfs(i, i) = 1;     // i == j
dfs(i + 1 ,i) = 0; // i > j
```
Recursive Entry
``` cpp
dfs(0, n - 1);
```
DP:
``` cpp
f[i][j] = 0;                             // i > j
f[i][j] = 1;                             // i == j
f[i][j] = f[i + 1][j - 1] + 2;           // s[i] == s[j]
f[i][j] = max(f[i + 1][j], f[i][j - 1]); // s[i] != s[j]
```
## Enumerate Next
Divide it into multiple smaller sub-problems.


