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
Example: [1039. Minimum Score Triangulation of Polygon](https://leetcode.com/problems/minimum-score-triangulation-of-polygon/)
Recursion:
``` cpp
dfs(i, j) = min(dfs(i, k) + dfs(k, j) + v[i] * v[j] * v[k] ); // k from i + 1 to j - 1
```
Base Case:
``` cpp
dfs(i, i + 1) = 0; // Only two points cannot form a triangle.
```
Recursive Entry
``` cpp
dfs(0, n - 1);
```
Code:
``` cpp
int dfs(const int i, const int j, const vector<int>& values)
{
    if (j - i == 1)
    {
        return 0;
    }

    int mn = INT_MAX, side = values[i] * values[j];
    for (int k = i + 1; k < j; ++k)
    {
        mn = min(mn, dfs(i, k, values) + dfs(k, j, values) + side * values[k]);
    }

    return mn;
}
```
Use array:
``` cpp
f[i][j] = min(f[i][k] + f[k][j] + v[i] * v[j] * v[k] ); // k from i + 1 to j - 1
f[0][n - 1] // Answer
```
Order:  
1. i < k, f[i] comes from f[k], so enumerate `i` from large to small.
2. j > k, f[i][j] comes from f[i][k], so enumerate `j` from small to large. 