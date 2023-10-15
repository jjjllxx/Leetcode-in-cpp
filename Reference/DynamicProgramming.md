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
