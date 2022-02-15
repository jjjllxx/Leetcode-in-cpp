# 70. Climbing Stairs
https://leetcode-cn.com/problems/climbing-stairs  
You are climbing a staircase. It takes n steps to reach the top.
Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Example 1:   
Input: n = 2  
Output: 2  
Explanation: There are two ways to climb to the top.  
1. 1 step + 1 step  
2. 2 steps  

Example 2:  
Input: n = 3  
Output: 3  
Explanation: There are three ways to climb to the top.  
1. 1 step + 1 step + 1 step  
2. 1 step + 2 steps  
3. 2 steps + 1 step  

Constraints:  
1 <= n <= 45   

``` cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n<4) return n;
        int f0=2,f1=3;
        for(int i=4;i<=n;i++){
            swap(f0,f1);
            f1+=f0;
        }
        return f1;
    }
};
```
