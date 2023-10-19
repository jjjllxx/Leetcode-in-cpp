# Dynamic Programming
## Time Complexity
Time Complexity = (Number of State) * (Time to Calculate Single State)

## 0-1 Knapsack
### Recursion(Time Complexity is not ok)
``` cpp
dfs(i, c) = max(dfs(i - 1, c) , dfs(i - 1, c - w[i]) + v[i])
``` 
``` cpp
int zeroOneKnapsack(const int          i,
                    const int          capacity,
                    const vector<int>& weights,
                    const vector<int>& values)
{
    if (i < 0)
    {
        return 0;
    }

    if (weights[i] > capacity)
    {
        return zeroOneKnapsack(i - 1, capacity, weights, values);
    }

    return max(zeroOneKnapsack(i - 1, capacity, weights, values),
               zeroOneKnapsack(i - 1, capacity - weights[i], weights, values) + values[i]);
}
```
### Variants
1. At most `capacity`, to calculate `number of plans`/`maximum value`.
2. Exact `capacity`, to caculate `number of plans`/`maximum value`/`min value`.
3. At least `capacity`, to calculate `number of plans`/`minimum value`.

To calculate `number of plans`: 
``` cpp
dfs(i, c) = dfs(i - 1, c) + dfs(i - 1, c - w[i]) // recursion
f[i][c] = f[i - 1][c] + f[i - 1][c - w[i]] // use memorization array
f[i + 1][c] = f[i][c] + f[i][c - w[i]] // to avoid negative index
```
### Optimization
1. Scrolling Array.
``` cpp
f[(i + 1) % 2][c] = f[i % 2][c] + f[i % 2][c - w[i]]
```
2. One Array (calculate from right to left)
``` cpp
f[c] = f[c] + f[c - w[i]]
```
## Unbounded Knapsack
### Recursion(Time Complexity is not ok)
The number of each goods is unlimited.
``` cpp
dfs(i, c) = max(dfs(i - 1, c) , dfs(i, c - w[i]) + v[i])
```
``` cpp
int unboundedKnapsack(const int          i,
                      const int          capacity,
                      const vector<int>& weights,
                      const vector<int>& values)
{
    if (i < 0)
    {
        return 0;
    }

    if (weights[i] > capacity)
    {
        return unboundedKnapsack(i - 1, capacity, weights, values);
    }

    return max(unboundedKnapsack(i - 1, capacity, weights, values),
               unboundedKnapsack(i, capacity - weights[i], weights, values) + values[i]);
}
```
### Variants
1. At most `capacity`, to calculate `number of plans`/`maximum value`.
2. Exact `capacity`, to caculate `number of plans`/`maximum value`/`min value`.
3. At least `capacity`, to calculate `number of plans`/`minimum value`.

To calculate `minimum value`: 
``` cpp
dfs(i, c) = min(dfs(i - 1, c) + dfs(i, c - w[i]) + v[i]) // recursion
f[i][c] = min(f[i - 1][c], f[i][c - w[i]] + v[i]) // use memorization array
f[i + 1][c] = min(f[i][c], f[i + 1][c - w[i]] + v[i]) // to avoid negative index
```
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

