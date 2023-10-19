# State Machine
## Unlimited trade times
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
## With Cooldown
``` cpp
dfs(i, 0) = max(dfs(i - 1, 0), dfs(i - 1, 1) + prices[i]);
dfs(i, 1) = max(dfs(i - 1, 1), dfs(i - 2, 0) - prices[i]);
```
## Trade at most k times
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
## Trade exact k times
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
## Trade at least k times
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
