# Subsequence
## Longest Common Subsequence (LCS)
### Definition
1. subarray/substring: continuous
2. subsequence: do not have to be continous

### Formula
Assuming string `s` and `t`:
``` cpp
dfs(i, j) = max(dfs(i - 1, j), dfs(i, j - 1), dfs(i - 1, j - 1) + s[i] != t[j])
```
Simplify to:
``` cpp
dfs(i, j) = dfs(i - 1, j - 1) + 1               s[i] == t[j];
dfs(i, j) = max(dfs(i, j - 1), dfs(i, j - 1))   s[i] != t[j];
```
### Edit Distance
``` cpp
dfs(i, j) = dfs(i - 1, j - 1)                                         s[i] == t[j];
dfs(i, j) = min(dfs(i, j - 1), dfs(i, j - 1), dfs(i - 1, j - 1)) + 1  s[i] != t[j];
```

## Longest Increasing Subsequence (LIS)
### Formula
``` cpp
dfs(i) = max{dfs(j)}   j < i && nums[j] < nums[i];
f[i] = max{f[j]}       j < i && nums[j] < nums[i];
```
### Connection with LCS
The LCS of sorted nums with original nums is its LIS.

### Skill: Swap state and state value
f[i] expresses the length of LIS with ending element nums[i].
g[i] expresses the minimun ending element of LIS with length i + 1.