## State Machine
### Unlimited trade times
`dfs(i, 0)`: by the end of day `i`, the maximum profit of not holding a stock.   
`dfs(i, 1)`: by the end of day `i`, the maximum profit of holding a stock.   
The end of day `i - 1` equals to the start of day `i`.  
``` cpp
dfs(i, 0) = max(dfs(i - 1, 0), dfs(i - 1, 1) + prices[i]);
dfs(i, 1) = max(dfs(i - 1, 1), dfs(i - 1, 0) - prices[i]);
```
Base Case:
``` cpp
dfs(-1, 0) = 0;    // At the start of day 0, the profit is 0 if don't hold a stock.
dfs(-1, 1) = -∞;   // At the start of day 0, it is impossible to hold a stock. 
```
Recursive Entry
``` cpp
max(dfs(n - 1, 0), dfs(n - 1, 1)) = dfs(n - 1, 0);
```
Transfer to dp:
``` cpp
f[0][0] = 0;
f[0][1] = -∞;
f[i + 1][0] = max(f[i][0], f[i][1] + prices[i]);
f[i + 1][1] = max(f[i][1], f[i][0] - prices[i]);
// The answer is f[n][0]
```
### With Cooldown
``` cpp
dfs(i, 0) = max(dfs(i - 1, 0), dfs(i - 1, 1) + prices[i]);
dfs(i, 1) = max(dfs(i - 1, 1), dfs(i - 2, 0) - prices[i]);
```
### Trade at most k times
`dfs(i, j, 0)`: by the end of day `i`, completing at most `j` times of trade, the maximum profit of not holding a stock.   
`dfs(i, j, 1)`: by the end of day `i`, completing at most `j` times of trade, the maximum profit of holding a stock.   
``` cpp
dfs(i, j, 0) = max(dfs(i - 1, j, 0), dfs(i - 1, j, 1) + prices[i]);
dfs(i, j, 1) = max(dfs(i - 1, j, 1), dfs(i - 1, j - 1, 0) - prices[i]);
```
Base Case:
``` cpp
dfs(·, -1, ·) = -∞;   // j cannot be negative.
dfs(-1, j, 0) = 0;    // At the start of day 0, the profit is 0 if don't hold a stock.
dfs(-1, j, 1) = -∞;   // At the start of day 0, it is impossible to hold a stock. 
```
Recursive Entry
``` cpp
max(dfs(n - 1, k, 0), dfs(n - 1, k, 1)) = dfs(n - 1, k, 0);
```
Transfer to dp:
``` cpp
f[·][0][·] = -∞;
f[0][j][0] = 0;  // for j >= 1
f[0][j][1] = -∞; // for j >= 1
f[i + 1][j][0] = max(f[i][j][0], f[i][j][1] + prices[i]);
f[i + 1][j][1] = max(f[i][j][1], f[i][j - 1][0] - prices[i]);
// The answer is f[n][k + 1][0]
```
Space optimization
``` cpp
int maxProfit(int k, vector<int>& prices)
{
    vector<int> dp0(k + 2), dp1(k + 2, INT_MIN >> 1);
    dp0[0] = INT_MIN >> 1; // INT_MIN should change to other small value to prevent overflow.

    for (int p : prices)
    {
        for (int j = k + 1; j >= 1; --j) // Update larger j first
        {
            dp0[j] = max(dp0[j], dp1[j] + p);
            dp1[j] = max(dp1[j], dp0[j - 1] - p);
        }
    }

    return dp0[k + 1];
}
```
### Trade exact k times
``` cpp
f[·][j][·] = -∞; // for j != 1
f[0][0][0] = 0; 
f[i + 1][j][0] = max(f[i][j][0], f[i][j][1] + prices[i]);
f[i + 1][j][1] = max(f[i][j][1], f[i][j - 1][0] - prices[i]);
// The answer is f[n][k + 1][0]
```

``` cpp
int exactK(int k, vector<int>& prices)
{
    vector<int> dp0(k + 2, INT_MIN >> 1), dp1(k + 2, INT_MIN >> 1);
    dp0[1] = 0;

    for (int p : prices)
    {
        for (int j = k + 1; j >= 1; --j)
        {
            dp0[j] = max(dp0[j], dp1[j] + p);
            dp1[j] = max(dp1[j], dp0[j - 1] - p);
        }
    }

    return dp0[k + 1];
}
```

### Trade at least k times
``` cpp
f[·][j][·] = -∞; // for j >= 1
f[0][0][0] = 0; 
f[i + 1][j][0] = max(f[i][j][0], f[i][j][1] + prices[i]);      // j >= 1
f[i + 1][j][1] = max(f[i][j][1], f[i][j - 1][0] - prices[i]);  // j >= 1

f[i + 1][0][0] = max(f[i][0][0], f[i][0][1] + prices[i]);      // j >= 1
f[i + 1][0][1] = max(f[i][0][1], f[i][0][0] - prices[i]);  // j >= 1
// The answer is f[n][k + 1][0]
```

``` cpp
int atLeastK(int k, vector<int>& prices)
{
    vector<int> dp0(k + 1, INT_MIN >> 1), dp1(k + 1, INT_MIN >> 1);

    dp0[0] = 0;
    int tmp;

    for (int p : prices)
    {
        for (int j = k; j >= 1; --j)
        {
            dp0[j] = max(dp0[j], dp1[j] + p);
            dp1[j] = max(dp1[j], dp0[j - 1] - p);
        }

        tmp = dp0[0];
        dp0[0] = max(dp0[0], dp1[0] + p);
        dp1[0] = max(dp1[0], tmp - p);
    }

    return dp0[k];
}
```
