# 254. Factor Combinations
https://leetcode-cn.com/problems/factor-combinations/  
Numbers can be regarded as the product of their factors.  
For example, 8 = 2 x 2 x 2 = 2 x 4.  
Given an integer n, return all possible combinations of its factors. You may return the answer in any order.  
Note that the factors should be in the range [2, n - 1].  

Example 1:  
Input: n = 1  
Output: []  

Example 2:  
Input: n = 12  
Output: [[2,6],[3,4],[2,2,3]]  

Example 3:  
Input: n = 37  
Output: []  

Constraints:  
1 <= n <= 10^7  

``` cpp
class Solution {
public:
    vector<vector<int>> ans;

    vector<vector<int>> backtrack(int n,int start){
        vector<vector<int>> res;
        for (int i = start; i * i <= n; ++i) {
            if (n % i == 0) {
                res.push_back({i, n / i});
                vector<vector<int>> tmp=backtrack(n / i, i);
                for (auto v : tmp) {
                    v.push_back(i);
                    res.push_back(v);
                }
            }
        }
        return res;
    }

    vector<vector<int>> getFactors(int n) {
        return backtrack(n,2);
    }
};
```
